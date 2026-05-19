# RSAP — Repository Security Audit Protocol

**RSAP (Repository Security Audit Protocol)** es un protocolo orientado a repositorios GitHub que define cómo auditar, documentar y comunicar el estado de seguridad y calidad de un proyecto mediante *skills* especializadas para uso con IA.

Este repositorio reúne los componentes base de **RSAP v1.0** y propone una estructura reproducible para:

- auditar un repositorio desde una perspectiva de seguridad,
- generar un informe técnico con hallazgos verificables,
- puntuar áreas clave mediante una rúbrica consistente,
- producir artefactos públicos de confianza, como `CERTIFICATIONS.md`,
- facilitar una calibración más segura y explícita del desarrollo asistido por IA.

---

## Objetivo

El objetivo de RSAP es ofrecer un marco claro para que repositorios, mantenedores y equipos técnicos puedan:

- **evaluar exposición a riesgos comunes**,
- **estandarizar criterios de revisión**,
- **mejorar trazabilidad de decisiones de seguridad**,
- **hacer visible el nivel de madurez del proyecto**,
- **usar IA de forma más controlada, auditable y prudente**.

RSAP no pretende reemplazar una auditoría profesional completa ni una revisión manual experta.  
Su propósito es actuar como **protocolo estructurado**, repetible y entendible por terceros.

---

## ¿Qué problema busca resolver?

En muchos flujos de desarrollo asistido por IA, el análisis de seguridad queda disperso, implícito o poco documentado.  
RSAP propone un enfoque distinto:

- reglas explícitas,
- entregables consistentes,
- criterios comparables,
- y una separación clara entre análisis, evidencia y certificación.

Esto ayuda a reducir improvisación y mejora la capacidad de revisar si un repositorio está siendo mantenido con criterios de seguridad razonables.

---

## Estructura del repositorio

Actualmente este repositorio contiene dos *skills* principales:

- `security-audit-skill/`  
  Skill orientada a realizar una **auditoría de seguridad estructurada** sobre un repositorio GitHub.

- `rsap-certifications-skill/`  
  Skill orientada a generar el archivo **`CERTIFICATIONS.md`**, que funciona como índice público de confianza y estado de cumplimiento del protocolo.

---

## Skills incluidas

### 1. `security-audit-github`

Esta skill define el proceso para analizar un repositorio y producir un informe técnico de auditoría.

Sus objetivos incluyen:

- inventariar archivos relevantes,
- detectar hallazgos por severidad,
- identificar riesgos de secretos, configuración, hardening y producción,
- aplicar una rúbrica por ejes,
- generar una tabla de métricas con puntuaciones entre 0 y 100.

### Output esperado

- informe técnico en Markdown,
- riesgos priorizados,
- tabla de métricas,
- base para sello o visualización radial de seguridad.

---

### 2. `rsap-certifications`

Esta skill toma el estado general del repositorio y consolida certificaciones visibles en un único documento.

Sus objetivos incluyen evaluar la presencia y completitud de:

- `README.md`
- `SECURITY.md`
- `SCRIPTS.md`
- sello de seguridad
- sello de calidad
- workflows de GitHub Actions / CI
- GitHub Advisory / canal de disclosure

### Output esperado

- archivo `CERTIFICATIONS.md`
- resumen de elementos completos, incompletos y ausentes
- priorización de próximos pasos para alcanzar mayor madurez RSAP

---

## Cómo entender RSAP

RSAP está pensado como un protocolo con dos niveles complementarios:

### Nivel 1 — Auditoría técnica
Se revisa el repositorio, sus archivos, configuración y señales operativas para identificar riesgos, fortalezas y debilidades.

### Nivel 2 — Certificación visible
Se traduce el resultado en documentación entendible por terceros, de modo que el estado del proyecto no dependa solo de interpretación subjetiva.

---

## Áreas de evaluación

La auditoría RSAP trabaja sobre ejes como:

- gestión de secretos,
- hardening de superficie,
- sanitización y validación,
- buenas prácticas de código,
- mantenibilidad,
- privacidad y datos,
- configuración del repositorio,
- preparación para producción.

Estas áreas permiten construir una visión más equilibrada del estado del proyecto, especialmente en contextos donde se usa IA para asistir desarrollo o revisión.

---

## Relación con IA y desarrollo seguro

Este repositorio no contiene una aplicación tradicional.  
Su foco está en **definir skills y criterios** que puedan ser usados en flujos de trabajo con IA para mejorar la calidad del análisis.

RSAP busca que el uso de IA en desarrollo no se limite a “generar código”, sino que también contribuya a:

- revisar riesgos,
- explicitar decisiones,
- detectar omisiones,
- fortalecer documentación,
- y promover una cultura de seguridad desde etapas tempranas.

En ese sentido, RSAP se puede entender como una herramienta de **calibración**:  
ayuda a alinear el uso de IA con prácticas más prudentes, verificables y mantenibles.

---

## Estado del proyecto

**Estado actual:** en desarrollo temprano.

RSAP se encuentra en una etapa inicial de expansión. La estructura base ya define intención, alcance y outputs esperados, pero aún puede evolucionar en:

- templates adicionales,
- ejemplos de auditoría reales,
- integración con workflows,
- automatización de chequeos,
- mejoras de documentación,
- y refinamiento de criterios de certificación.

La prudencia forma parte del enfoque del proyecto: avanzar con criterio es preferible a prometer más de lo que hoy puede sostenerse.

---

## Casos de uso posibles

RSAP puede ser útil para:

- repositorios personales que quieren elevar su estándar de seguridad,
- proyectos open source que desean comunicar mejor su madurez,
- equipos que usan IA y quieren más trazabilidad,
- auditorías preliminares antes de publicar o escalar un proyecto,
- generación de documentación de confianza para terceros.

---

## Qué RSAP no promete

RSAP **no garantiza ausencia de vulnerabilidades**.  
Tampoco sustituye:

- auditorías profesionales especializadas,
- pentesting,
- revisión legal o de compliance,
- hardening operativo real en infraestructura externa.

El protocolo sirve como apoyo estructurado, no como certificado absoluto.

---

## Principios del proyecto

- **Prudencia antes que marketing**
- **Trazabilidad antes que ambigüedad**
- **Criterio explícito antes que intuición opaca**
- **Mejora incremental antes que falsa sensación de seguridad**
- **IA como apoyo auditable, no como autoridad incuestionable**

---

## Siguientes pasos sugeridos

Algunas mejoras recomendadas para el repositorio:

1. agregar ejemplos reales de auditoría RSAP,
2. incorporar `CERTIFICATIONS.md` de ejemplo,
3. añadir `SCRIPTS.md` con verificaciones automatizables,
4. incluir workflows de GitHub Actions,
5. ampliar documentación para adopción por terceros.

---

## Seguridad

Si detectas una vulnerabilidad, exposición de información sensible o una debilidad relevante en el protocolo, por favor revisa **`SECURITY.md`** antes de reportarla públicamente.

---

## Licencia

Este proyecto se distribuye bajo licencia **Apache-2.0**.

---

## Visión

RSAP propone una idea simple pero importante:

> si la IA puede ayudar a generar software, también debe ayudar a hacerlo con más criterio, más trazabilidad y más seguridad.

Ese es el espíritu de este repositorio.