---
name: security-audit-github
description: >
  Auditoría de seguridad profunda para repositorios GitHub. Genera un informe técnico
  estructurado con hallazgos por severidad, evidencia con número de línea, y tabla de
  métricas con puntuaciones (0–100) por categoría, apto para producir un gráfico radial
  de seguridad. Usar siempre que el usuario pida auditar, revisar, evaluar o puntuar
  un repositorio en términos de seguridad, buenas prácticas, secretos, vulnerabilidades
  o preparación para producción. También aplica si el usuario menciona "sello de seguridad",
  "radar de seguridad", "score del repo" o quiere generar un informe de ciberseguridad.
---

# Security Audit Skill — Repositorios GitHub

Auditoría de seguridad estructurada que produce un informe técnico para mantenedores
y una tabla de métricas para visualización radial pública.

---

## Flujo de trabajo

### Paso 1 — Determinar el modo de input

**Modo A — Archivos locales** (disponibles en contexto o subidos):
- Proceder directamente al análisis con los archivos disponibles.
- Documentar qué archivos se analizaron y cuáles quedaron fuera del alcance.

**Modo B — URL de repositorio GitHub**:
- Usar la GitHub API para obtener el árbol de archivos:
  `GET https://api.github.com/repos/{owner}/{repo}/git/trees/HEAD?recursive=1`
- Priorizar archivos de texto relevantes para seguridad (ver §Prioridad de archivos).
- Documentar limitaciones de acceso (repo privado, rate limit, etc.).

---

### Paso 2 — Inventario del repositorio

Listar todos los archivos detectados, agrupados por tipo:
- Código fuente (`.js`, `.ts`, `.py`, `.go`, `.java`, etc.)
- Configuración (`.env*`, `.yml`, `.json`, `.toml`, `.ini`, `.cfg`)
- Infraestructura (`.github/workflows`, `Dockerfile`, `docker-compose*`, `terraform/`)
- Documentación (`README*`, `SECURITY.md`, `CHANGELOG*`, `LICENSE`)
- Assets binarios (`.png`, `.mp3`, `.pdf`, etc.) — marcar como "no auditados a nivel forense"

**Archivos de higiene base a verificar explícitamente**:
- [ ] `.gitignore`
- [ ] `README.md`
- [ ] `SECURITY.md`
- [ ] `.github/workflows/`
- [ ] `package.json` / `requirements.txt` / equivalente de dependencias

---

### Paso 3 — Análisis archivo por archivo

Para cada archivo relevante de código y configuración:

```
[nombre del archivo]
├── Hallazgo: descripción del hallazgo
├── Severidad: Crítica / Alta / Media / Baja / Positivo
├── Categoría: [eje de rúbrica al que pertenece]
└── Evidencia: archivo:línea o rango (ej: script.js:249-254)
```

**Prioridad de análisis** (orden descendente):
1. Archivos de configuración y variables de entorno
2. Código que maneja autenticación, sesiones, o datos de usuario
3. Código que realiza llamadas a red o accede a recursos externos
4. Código de lógica principal de aplicación
5. Assets y archivos estáticos

---

### Paso 4 — Puntuación por eje

Leer el archivo de rúbrica correspondiente antes de puntuar cada eje.
**No puntuar de memoria — siempre consultar la rúbrica.**

| Eje | Archivo de rúbrica |
|---|---|
| Gestión de secretos | `references/rubrica_secretos.md` |
| Hardening de superficie | `references/rubrica_hardening.md` |
| Sanitización / validación | `references/rubrica_sanitizacion.md` |
| Buenas prácticas de código | `references/rubrica_buenas_practicas.md` |
| Mantenibilidad | `references/rubrica_mantenibilidad.md` |
| Privacidad / datos | `references/rubrica_privacidad.md` |
| Configuración del repositorio | `references/rubrica_configuracion_repo.md` |
| Preparación para producción | `references/rubrica_produccion.md` |

