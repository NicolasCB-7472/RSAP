# Rúbrica — Hardening de Superficie (0–100)

## ¿Qué mide este eje?
La robustez de la capa de entrega del proyecto frente a ataques externos. Cubre cabeceras de seguridad HTTP, políticas de contenido, configuración TLS, y reducción de superficie de ataque en el punto de exposición (web, API, servicio).

> **Nota de alcance**: En repos sin infraestructura versionada (solo HTML/JS estático), este eje evalúa lo que *puede* controlarse desde el código: meta-tags CSP, integridad de recursos externos (SRI), y ausencia de patrones que amplifiquen vulnerabilidades en el servidor.

---

## Criterios de evaluación

### ✅ Positivos (suman puntos)
| Criterio | Peso |
|---|---|
| Content Security Policy (CSP) definida en cabeceras o meta-tag | +25 |
| Subresource Integrity (SRI) en recursos externos (CDN, fuentes) | +15 |
| Cabeceras de seguridad presentes en config de servidor/CDN versionada: `X-Frame-Options`, `X-Content-Type-Options`, `Referrer-Policy`, `Permissions-Policy` | +20 |
| TLS forzado (HTTPS, HSTS) si aplica | +15 |
| Fuentes y recursos externos self-hosted o eliminados | +10 |
| Ausencia de dependencias externas innecesarias en runtime | +15 |

### ❌ Negativos (restan puntos)
| Criterio | Penalización |
|---|---|
| Sin CSP en frontend web | -20 |
| Dependencias de terceros sin SRI en recursos críticos | -15 |
| Configuración de servidor/CDN no versionada (no auditble desde el repo) | -10 |
| Uso de `http://` en lugar de `https://` en llamadas externas | -20 |
| `X-Frame-Options` ausente (riesgo de clickjacking) | -10 |

---

## Escala de referencia

| Rango | Interpretación |
|---|---|
| 85–100 | Hardening activo. Superficie de ataque minimizada. |
| 65–84 | Aceptable. Faltan algunos controles pero sin exposición crítica. |
| 40–64 | Débil. Controles ausentes que un atacante puede explotar. |
| 0–39 | Crítico. Sin hardening observable; superficie amplia. |

---

## Limitaciones del análisis
- Las cabeceras HTTP reales solo pueden verificarse contra el servidor en producción.
- Si el repo no incluye configuración de servidor (nginx, apache, vercel.json, etc.), la puntuación máxima alcanzable es ~55 (solo se evalúa lo controlable desde código fuente).
