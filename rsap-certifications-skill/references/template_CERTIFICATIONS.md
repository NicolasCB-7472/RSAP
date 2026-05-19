# Certificaciones — [Nombre del Proyecto]

> Índice de confianza del repositorio bajo el protocolo **RSAP v1.0**
> *(Repository Security Audit Protocol)*

Este archivo consolida el estado de todas las certificaciones de seguridad
y calidad del proyecto. Es auditable públicamente por cualquier tercero.

**Repositorio:** [`[owner/repo]`]([URL del repositorio])
**Protocolo:** RSAP v1.0
**Última actualización:** [Fecha]

---

## Sellos

<table>
<tr>
  <td align="center" width="50%">
    <strong>Sello de Seguridad</strong><br><br>
    <img src="[ruta/al/SelloSeguridad.png]" alt="Sello de Seguridad RSAP" width="300"/><br><br>
    <em>Puntaje general: <strong>[X]/100</strong></em><br>
    <em>Auditado: [Fecha de auditoría]</em>
  </td>
  <td align="center" width="50%">
    <strong>Sello de Calidad</strong><br><br>
    <img src="[ruta/al/SelloCalidad.png]" alt="Sello de Calidad RSAP" width="300"/><br><br>
    <em>[Descripción breve del criterio de calidad]</em><br>
    <em>Emitido: [Fecha]</em>
  </td>
</tr>
</table>

---

## Estado de certificaciones

| # | Elemento | Estado | Descripción | Última revisión |
|---|---|---|---|---|
| 1 | 📄 `README.md` | [✅/⚠️/❌] | [Nota breve sobre el estado] | [Fecha] |
| 2 | 🔐 `SECURITY.md` | [✅/⚠️/❌] | [Nota breve sobre el estado] | [Fecha] |
| 3 | 🛠️ `SCRIPTS.md` | [✅/⚠️/❌] | [Nota breve sobre el estado] | [Fecha] |
| 4 | 🛡️ Sello de Seguridad | [✅/⚠️/❌] | [Nota breve sobre el estado] | [Fecha] |
| 5 | ⭐ Sello de Calidad | [✅/⚠️/❌] | [Nota breve sobre el estado] | [Fecha] |
| 6 | ⚙️ GitHub Actions / CI | [✅/⚠️/❌] | [Nota breve sobre el estado] | [Fecha] |
| 7 | 🔒 GitHub Advisory | [✅/⚠️/❌] | [Nota breve sobre el estado] | [Fecha] |

---

## Detalle por elemento

### 📄 README.md
**Estado:** [✅ Completo / ⚠️ Incompleto / ❌ Ausente]

[Descripción de qué cubre el README: audiencia, secciones presentes,
consideraciones de seguridad documentadas, vínculo al sello.]

> 📎 Ver: [README.md](./README.md)

---

### 🔐 SECURITY.md
**Estado:** [✅ Completo / ⚠️ Incompleto / ❌ Ausente]

[Descripción de la política de seguridad: canal de reporte configurado
(GitHub Advisory / email), tiempo de respuesta declarado, protocolo de
auditoría documentado, compromisos del mantenedor.]

> 📎 Ver: [SECURITY.md](./SECURITY.md)

---

### 🛠️ SCRIPTS.md
**Estado:** [✅ Completo / ⚠️ Incompleto / ❌ Ausente]

[Descripción de los scripts disponibles: cuáles de verificación,
cuáles de corrección, integración con CI si aplica.]

> 📎 Ver: [SCRIPTS.md](./SCRIPTS.md)

---

### 🛡️ Sello de Seguridad
**Estado:** [✅ Presente / ⚠️ Desactualizado / ❌ Ausente]
**Puntaje general:** [X]/100
**Fecha de auditoría:** [Fecha]

Gráfico radial generado bajo el protocolo RSAP v1.0.
Evalúa 8 ejes: Gestión de secretos, Hardening de superficie,
Sanitización/validación, Buenas prácticas, Mantenibilidad,
Privacidad/datos, Configuración del repositorio, Preparación para producción.

| Eje | Puntaje |
|---|---|
| Gestión de secretos | [X]/100 |
| Hardening de superficie | [X]/100 |
| Sanitización / validación | [X]/100 |
| Buenas prácticas de código | [X]/100 |
| Mantenibilidad | [X]/100 |
| Privacidad / datos | [X]/100 |
| Configuración del repositorio | [X]/100 |
| Preparación para producción | [X]/100 |

> 📎 Ver: [`[ruta/al/SelloSeguridad.png]`]([ruta/al/SelloSeguridad.png])

---

### ⭐ Sello de Calidad
**Estado:** [✅ Presente / ⚠️ Desactualizado / ❌ Ausente]
**Emitido:** [Fecha]

[Descripción del criterio de calidad que representa el sello:
funcionalidad, experiencia de usuario, estándares de código, etc.]

> 📎 Ver: [`[ruta/al/SelloCalidad.png]`]([ruta/al/SelloCalidad.png])

---

### ⚙️ GitHub Actions / CI
**Estado:** [✅ Activo / ⚠️ Parcial / ❌ Ausente]

[Descripción de los workflows configurados: qué verifican,
en qué ramas se ejecutan, si incluyen los scripts de seguridad RSAP.]

> 📎 Ver: [`.github/workflows/`](./.github/workflows/)

---

### 🔒 GitHub Advisory
**Estado:** [✅ Configurado / ❌ No configurado]

[Estado del canal de responsible disclosure.
Si está configurado: indicar que los reportes privados están habilitados.
Si no: indicar que está pendiente de configuración.]

> 📎 Ver: [Security Advisories](../../security/advisories)

---

## Sobre el protocolo RSAP

**RSAP** *(Repository Security Audit Protocol)* es un estándar de evaluación
estructurada para repositorios GitHub con el objetivo de hacer la seguridad
de proyectos personales y open source verificable, repetible y transparente.

El protocolo define rúbricas documentadas para 8 ejes de seguridad,
templates estándar para archivos de gobernanza, scripts de verificación
automatizables, y un sistema de sellos públicos como señal de confianza auditable.

**Versión del protocolo:** RSAP v1.0
**Skill utilizado:** `security-audit-github` + `rsap-certifications`
**Licencia del protocolo:** [Apache 2.0](./LICENSE)

---

*Este archivo fue generado bajo el protocolo RSAP v1.0.
Los sellos reflejan el estado del repositorio en la fecha indicada.*
