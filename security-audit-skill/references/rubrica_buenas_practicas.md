# Rúbrica — Buenas Prácticas de Código (0–100)

## ¿Qué mide este eje?
La calidad del código desde una perspectiva de seguridad aplicada: patrones seguros de programación, manejo correcto de errores, principio de mínimo privilegio, y ausencia de anti-patrones conocidos que faciliten vulnerabilidades.

---

## Criterios de evaluación

### ✅ Positivos (suman puntos)
| Criterio | Peso |
|---|---|
| Manejo de errores explícito (sin swallow de excepciones silenciosas en flujos críticos) | +15 |
| Ausencia de funciones peligrosas: `eval()`, `exec()`, `system()`, `dangerouslySetInnerHTML` | +20 |
| Código modular con responsabilidades bien separadas (facilita auditoría) | +15 |
| Dependencias con versiones fijas (no rangos abiertos como `^`, `*`, `latest`) | +15 |
| Comunicaciones externas sobre HTTPS/TLS | +10 |
| Uso de librerías de seguridad establecidas en lugar de implementaciones caseras (crypto, auth) | +15 |
| Ausencia de stack traces o información sensible expuesta en errores de usuario | +10 |

### ❌ Negativos (restan puntos)
| Criterio | Penalización |
|---|---|
| `eval()` o equivalentes con input no confiable | -35 |
| Criptografía implementada desde cero (no usar librerías estándar) | -25 |
| Stack traces o mensajes de error detallados expuestos al usuario final | -20 |
| Dependencias con rangos abiertos que permiten actualizaciones automáticas no controladas | -10 |
| Lógica de autenticación/autorización inconsistente o con bypasses evidentes | -30 |
| Catches vacíos `catch(e) {}` en flujos de seguridad | -10 |

---

## Escala de referencia

| Rango | Interpretación |
|---|---|
| 88–100 | Código seguro y auditble. Patrones correctos consistentemente aplicados. |
| 70–87 | Buenas prácticas presentes con deuda técnica menor de seguridad. |
| 50–69 | Anti-patrones presentes; requiere refactoring de seguridad. |
| 0–49 | Prácticas peligrosas activas; riesgo de explotación directa. |

---

## Limitaciones del análisis
- El análisis es estático; no reemplaza un pentest activo.
- Para repos sin código ejecutable (solo assets, documentación), este eje puede quedar N/A o evaluarse parcialmente.
