---
name: rsap-certifications
description: >
  Genera el archivo CERTIFICATIONS.md de un repositorio bajo el protocolo RSAP
  (Repository Security Audit Protocol). Este archivo consolida en una sola página
  todas las certificaciones de calidad y seguridad del proyecto: README, SelloCalidad,
  SelloSeguridad, SECURITY.md, SCRIPTS.md, GitHub Actions/CI, y GitHub Advisory.
  Usar siempre que el usuario pida generar, actualizar o revisar el CERTIFICATIONS.md,
  mencione "sello de calidad", "sello de seguridad", "certificaciones del repo",
  "índice de confianza", o quiera documentar el estado de cumplimiento RSAP de un repositorio.
---

# RSAP Certifications Skill

Genera el archivo `CERTIFICATIONS.md` — índice de confianza visible del repositorio
bajo el protocolo **RSAP v1.0** (Repository Security Audit Protocol).

El archivo resultante es público, auditable por terceros, y funciona como
punto de entrada único para evaluar la madurez de seguridad y calidad del proyecto.

---

## Flujo de trabajo

### Paso 1 — Recopilar información del proyecto

Antes de generar el archivo, obtener o inferir:

| Dato | Fuente |
|---|---|
| Nombre del proyecto | Conversación / nombre del repo |
| Descripción breve | README o conversación |
| URL del repositorio | Conversación o contexto |
| Versión del protocolo | Siempre `RSAP v1.0` salvo indicación contraria |
| Fecha de certificación | Fecha actual |
| Estado de cada elemento | Ver §Checklist de elementos (abajo) |
| Puntaje de seguridad | Tabla de métricas del informe de auditoría (si disponible) |
| Ruta del SelloSeguridad | Inferir del repo o usar placeholder |
| Ruta del SelloCalidad | Inferir del repo o usar placeholder |

Si algún dato no está disponible, usar el placeholder correspondiente
definido en `references/placeholders.md`.

---

### Paso 2 — Evaluar el estado de cada elemento

Para cada elemento certificable, determinar su estado:

| Estado | Símbolo | Significado |
|---|---|---|
| Presente y completo | ✅ | El archivo/elemento existe y cumple estructura mínima RSAP |
| Presente pero incompleto | ⚠️ | Existe pero le faltan secciones o está desactualizado |
| Ausente | ❌ | No existe en el repositorio |
| No aplica | `—` | El elemento no corresponde al tipo/scope del proyecto |

**Elementos a evaluar** (leer `references/elementos_rsap.md` para criterios detallados):

1. `README.md` — Documentación orientada a usuario técnico/auditor
2. `SECURITY.md` — Política de seguridad y responsible disclosure
3. `SCRIPTS.md` — Scripts de verificación y corrección bash
4. `SelloSeguridad` — Gráfico radial del protocolo RSAP (imagen)
5. `SelloCalidad` — Sello visual de calidad del proyecto (imagen)
6. `GitHub Actions / CI` — Workflow de verificación automática
7. `GitHub Advisory` — Canal de responsible disclosure configurado

---

### Paso 3 — Generar CERTIFICATIONS.md

Leer `references/template_CERTIFICATIONS.md` y completar con los datos recopilados.

**Reglas de generación:**
- Mantener la estructura de secciones exactamente como en el template.
- Completar todos los placeholders `[entre corchetes]`.
- Insertar el estado (✅ / ⚠️ / ❌ / —) en cada fila de la tabla.
- Si hay puntaje de auditoría disponible, incluirlo en la sección de SelloSeguridad.
- Si no hay imagen real del sello, usar la ruta placeholder y agregar nota.
- El tono es técnico pero legible para un tercero que no conoce el proyecto.

---

### Paso 4 — Output

Entregar:
1. El archivo `CERTIFICATIONS.md` completo, listo para commitear en la raíz del repo.
2. Un resumen breve de qué elementos están completos, cuáles incompletos, y cuáles ausentes.
3. Si hay elementos ❌ o ⚠️, sugerir el orden de prioridad para completarlos
   (siempre: SECURITY.md > README.md > SelloSeguridad > Actions > resto).

---

## Referencias

- `references/template_CERTIFICATIONS.md` — Template completo del archivo a generar
- `references/elementos_rsap.md` — Criterios de evaluación por elemento
- `references/placeholders.md` — Valores placeholder estándar por campo