**Reglas de puntuación**:
- Empezar desde 60 (base neutra) y aplicar positivos/negativos de la rúbrica.
- Nunca salir del rango 0–100.
- Si un eje no es evaluable por falta de archivos relevantes, marcarlo como `N/A` con justificación.
- Registrar qué criterios de la rúbrica se aplicaron para cada puntuación.

---

### Paso 5 — Generar el informe

Seguir esta estructura exacta:

```
# Informe de Auditoría de Seguridad — [owner/repo]
**Fecha:** [fecha]
**Alcance:** [archivos analizados / modo de análisis]

---

## Resumen Ejecutivo
[3–5 líneas: hallazgo más crítico, fortaleza principal, recomendación urgente]

---

## 1. Inventario del Repositorio
[tabla o lista de archivos por categoría]

---

## 2. Auditoría Archivo por Archivo
[hallazgos estructurados por archivo, con severidad y evidencia]

---

## 3. Riesgos Consolidados y Priorizados
[lista ordenada por severidad, con descripción y categoría]

---

## 4. Tabla de Métricas
| Área | Puntuación (0–100) | Justificación breve |
|---|---|---|
| Gestión de secretos | X | ... |
| Hardening de superficie | X | ... |
| Sanitización / validación | X | ... |
| Buenas prácticas de código | X | ... |
| Mantenibilidad | X | ... |
| Privacidad / datos | X | ... |
| Configuración del repositorio | X | ... |
| Preparación para producción | X | ... |
| **Puntaje general** | **X** | Media ponderada |

---

## 5. Recomendaciones Accionables
[lista ordenada por impacto, con pasos concretos]

---

## Limitaciones del Análisis
[qué no se pudo verificar y por qué]
```

---

## Cálculo del puntaje general

```
Puntaje general = media ponderada de los 8 ejes

Pesos sugeridos (ajustables por contexto):
- Gestión de secretos:          15%
- Hardening de superficie:      12%
- Sanitización / validación:    15%
- Buenas prácticas de código:   15%
- Mantenibilidad:               10%
- Privacidad / datos:           12%
- Configuración del repositorio: 11%
- Preparación para producción:  10%
```

---

## Escala de severidad de hallazgos

| Severidad | Descripción |
|---|---|
| **Crítica** | Explotable directamente; requiere acción inmediata. |
| **Alta** | Riesgo significativo; parchear antes del próximo deploy. |
| **Media** | Riesgo real pero con mitigantes presentes; planificar solución. |
| **Baja** | Mejora de calidad o riesgo teórico bajo condiciones específicas. |
| **Positivo** | Buena práctica detectada; documentar como fortaleza. |

---

## Consideraciones de contexto

Ajustar el tono y los criterios según el tipo de proyecto declarado:

- **Personal/portfolio**: No penalizar ausencia de CI o tests con igual peso que un proyecto empresarial. Enfocarse en lo que sí puede comprometer seguridad real.
- **Open source colaborativo**: Mayor peso en branch protection, SECURITY.md, y supply chain.
- **Empresarial/profesional**: Todos los ejes con peso completo; sin concesiones por contexto.

El contexto no excusa hallazgos críticos — solo ajusta la severidad de los moderados.

---

## Output final

1. **Informe técnico** (`.md`) — para mantenedores del código
2. **Tabla de métricas** — extraíble para gráfico radial público
3. **Oferta al usuario**: generar el gráfico radial a partir de las puntuaciones (usando el widget interactivo o una imagen SVG con el branding del proyecto si se proporciona)

---

## Templates de archivos estándar del protocolo

Cuando el usuario solicite generar o revisar los archivos base del protocolo,
leer el template correspondiente antes de producir el output:

| Archivo | Template | Cuándo usar |
|---|---|---|
| `README.md` | `references/template_README.md` | Al generar README orientado a usuario técnico/auditor |
| `SECURITY.md` | `references/template_SECURITY.md` | Al generar política de seguridad con protocolo visible |
| `SCRIPTS.md` | `references/template_SCRIPTS.md` | Al generar scripts bash de verificación y corrección |

Los templates incluyen cabezales fijos y comentarios guía para el mantenedor.
Adaptar el contenido al proyecto específico manteniendo la estructura de índice.
