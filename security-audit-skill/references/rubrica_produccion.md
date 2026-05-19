# Rúbrica — Preparación para Producción (0–100)

## ¿Qué mide este eje?
El grado en que el repositorio está listo para operar en un entorno real con usuarios reales, bajo condiciones adversas. No evalúa si *funciona*, sino si está *preparado para fallar de forma segura* y ser operado responsablemente.

---

## Criterios de evaluación

### ✅ Positivos (suman puntos)
| Criterio | Peso |
|---|---|
| Separación de entornos: variables de entorno diferenciadas para dev/staging/prod | +20 |
| Manejo de errores graceful: el sistema falla sin exponer internals | +15 |
| Proceso de build/deploy documentado o automatizado | +15 |
| Dependencias de producción separadas de las de desarrollo | +10 |
| Rate limiting o protección contra abuso implementados (si aplica) | +10 |
| Monitoreo o logging de eventos de seguridad contemplado | +10 |
| Documentación de consideraciones de seguridad para el despliegue | +20 |

### ❌ Negativos (restan puntos)
| Criterio | Penalización |
|---|---|
| Variables de entorno hardcodeadas con valores de producción | -30 |
| Modo debug o verbose activo en configuración por defecto | -20 |
| Sin instrucciones de despliegue seguro (quién lo despliega comete errores) | -15 |
| Dependencias de desarrollo incluidas en bundle de producción | -10 |
| Sin contemplar expiración de sesiones, tokens o caché | -10 |
| Sin manejo de errores para casos de fallo de servicios externos | -15 |

---

## Escala de referencia

| Rango | Interpretación |
|---|---|
| 85–100 | Listo para producción con controles operativos de seguridad. |
| 60–84 | Funcional pero requiere trabajo antes de exponer a usuarios reales. |
| 35–59 | Solo apto para desarrollo local; requiere hardening significativo. |
| 0–34 | No apto para producción en estado actual. |

---

## Limitaciones del análisis
- Para proyectos personales/portfolio que no pretenden llegar a producción real, este eje puede evaluarse con criterio ajustado al contexto declarado.
- La separación de entornos solo es verificable si el repo incluye configuración de infraestructura versionada.
