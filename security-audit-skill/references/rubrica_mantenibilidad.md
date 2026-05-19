# Rúbrica — Mantenibilidad (0–100)

## ¿Qué mide este eje?
La capacidad del repositorio de ser auditado, actualizado y corregido de forma sostenible a lo largo del tiempo. La mantenibilidad pobre es un riesgo de seguridad indirecto: el código que nadie entiende es el código que nadie parchea.

---

## Criterios de evaluación

### ✅ Positivos (suman puntos)
| Criterio | Peso |
|---|---|
| Código estructurado en módulos/archivos con responsabilidades claras | +15 |
| Presencia de tests (unitarios, integración, e2e) | +20 |
| Dependencias actualizadas o con política de actualización activa (Dependabot, Renovate) | +15 |
| CHANGELOG o commits semánticos que documentan cambios de seguridad | +10 |
| Observabilidad: logging adecuado sin silenciar errores críticos | +15 |
| Linters o formatters configurados (garantizan consistencia legible) | +10 |
| Archivos individuales de tamaño razonable (<500 líneas como referencia) | +15 |

### ❌ Negativos (restan puntos)
| Criterio | Penalización |
|---|---|
| Archivo único monolítico >1000 líneas sin separación de responsabilidades | -20 |
| Sin tests de ningún tipo | -15 |
| Dependencias desactualizadas con CVEs conocidos | -25 |
| Catches silenciosos `catch(() => {})` en flujos críticos | -10 |
| Sin documentación de cambios (ni CHANGELOG ni commits descriptivos) | -10 |
| Código sin comentarios en lógica compleja o de seguridad | -10 |

---

## Escala de referencia

| Rango | Interpretación |
|---|---|
| 85–100 | Código sostenible. Fácil de auditar y actualizar. |
| 65–84 | Mantenible con deuda técnica moderada. |
| 45–64 | Deuda técnica alta; actualizaciones de seguridad son costosas. |
| 0–44 | Código difícil de auditar; riesgo de vulnerabilidades no detectadas. |

---

## Limitaciones del análisis
- Para proyectos personales/hobbistas, la ausencia de tests no necesariamente implica riesgo crítico si el scope es limitado.
- La calidad de los tests no es evaluable sin ejecutarlos.
