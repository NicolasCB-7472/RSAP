# Elementos RSAP — Criterios de evaluación

Criterios para determinar el estado (✅ / ⚠️ / ❌) de cada elemento
certificable bajo el protocolo RSAP v1.0.

---

## 1. README.md

**✅ Completo** si contiene:
- Descripción general del proyecto y stack tecnológico
- Sección de **Consideraciones de seguridad** con al menos: superficie de ataque,
  dependencias externas, y datos del usuario
- Configuración segura recomendada
- Referencia al SECURITY.md y al sello de seguridad

**⚠️ Incompleto** si:
- Existe pero le falta la sección de consideraciones de seguridad
- No referencia al sello ni al SECURITY.md
- Está orientado solo a funcionalidad sin contexto de seguridad

**❌ Ausente** si no existe ningún archivo README* en la raíz del repo.

---

## 2. SECURITY.md

**✅ Completo** si contiene:
- Canal de reporte de vulnerabilidades (GitHub Advisory y/o email)
- Tiempo de respuesta declarado
- Descripción del protocolo de auditoría RSAP
- Compromisos del mantenedor

**⚠️ Incompleto** si:
- Existe pero no menciona GitHub Advisory ni canal de contacto
- No documenta el protocolo de auditoría
- Falta la tabla de versiones soportadas

**❌ Ausente** si no existe `SECURITY.md` en la raíz del repo.

---

## 3. SCRIPTS.md

**✅ Completo** si contiene:
- Al menos un script de verificación funcional (`verify_*.sh`)
- Al menos un script de corrección con confirmación explícita (`fix_*.sh`)
- Instrucciones de uso desde raíz del repo
- Nota sobre qué scripts NO van a CI

**⚠️ Incompleto** si:
- Solo tiene scripts de verificación sin corrección (o viceversa)
- Falta el bloque de integración con CI/CD
- Los scripts no tienen comentarios de seguridad (`verify_secrets.sh`)

**❌ Ausente** si no existe `SCRIPTS.md` en el repo.

**— No aplica** si el proyecto es solo documentación o assets sin lógica ejecutable.

---

## 4. Sello de Seguridad

**✅ Presente** si:
- Existe una imagen del gráfico radial RSAP en el repo
- La imagen está referenciada desde README o CERTIFICATIONS
- Tiene fecha de auditoría documentada

**⚠️ Desactualizado** si:
- La imagen existe pero tiene más de 6 meses sin actualización
- No hay fecha de auditoría documentada

**❌ Ausente** si no hay ninguna imagen de gráfico radial de seguridad en el repo.

---

## 5. Sello de Calidad

**✅ Presente** si:
- Existe una imagen de sello de calidad en el repo
- El criterio de calidad que representa está documentado

**⚠️ Desactualizado** si:
- Existe pero no tiene fecha ni criterio documentado

**❌ Ausente** si no hay imagen de sello de calidad.

**— No aplica** si el proyecto está en fase inicial y aún no se emitió sello de calidad.

---

## 6. GitHub Actions / CI

**✅ Activo** si:
- Existe al menos un workflow en `.github/workflows/`
- El workflow se ejecuta en push o PR a rama principal
- Incluye al menos uno de: verify_hygiene, verify_secrets, verify_headers

**⚠️ Parcial** si:
- Existe un workflow pero no incluye verificaciones de seguridad RSAP
- Solo corre en algunas ramas o eventos

**❌ Ausente** si no existe `.github/workflows/` con ningún archivo `.yml`.

**— No aplica** para repos de solo documentación o assets estáticos sin build.

---

## 7. GitHub Advisory

**✅ Configurado** si:
- El repo tiene habilitados los Private Security Advisories de GitHub
- Está referenciado desde SECURITY.md como canal de reporte

**❌ No configurado** si:
- No hay mención de GitHub Advisory en SECURITY.md
- El repo no tiene la pestaña Security habilitada

> **Nota:** Para verificar si Private Security Advisories está habilitado:
> Settings → Code security → Private vulnerability reporting → Enabled
