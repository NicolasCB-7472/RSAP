# Política de Seguridad — [Nombre del Proyecto]

Este archivo describe la política de seguridad del proyecto, el proceso para
reportar vulnerabilidades, y el protocolo de auditoría bajo el cual fue evaluado.

---

## Índice

1. [Versiones soportadas](#versiones-soportadas)
2. [Reporte de vulnerabilidades](#reporte-de-vulnerabilidades)
3. [Protocolo de auditoría de seguridad](#protocolo-de-auditoría-de-seguridad)
4. [Sello de seguridad](#sello-de-seguridad)
5. [Compromisos del mantenedor](#compromisos-del-mantenedor)

---

## Versiones soportadas

<!-- Indicar qué versiones o ramas reciben parches de seguridad.
     Para proyectos personales activos, generalmente solo `main`. -->

| Versión / Rama | Soportada |
|---|---|
| `main` | ✅ Sí |
| Releases anteriores | ❌ No |

---

## Reporte de vulnerabilidades

**No abrir issues públicos para reportar vulnerabilidades de seguridad.**

Para reportar una vulnerabilidad, usar **GitHub Security Advisories** (recomendado
para proyectos personales y open source):

1. Ir a la pestaña **Security** del repositorio → **"Report a vulnerability"**
2. El reporte es completamente privado — invisible al público hasta que el
   mantenedor decida publicarlo tras la corrección.
3. Permite coordinación estructurada: severidad, versiones afectadas, CVE opcional.

**¿Por qué Security Advisories en lugar de email?**
- No expone el email del mantenedor públicamente.
- El reporte queda trazable dentro del propio repositorio.
- GitHub puede gestionar la asignación de un CVE oficial si el proyecto lo amerita.
- Flujo estructurado con campos de severidad, versiones afectadas y timeline.

**¿Cuándo agregar un email de contacto?**
Solo cuando el proyecto está pensado para adopción por organizaciones o equipos
corporativos, que pueden tener procesos internos de seguridad que requieren
un canal de email formal. En ese caso, agregar:

```
Para reportes corporativos o si Security Advisories no está disponible:
[email dedicado — no usar email personal]
```
- Descripción del hallazgo y vector de ataque
- Pasos para reproducir (si aplica)
- Severidad estimada (Crítica / Alta / Media / Baja)
- Archivos y líneas de código involucrados

**Tiempo de respuesta esperado:** [X días hábiles]
**Política de divulgación:** [X días] tras la corrección, coordinar publicación con el reportador.

---

## Protocolo de auditoría de seguridad

Este repositorio fue auditado bajo el protocolo **security-audit-github**,
un estándar de evaluación estructurada para repositorios GitHub desarrollado
con el objetivo de hacer la seguridad de proyectos personales y open source
verificable, repetible y transparente.

### ¿Qué evalúa el protocolo?

El protocolo analiza 8 ejes de seguridad, cada uno con criterios y rúbricas
documentadas, puntuados de 0 a 100:

| Eje | Descripción breve |
|---|---|
| Gestión de secretos | Ausencia de credenciales expuestas y controles preventivos |
| Hardening de superficie | Cabeceras HTTP, CSP, SRI, reducción de superficie de ataque |
| Sanitización / validación | Tratamiento seguro de inputs y datos externos |
| Buenas prácticas de código | Patrones seguros, manejo de errores, dependencias |
| Mantenibilidad | Estructura auditable, tests, observabilidad |
| Privacidad / datos | Minimización de datos y control de terceros |
| Configuración del repositorio | Higiene operativa: `.gitignore`, CI, branch protection |
| Preparación para producción | Separación de entornos, despliegue seguro documentado |

### ¿Cómo se genera el informe?

1. Se clona el repositorio y se analizan todos los archivos de texto relevantes.
2. Cada hallazgo se clasifica por severidad (Crítica / Alta / Media / Baja / Positivo)
   y se referencia con número de línea de evidencia.
3. Se asigna una puntuación por eje usando rúbricas documentadas públicamente.
4. El informe técnico completo queda en manos del mantenedor.
5. El gráfico radial (sello) se publica en el repositorio como señal auditable.

### ¿Dónde está la rúbrica completa?

El skill y sus rúbricas son de código abierto:
`[link al repositorio del skill / protocolo]`

---

## Sello de seguridad

<!-- Insertar imagen del gráfico radial más reciente -->

![Sello de Seguridad]([ruta/al/sello.png])

**Fecha de auditoría:** [fecha]
**Herramienta utilizada:** security-audit-github skill v[versión]
**Puntaje general:** [X]/100

*El sello refleja el estado del repositorio en la fecha indicada.
Las mejoras posteriores a la auditoría pueden no estar reflejadas hasta
la próxima revisión.*

---

## Compromisos del mantenedor

- Responder reportes de seguridad dentro del tiempo declarado arriba.
- No publicar detalles de vulnerabilidades antes de tener una corrección disponible.
- Actualizar el sello de seguridad tras cambios significativos en el código.
- Mantener las dependencias actualizadas con prioridad en aquellas con CVEs conocidos.
- Documentar vulnerabilidades conocidas y no resueltas en el README con su severidad.
