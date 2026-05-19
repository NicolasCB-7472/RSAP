# Rúbrica — Gestión de Secretos (0–100)

## ¿Qué mide este eje?
La capacidad del repositorio de evitar la exposición de información sensible: credenciales, tokens, claves API, contraseñas, certificados privados u otros datos que otorguen acceso a sistemas externos.

---

## Criterios de evaluación

### ✅ Positivos (suman puntos)
| Criterio | Peso |
|---|---|
| No se detectan secretos hardcodeados en ningún archivo de texto | +30 |
| Existe `.gitignore` con reglas para `.env*`, `*.pem`, `*.key`, `*.p12`, etc. | +20 |
| Se usan variables de entorno o gestores externos (Vault, AWS SM, GitHub Secrets) | +20 |
| El historial de commits no contiene secretos (aunque luego hayan sido removidos) | +15 |
| Presencia de herramientas de detección: gitleaks, detect-secrets, git-secrets en CI | +15 |

### ❌ Negativos (restan puntos)
| Criterio | Penalización |
|---|---|
| Secreto hardcodeado encontrado en código fuente activo | -40 |
| Secreto detectado en historial de commits (aunque removido) | -25 |
| Archivo `.env` commiteado con valores reales | -30 |
| `.gitignore` ausente completamente | -15 |
| Tokens o credenciales en comentarios de código | -20 |

---

## Escala de referencia

| Rango | Interpretación |
|---|---|
| 90–100 | Excelente. Controles activos y sin exposición detectada. |
| 70–89 | Bueno. Sin secretos expuestos pero faltan guardrails preventivos. |
| 50–69 | Riesgo latente. Ausencia de controles aunque no haya exposición actual. |
| 30–49 | Riesgo alto. Debilidades estructurales que facilitan futuros leaks. |
| 0–29 | Crítico. Secretos expuestos detectados en código o historial. |

---

## Limitaciones del análisis
- El análisis de historial de commits es limitado sin acceso completo a `git log`.
- Los assets binarios (imágenes, audio) no se inspeccionan a nivel forense.
- Secretos en sistemas externos (CI, cloud) no son visibles desde el repo.
