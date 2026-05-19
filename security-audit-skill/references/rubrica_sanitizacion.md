# Rúbrica — Sanitización / Validación (0–100)

## ¿Qué mide este eje?
La solidez con la que el código trata los datos que ingresan al sistema, ya sea desde el usuario, APIs externas, almacenamiento local u otras fuentes no confiables. Un fallo aquí es la raíz de la mayoría de vulnerabilidades de aplicación (XSS, SQLi, path traversal, etc.).

---

## Criterios de evaluación

### ✅ Positivos (suman puntos)
| Criterio | Peso |
|---|---|
| Uso de `textContent` en lugar de `innerHTML` para renderizar datos de usuario | +20 |
| Inputs sanitizados antes de insertarse en DOM, SQL, o sistema de archivos | +20 |
| Validación de longitud, tipo y formato en entradas de usuario | +15 |
| Parseo de datos externos (JSON, localStorage) protegido con try/catch | +15 |
| Uso de consultas parametrizadas / ORM en accesos a base de datos | +15 |
| Whitelist de valores permitidos (clamp, enum, regex) en parámetros críticos | +15 |

### ❌ Negativos (restan puntos)
| Criterio | Penalización |
|---|---|
| Uso de `innerHTML` con datos de usuario sin sanitizar | -35 |
| Uso de `eval()` o `Function()` con input externo | -30 |
| Consultas SQL construidas por concatenación de strings | -30 |
| Ausencia de validación en parámetros que afectan lógica de negocio | -20 |
| Datos de localStorage/sessionStorage usados sin validación de tipo/formato | -15 |
| Path traversal posible por falta de sanitización en rutas de archivo | -25 |

---

## Escala de referencia

| Rango | Interpretación |
|---|---|
| 88–100 | Excelente. Todas las entradas controladas y sanitizadas. |
| 70–87 | Bueno. Validación presente con casos edge menores sin cubrir. |
| 50–69 | Moderado. Algunas entradas no validadas; riesgo real de explotación. |
| 0–49 | Crítico. Vectores de ataque directos detectados (XSS, SQLi, etc.). |

---

## Limitaciones del análisis
- En frameworks con sanitización automática (React, Angular), el riesgo base es menor; ajustar la puntuación en consecuencia.
- El análisis es estático: no detecta vulnerabilidades que emergen solo en runtime con datos específicos.
