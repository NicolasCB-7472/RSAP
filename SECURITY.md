# Security Policy

## Alcance

Este repositorio define y documenta **skills, criterios y artefactos del protocolo RSAP** (Repository Security Audit Protocol) para uso en flujos de trabajo asistidos por IA.

Aunque no se trata de una aplicación productiva tradicional, sí puede contener elementos sensibles desde el punto de vista de seguridad, por ejemplo:

- criterios de auditoría mal definidos,
- templates inseguros o ambiguos,
- recomendaciones que induzcan malas prácticas,
- exposición accidental de secretos o credenciales,
- documentación que genere una falsa percepción de seguridad.

Por esa razón, los reportes de seguridad son bienvenidos.

---

## Qué reportar

Se consideran relevantes, entre otros, los siguientes hallazgos:

- secretos, tokens, claves o credenciales expuestas en el repositorio,
- archivos sensibles commiteados por error,
- plantillas o instrucciones que promuevan prácticas inseguras,
- omisiones críticas en la documentación de seguridad,
- fallos en workflows o automatizaciones que puedan degradar controles del repositorio,
- inconsistencias graves entre el protocolo y prácticas mínimas de desarrollo seguro,
- contenido que pueda inducir a una certificación engañosa o no sustentable.

---

## Qué no reportar como vulnerabilidad

En principio, no se consideran vulnerabilidades de seguridad por sí solas:

- errores tipográficos,
- diferencias de estilo editorial,
- desacuerdos menores sobre redacción,
- ausencia de features no relacionadas con seguridad,
- sugerencias generales de mejora sin impacto razonable en riesgo.

Aun así, si tienes dudas, es preferible reportarlo con contexto.

---

## Cómo reportar un problema de seguridad

Por favor **no publiques secretos ni material sensible en issues públicos**.

Si detectas un problema de seguridad:

1. prepara una descripción clara del hallazgo,
2. indica archivo(s) afectados, si corresponde,
3. explica impacto potencial,
4. incluye pasos de reproducción si aplican,
5. comparte solo la mínima evidencia necesaria.

Si el hallazgo incluye credenciales o material sensible, **redáctalo parcialmente** y evita exponer el valor completo.

---

## Canal de reporte

Actualmente, si no existe un canal privado adicional configurado en GitHub, la recomendación es:

- abrir un canal privado de contacto tan pronto como el proyecto madure, y
- mientras tanto, evitar toda divulgación pública de secretos o material explotable.

Si necesitas reportar algo crítico y el repositorio aún no dispone de un canal privado formal, la prioridad debe ser **contener la exposición** antes de difundir detalles.

---

## Buenas prácticas esperadas para este repositorio

Este repositorio busca mantener, como mínimo, las siguientes prácticas:

- no almacenar secretos reales,
- no commitear archivos `.env` con valores activos,
- documentar con claridad el alcance del protocolo,
- revisar que las skills no fomenten patrones inseguros,
- mejorar progresivamente controles de higiene del repositorio,
- corregir con prioridad cualquier exposición de información sensible.

---

## Divulgación responsable

Se agradece una divulgación responsable y prudente.

La intención es:

- confirmar recepción del reporte,
- evaluar el impacto,
- corregir el problema en un plazo razonable,
- y luego documentar el cambio sin exponer innecesariamente material sensible.

Los tiempos exactos pueden variar porque el proyecto está en etapa temprana, pero los reportes bien documentados serán tratados con seriedad.

---

## Limitaciones actuales

Este proyecto está en evolución.  
Eso implica que algunos controles, automatizaciones o canales formales todavía pueden no estar completos.

Esa falta de madurez no invalida los reportes; al contrario, los hace especialmente útiles para fortalecer el protocolo desde temprano.

---

## Principio rector

RSAP no busca prometer seguridad absoluta.

Busca algo más útil y honesto:

- hacer visibles los riesgos,
- mejorar criterios,
- reducir errores evitables,
- y promover un uso más seguro y responsable de la IA en desarrollo de software.

Gracias por contribuir a ese objetivo.