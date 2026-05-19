# Scripts de Seguridad — [Nombre del Proyecto]

Scripts bash de apoyo al protocolo de auditoría **security-audit-github**.
Organizados en dos categorías: **verificación** (solo reportan, no modifican)
y **corrección** (aplican fixes básicos con confirmación explícita).

> ⚠️ Ejecutar siempre desde la raíz del repositorio.
> Los scripts de corrección solicitan confirmación antes de modificar archivos.

---

## Índice

1. [Requisitos](#requisitos)
2. [Scripts de Verificación](#scripts-de-verificación)
   - [verify_hygiene.sh — Higiene base del repo](#verify_hygienesh)
   - [verify_secrets.sh — Detección de secretos](#verify_secretssh)
   - [verify_headers.sh — Cabeceras y hardening frontend](#verify_headerssh)
   - [verify_deps.sh — Dependencias y versiones](#verify_depssh)
3. [Scripts de Corrección](#scripts-de-corrección)
   - [fix_gitignore.sh — Agregar reglas de seguridad al .gitignore](#fix_gitignore)
   - [fix_headers.sh — Insertar meta CSP básica en HTML](#fix_headerssh)
4. [Uso en CI/CD](#uso-en-cicd)

---

## Requisitos

- `bash` >= 4.0
- `grep`, `find`, `sed` (incluidos en cualquier sistema Unix/Linux/macOS)
- `git` para scripts que analizan historial
- Opcional: `gitleaks` para análisis forense de secretos en historial

---

## Scripts de Verificación

### verify_hygiene.sh

Verifica la presencia de archivos base de higiene del repositorio.
**No modifica nada.**

```bash
#!/usr/bin/env bash
# verify_hygiene.sh — Verifica archivos base de higiene del repo
# Uso: bash scripts/verify_hygiene.sh

set -euo pipefail

PASS=0
WARN=0
FAIL=0

check() {
  local label="$1"
  local file="$2"
  if [[ -f "$file" ]]; then
    echo "  ✅ PASS — $label ($file)"
    ((PASS++))
  else
    echo "  ❌ FAIL — $label no encontrado: $file"
    ((FAIL++))
  fi
}

warn() {
  local label="$1"
  local condition="$2"
  echo "  ⚠️  WARN — $label: $condition"
  ((WARN++))
}

echo "=== Verificación de higiene base ==="
echo ""

check "Licencia"              "LICENSE"
check "README"                "README.md"
check "Política de seguridad" "SECURITY.md"
check ".gitignore"            ".gitignore"

# Verificar que .gitignore tenga reglas para secretos
# NOTA: grep lee el archivo de texto .gitignore buscando esas palabras
# como reglas escritas — no accede a variables de entorno ni al sistema.
if [[ -f ".gitignore" ]]; then
  if grep -qiE '\.env|\.pem|\.key|secret|credential' .gitignore; then
    echo "  ✅ PASS — .gitignore contiene reglas para secretos/credenciales"
    ((PASS++))
  else
    warn ".gitignore existe pero sin reglas para secretos (.env, .pem, .key)" \
         "Agregar manualmente o ejecutar fix_gitignore.sh"
  fi
fi

# Verificar presencia de CI
if [[ -d ".github/workflows" ]] && compgen -G ".github/workflows/*.yml" > /dev/null 2>&1; then
  echo "  ✅ PASS — Workflows de CI/CD encontrados en .github/workflows/"
  ((PASS++))
else
  echo "  ❌ FAIL — Sin workflows de CI/CD (.github/workflows/)"
  ((FAIL++))
fi

echo ""
echo "=== Resultado: $PASS PASS | $WARN WARN | $FAIL FAIL ==="

[[ $FAIL -eq 0 ]] && exit 0 || exit 1
```

---

### verify_secrets.sh

Busca patrones comunes de secretos hardcodeados en archivos de texto.
**No modifica nada. No analiza binarios.**

```bash
#!/usr/bin/env bash
# verify_secrets.sh — Detección básica de secretos en código fuente
# Uso: bash scripts/verify_secrets.sh
#
# NOTA: Este archivo contiene patrones regex para DETECTAR secretos.
# No contiene secretos reales ni valores sensibles.
# NO debe incluirse en .gitignore — debe estar versionado como parte
# del protocolo de auditoría del repositorio.

set -euo pipefail

FINDINGS=0

echo "=== Detección de secretos hardcodeados ==="
echo ""

# Patrones a buscar (ajustar según el stack del proyecto)
declare -A PATTERNS=(
  ["API Key genérica"]='(?i)(api[_-]?key|apikey)\s*[=:]\s*["\x27][A-Za-z0-9_\-]{16,}'
  ["Token Bearer"]='(?i)bearer\s+[A-Za-z0-9\-_\.]{20,}'
  ["AWS Access Key"]='AKIA[0-9A-Z]{16}'
  ["Private Key header"]='-----BEGIN (RSA |EC |OPENSSH )?PRIVATE KEY-----'
  ["Password hardcodeada"]='(?i)(password|passwd|pwd)\s*[=:]\s*["\x27][^"\x27]{6,}'
  ["Conexión con credenciales"]='(?i)(mongodb|postgres|mysql|redis):\/\/[^:]+:[^@]+@'
)

SEARCH_DIRS=("." )
EXCLUDE_DIRS=("node_modules" ".git" "vendor" "dist" "build")

# Construir argumentos de exclusión para find
EXCLUDE_ARGS=()
for dir in "${EXCLUDE_DIRS[@]}"; do
  EXCLUDE_ARGS+=(-not -path "./$dir/*")
done

# Archivos de texto a analizar
mapfile -t FILES < <(find . "${EXCLUDE_ARGS[@]}" -type f \( \
  -name "*.js" -o -name "*.ts" -o -name "*.py" -o -name "*.html" \
  -o -name "*.css" -o -name "*.json" -o -name "*.yml" -o -name "*.yaml" \
  -o -name "*.env*" -o -name "*.conf" -o -name "*.config" \
\))

for label in "${!PATTERNS[@]}"; do
  pattern="${PATTERNS[$label]}"
  results=$(grep -rPn "$pattern" "${FILES[@]}" 2>/dev/null || true)
  if [[ -n "$results" ]]; then
    echo "  🚨 HALLAZGO — $label:"
    echo "$results" | sed 's/^/     /'
    ((FINDINGS++))
  fi
done

echo ""
if [[ $FINDINGS -eq 0 ]]; then
  echo "  ✅ Sin secretos detectados con patrones básicos."
  echo "     Recomendado: ejecutar también 'gitleaks detect' para análisis de historial."
else
  echo "  ❌ $FINDINGS tipo(s) de secreto detectado(s). Revisar hallazgos arriba."
fi

echo ""
echo "⚠️  Este script realiza detección básica de patrones."
echo "   No reemplaza herramientas especializadas como gitleaks o truffleHog."

[[ $FINDINGS -eq 0 ]] && exit 0 || exit 1
```

---

### verify_headers.sh

Verifica la presencia de meta-tags de seguridad en archivos HTML del proyecto.
**No modifica nada.**

```bash
#!/usr/bin/env bash
# verify_headers.sh — Verifica hardening en archivos HTML
# Uso: bash scripts/verify_headers.sh

set -euo pipefail

PASS=0
FAIL=0

echo "=== Verificación de hardening frontend (HTML) ==="
echo ""

mapfile -t HTML_FILES < <(find . -not -path "./.git/*" -name "*.html" -type f)

if [[ ${#HTML_FILES[@]} -eq 0 ]]; then
  echo "  ℹ️  No se encontraron archivos HTML en el repositorio."
  exit 0
fi

for file in "${HTML_FILES[@]}"; do
  echo "  📄 $file"

  # Content Security Policy
  if grep -qi 'content-security-policy' "$file"; then
    echo "     ✅ CSP meta-tag presente"
    ((PASS++))
  else
    echo "     ❌ Sin Content-Security-Policy"
    ((FAIL++))
  fi

  # Subresource Integrity en recursos externos
  if grep -qiE '<(script|link)[^>]+src=["\x27]https://' "$file"; then
    if grep -qiE 'integrity=["\x27]sha(256|384|512)-' "$file"; then
      echo "     ✅ SRI (integrity) presente en recursos externos"
      ((PASS++))
    else
      echo "     ❌ Recursos externos sin Subresource Integrity (SRI)"
      ((FAIL++))
    fi
  fi

  # Recursos HTTP en lugar de HTTPS
  if grep -qiE 'src=["\x27]http://' "$file"; then
    echo "     ❌ Recursos cargados con HTTP (no HTTPS)"
    ((FAIL++))
  fi

  echo ""
done

echo "=== Resultado: $PASS PASS | $FAIL FAIL ==="
[[ $FAIL -eq 0 ]] && exit 0 || exit 1
```

---

### verify_deps.sh

Verifica el estado de dependencias del proyecto (si aplica según el stack).
**No modifica nada.**

```bash
#!/usr/bin/env bash
# verify_deps.sh — Verifica estado de dependencias
# Uso: bash scripts/verify_deps.sh

set -euo pipefail

echo "=== Verificación de dependencias ==="
echo ""

# Node.js / npm
if [[ -f "package.json" ]]; then
  echo "  📦 Stack Node.js detectado"
  if command -v npm &>/dev/null; then
    echo "  Ejecutando npm audit..."
    npm audit --audit-level=moderate || true
  else
    echo "  ⚠️  npm no disponible — instalar Node.js para auditoría de dependencias"
  fi

# Python / pip
elif [[ -f "requirements.txt" ]] || [[ -f "pyproject.toml" ]]; then
  echo "  🐍 Stack Python detectado"
  if command -v pip-audit &>/dev/null; then
    pip-audit
  elif command -v safety &>/dev/null; then
    safety check
  else
    echo "  ⚠️  pip-audit o safety no disponibles"
    echo "     Instalar con: pip install pip-audit"
  fi

# Sin gestor de dependencias detectado
else
  echo "  ℹ️  No se detectó package.json ni requirements.txt"
  echo "     Si el proyecto tiene dependencias, agregar el gestor correspondiente."
fi
```

---

## Scripts de Corrección

> ⚠️ Los scripts de corrección **modifican archivos**. Siempre piden confirmación.
> Hacer commit del estado actual antes de ejecutarlos.

### fix_gitignore.sh

Agrega reglas de seguridad estándar al `.gitignore` existente (o lo crea).

```bash
#!/usr/bin/env bash
# fix_gitignore.sh — Agrega reglas de seguridad al .gitignore
# Uso: bash scripts/fix_gitignore.sh

set -euo pipefail

RULES=$(cat <<'EOF'

# === Seguridad — agregado por security-audit-github ===
# Variables de entorno y secretos
.env
.env.*
!.env.example

# Claves y certificados
*.pem
*.key
*.p12
*.pfx
*.crt
*.cer
id_rsa
id_ed25519

# Archivos de configuración con credenciales
secrets.json
credentials.json
service-account*.json
*secret*
*credential*

# Artefactos de build
dist/
build/
*.min.js.map

# Dependencias
node_modules/
vendor/
__pycache__/
*.pyc
EOF
)

echo "=== fix_gitignore.sh ==="
echo ""
echo "Se agregarán las siguientes reglas al .gitignore:"
echo "$RULES"
echo ""
read -rp "¿Confirmar? (s/N): " confirm

if [[ "${confirm,,}" != "s" ]]; then
  echo "Cancelado."
  exit 0
fi

echo "$RULES" >> .gitignore
echo ""
echo "✅ Reglas agregadas a .gitignore"
echo "   Verificar con: git diff .gitignore"
```

---

### fix_headers.sh

Inserta un meta-tag de Content Security Policy básica en archivos HTML
que no lo tengan. **Solicita confirmación por archivo.**

```bash
#!/usr/bin/env bash
# fix_headers.sh — Inserta meta CSP básica en archivos HTML sin ella
# Uso: bash scripts/fix_headers.sh

set -euo pipefail

CSP_META='  <meta http-equiv="Content-Security-Policy" content="default-src '\''self'\''; script-src '\''self'\''; style-src '\''self'\'' https://fonts.googleapis.com; font-src '\''self'\'' https://fonts.gstatic.com; img-src '\''self'\'' data:;">'

echo "=== fix_headers.sh — Inserción de meta CSP ==="
echo ""
echo "⚠️  Ajustar la política CSP según las necesidades reales del proyecto"
echo "    antes de commitear. Una CSP demasiado restrictiva puede romper funcionalidad."
echo ""

mapfile -t HTML_FILES < <(find . -not -path "./.git/*" -name "*.html" -type f)

for file in "${HTML_FILES[@]}"; do
  if grep -qi 'content-security-policy' "$file"; then
    echo "  ⏭️  $file — Ya tiene CSP, omitiendo"
    continue
  fi

  echo "  📄 $file — Sin CSP detectada"
  echo "     Se insertará después de <head>:"
  echo "     $CSP_META"
  read -rp "     ¿Confirmar inserción? (s/N): " confirm

  if [[ "${confirm,,}" == "s" ]]; then
    sed -i "s|<head>|<head>\n$CSP_META|I" "$file"
    echo "     ✅ Insertado"
  else
    echo "     ⏭️  Omitido"
  fi
  echo ""
done

echo "=== Completado. Verificar cambios con: git diff ==="
```

---

## Uso en CI/CD

Para integrar los scripts de verificación en un workflow de GitHub Actions:

```yaml
# .github/workflows/security-check.yml
name: Security Audit

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  verify:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Higiene base del repositorio
        run: bash scripts/verify_hygiene.sh

      - name: Detección de secretos
        run: bash scripts/verify_secrets.sh

      - name: Hardening frontend
        run: bash scripts/verify_headers.sh

      - name: Dependencias (si aplica)
        run: bash scripts/verify_deps.sh
```

> Los scripts de **corrección** (`fix_*.sh`) nunca deben ejecutarse en CI —
> son exclusivamente para uso local del mantenedor.
