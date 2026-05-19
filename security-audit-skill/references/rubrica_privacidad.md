# Rúbrica — Privacidad / Datos (0–100)

## ¿Qué mide este eje?
El tratamiento responsable de datos personales, de uso, y de comportamiento del usuario. Evalúa tanto la minimización de datos recolectados como las garantías de que esos datos no se exponen, filtran o comparten sin consentimiento.

---

## Criterios de evaluación

### ✅ Positivos (suman puntos)
| Criterio | Peso |
|---|---|
| Solo se recolectan datos estrictamente necesarios para la funcionalidad (minimización) | +20 |
| Datos de usuario almacenados localmente (no enviados a servidores de terceros) | +15 |
| Sin telemetría, analytics ni tracking sin consentimiento explícito | +20 |
| Ausencia de dependencias de terceros que recolecten datos en background (fonts, CDNs de tracking) | +15 |
| Datos sensibles no logueados ni expuestos en consola/error messages | +15 |
| Política de privacidad presente si el proyecto recolecta datos personales | +15 |

### ❌ Negativos (restan puntos)
| Criterio | Penalización |
|---|---|
| Datos de usuario enviados a terceros sin consentimiento explícito | -30 |
| Uso de Google Fonts u otros servicios externos que exponen IP del usuario | -10 |
| Analytics o tracking sin mecanismo de opt-out | -20 |
| Datos personales logueados en consola o almacenados en texto plano | -25 |
| Retención de datos más allá de lo necesario para la funcionalidad | -15 |
| Ausencia de política de privacidad en proyecto con recolección real de datos | -20 |

---

## Escala de referencia

| Rango | Interpretación |
|---|---|
| 88–100 | Privacidad by design. Minimización activa de datos y terceros. |
| 68–87 | Buena práctica general con terceros de bajo riesgo presentes. |
| 45–67 | Riesgos de privacidad identificables; requiere atención. |
| 0–44 | Exposición de datos de usuarios a terceros sin control. |

---

## Limitaciones del análisis
- Los servicios de terceros (CDN, fuentes) se evalúan por su presencia en código; el comportamiento real de recolección depende de sus políticas externas.
- Para proyectos puramente locales sin red, este eje puede puntuar alto naturalmente.
