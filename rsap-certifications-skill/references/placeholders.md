# Placeholders estándar — RSAP Certifications

Valores por defecto para campos no disponibles al momento de generar
el `CERTIFICATIONS.md`. Reemplazar con datos reales antes de commitear.

---

## Campos de identificación

| Campo | Placeholder |
|---|---|
| Nombre del proyecto | `[Nombre del Proyecto]` |
| Owner/repo | `[owner/repo]` |
| URL del repositorio | `https://github.com/[owner/repo]` |
| Fecha | `[DD/MM/AAAA]` — usar fecha actual de generación |
| Versión del protocolo | `RSAP v1.0` (fijo hasta nueva versión) |

---

## Rutas de imágenes

| Elemento | Placeholder de ruta |
|---|---|
| SelloSeguridad | `./[carpeta]/SelloSeguridad.png` |
| SelloCalidad | `./[carpeta]/SelloCalidad.png` |

> Convención recomendada: guardar sellos en `[NombreProyecto]/Fruits/` o `assets/sellos/`
> para consistencia entre repos bajo RSAP.

---

## Puntajes

| Campo | Placeholder |
|---|---|
| Puntaje general | `[pendiente de auditoría]` |
| Puntaje por eje | `[—]` |
| Fecha de auditoría | `[pendiente]` |

Cuando el puntaje no está disponible, agregar la siguiente nota
debajo de la tabla de sellos:

```
> ⏳ Auditoría de seguridad pendiente bajo protocolo RSAP v1.0.
> El SelloSeguridad se publicará una vez completada.
```

---

## Estados por defecto para repo nuevo

Para un repositorio recién iniciado sin auditoría previa:

| Elemento | Estado inicial |
|---|---|
| README.md | ⚠️ (existe básico, falta sección seguridad) |
| SECURITY.md | ❌ |
| SCRIPTS.md | ❌ |
| Sello de Seguridad | ❌ |
| Sello de Calidad | ❌ |
| GitHub Actions / CI | ❌ |
| GitHub Advisory | ❌ |

Orden de prioridad para completar:
1. SECURITY.md + GitHub Advisory (responsible disclosure primero)
2. README.md con sección de seguridad
3. Sello de Seguridad (requiere completar auditoría RSAP)
4. SCRIPTS.md + GitHub Actions
5. Sello de Calidad
