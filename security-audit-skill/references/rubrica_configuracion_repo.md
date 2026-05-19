# Rúbrica — Configuración del Repositorio (0–100)

## ¿Qué mide este eje?
La higiene operativa del repositorio como unidad: controles de acceso, protección de ramas, automatización de seguridad, y presencia de archivos base que reducen el riesgo de errores humanos accidentales.

---

## Criterios de evaluación

### ✅ Positivos (suman puntos)
| Criterio | Peso |
|---|---|
| `.gitignore` presente con reglas para secretos y artefactos | +20 |
| Branch protection en `main`/`master` (requiere review antes de merge) | +15 |
| Flujo de CI/CD configurado (`.github/workflows` u equivalente) | +15 |
| `SECURITY.md` con política de responsible disclosure | +15 |
| `README.md` presente con instrucciones básicas de uso seguro | +10 |
| Firma de commits (GPG/SSH) configurada | +10 |
| Permisos de acceso al repo apropiados para el contexto (público/privado) | +15 |

### ❌ Negativos (restan puntos)
| Criterio | Penalización |
|---|---|
| Sin `.gitignore` (cualquier archivo puede commitearse accidentalmente) | -25 |
| Sin branch protection en rama principal | -15 |
| Sin CI/CD ni automatización de calidad | -10 |
| Repo público con información sensible en descripción o topics | -15 |
| Dependencias de CI con versiones flotantes (riesgo supply chain) | -10 |
| Sin `SECURITY.md` ni canal de reporte de vulnerabilidades | -10 |

---

## Escala de referencia

| Rango | Interpretación |
|---|---|
| 85–100 | Repositorio bien gobernado. Controles operativos activos. |
| 60–84 | Configuración básica presente; faltan controles avanzados. |
| 35–59 | Configuración mínima o ausente; riesgo operativo significativo. |
| 0–34 | Sin controles de repo; un error humano puede comprometer el proyecto. |

---

## Limitaciones del análisis
- Las branch protection rules y permisos de acceso solo son auditables si el repositorio es público o el analista tiene acceso de admin.
- Para repositorios personales/portfolio, la ausencia de CI puede ser intencional y no necesariamente un riesgo crítico.
