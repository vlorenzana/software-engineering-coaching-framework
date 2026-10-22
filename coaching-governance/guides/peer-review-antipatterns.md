# Antipatrones en Revisiones de Pares: Guía de Observación para el Coach

## Propósito

Esta guía cataloga los errores operativos y culturales más frecuentes en las revisiones de pares (*peer review*) — cada uno con su impacto observable y su estrategia de mitigación. El coach utiliza estos antipatrones como señales de `secav:CoachingIntervention`: si un patrón aparece de forma recurrente en las sesiones que observa, es candidato a una conversación individual o grupal.

Esta guía es el contrapunto a `coaching-governance/guides/code-review-best-practices.md`, que describe qué hacer. Esta guía describe qué evitar.

---

## 1. Revisar estilo manualmente

**Impacto:** El equipo gasta energía analítica en debates triviales — sangría, llaves, espacios — que desvían la atención del diseño y la lógica.

**Señal observable para el coach:**
- Los comentarios de la revisión se concentran en formato en lugar de arquitectura, seguridad o lógica de negocio.
- Los ingenieros discuten convenciones de estilo durante la sesión en lugar de delegarla a herramientas.
- El pipeline de CI/CD no tiene linters o formateadores configurados, o los ingenieros los ignoran.

**Estrategia de mitigación:**
Delegar el formato al 100 % a linters y formateadores automáticos en CI/CD. La energía humana en una revisión es un recurso escaso: debe invertirse en lo que la automatización no puede detectar.

**Referencia:** `coaching-governance/guides/code-review-best-practices.md` §3.7 — Style and consistency.

---

## 2. Sesiones demasiado largas

**Impacto:** La agudeza visual cae drásticamente después de 60 minutos continuos. Los errores complejos pasan desapercibidos cuando el revisor ya está en fatiga analítica.

**Señal observable para el coach:**
- Las sesiones de revisión superan 60 minutos continuos o 400 líneas de código (LOC) por bloque.
- Los hallazgos documentados en la segunda mitad de la sesión son superficiales o de bajo impacto comparados con los de la primera.
- Los ingenieros reportan agotamiento o pérdida de concentración al terminar revisiones largas.

**Estrategia de mitigación:**
Limitar cada bloque de revisión a un máximo de 60 minutos o 400 LOC. Si el cambio es mayor, dividirlo en bloques con descanso entre ellos o en sesiones separadas.

**Referencia:** `coaching-governance/guides/code-review-best-practices.md` §1 — Scope and size.

---

## 3. Falta de contexto inicial

**Impacto:** El revisor gasta tiempo intentando adivinar el propósito de los cambios, ralentizando el ciclo e incrementando el riesgo de aprobar código sin comprender su intención.

**Señal observable para el coach:**
- Los Pull Requests (PR) no incluyen descripción del *por qué*, *cómo* y criterios de aceptación.
- Los revisores hacen preguntas al autor sobre el propósito del cambio durante la sesión — señal de que ese contexto no estaba disponible antes.
- Los revisores reportan haber necesitado revisar tickets o documentos externos para entender el cambio.

**Estrategia de mitigación:**
Exigir que cada PR incluya una descripción estructurada con al menos: propósito del cambio, enfoque de implementación y criterios de aceptación. Esta es una responsabilidad del autor, no del revisor.

**Referencia:** `coaching-governance/guides/code-review-best-practices.md` §2 — Preparing a change for review.

---

## 4. Código inacabado o en estado WIP

**Impacto:** Las revisiones prematuras invalidan el esfuerzo previo cuando el código cambia a mitad de la sesión. Generan retrabajo y erosionan la confianza del revisor en el proceso.

**Señal observable para el coach:**
- Los revisores reciben PRs que todavía tienen TODOs sin resolver, pruebas que fallan, o cambios marcados como borradores.
- El autor modifica el código mientras la revisión está en curso, invalidando comentarios ya escritos.
- Los revisores expresan frustración porque sus comentarios quedan obsoletos entre revisión y revisión.

**Estrategia de mitigación:**
Usar el estado *Draft PR* para trabajo en progreso. La revisión formal solo se solicita cuando las pruebas automatizadas pasan completamente y el autor considera el código listo.

---

## 5. Falta de empatía en el feedback

**Impacto:** Los comentarios percibidos como ataques personales destruyen la confianza del equipo y generan actitud defensiva, reduciendo la calidad del diálogo técnico en revisiones futuras.

**Señal observable para el coach:**
- Los comentarios se dirigen al autor: *"tú hiciste mal X"*, *"nunca manejas este caso"*.
- El autor adopta postura defensiva — justifica sus decisiones en lugar de explorarlas.
- Los ingenieros evitan someter su código a revisión o dilatan la solicitud de revisión.
- Los comentarios no incluyen prefijos de severidad: no hay distinción entre sugerencias y bloqueantes.

**Estrategia de mitigación:**
Comentar siempre sobre el código, nunca sobre la persona. Usar formulaciones como *"el módulo X podría..."* en lugar de *"tú hiciste mal X"*. Etiquetar los comentarios con prefijos explícitos: `[Sugerencia]`, `[Bloqueante]`, `Nit:`.

**Referencia:** `coaching-governance/guides/code-review-best-practices.md` §4 — How to give feedback.

---

## 6. Falta de rigor con código asistido por IA

**Impacto:** El código generado o modificado por asistentes automáticos puede contener alucinaciones lógicas, duplicación sutil o vulnerabilidades que no son detectables por inspección superficial. La aprobación automática de código de IA introduce deuda técnica y riesgos de seguridad no auditados.

**Señal observable para el coach:**
- Los revisores aprueban código de IA sin evidencia de que revisaron la lógica de negocio explícitamente.
- El `secav:ReviewRecord` no indica que el artefacto fue producido con asistencia de IA (`secav:assistedByAI`).
- Los ingenieros asumen que el código generado por IA es correcto si los tests pasan.

**Estrategia de mitigación:**
El revisor humano debe validar exhaustivamente la lógica de negocio de todo código asistido por IA — especialmente las condiciones de borde y los flujos de datos. La IA no sustituye la revisión humana; la revisión humana de código de IA es obligatoria, no opcional.

**Referencia:** `coaching-governance/guides/code-review-best-practices.md` §9 — AI-assisted code and review; `coaching-governance/guides/ai-assisted-code-review.md`.

---

## 7. Lista de verificación mental del revisor eficiente

Antes de iniciar una sesión de revisión, el ingeniero verifica su estado bio-cognitivo. El coach observa si el equipo aplica estas condiciones de manera sistemática o las omite bajo presión.

| Fase | Control requerido | Señal de alerta para el coach |
|---|---|---|
| **Energía biológica** | Realizar revisiones complejas durante ventanas de mayor claridad mental (preferiblemente por la mañana); nunca bajo fatiga extrema al final de la jornada. | Revisiones sistemáticamente programadas al final del día o fuera del horario normal. |
| **Aislamiento** | Bloquear 30–60 minutos en el calendario; silenciar notificaciones de Slack, Teams y correo para evitar pérdida de foco por cambios de contexto. | Los ingenieros revisan código entre reuniones o con notificaciones activas. |
| **Análisis crítico** | Ignorar detalles estéticos ya cubiertos por herramientas automatizadas; enfocar la energía mental en arquitectura, seguridad de entradas y lógica de negocio. | Los hallazgos de revisión son mayoritariamente de estilo en lugar de diseño o seguridad. |
| **Cierre asertivo** | Calificar los aportes de forma explícita: si el código cumple su propósito con detalles menores, aprobar el cambio y dejar sugerencias como mejoras opcionales. | Las revisiones terminan sin decisión clara — sin aprobación ni lista de bloqueantes definida. |

---

## 8. Integración con SECAV-O

| Antipatrón | Término SECAV-O |
|---|---|
| Revisión de estilo manual (sin automatización) | `secav:ReviewActivity` con hallazgos de bajo impacto; coaching signal sobre uso de herramientas |
| Sesión demasiado larga | Condición previa de `secav:ReviewActivity` degradada; observable como precondición de `secav:HumanValidationActivity` |
| Falta de contexto en el PR | `secav:Artifact` sin descripción adecuada; la trazabilidad del cambio es incompleta |
| Código WIP en revisión formal | `secav:ReviewActivity` prematura; invalida potencial `secav:ReviewFinding` |
| Feedback sin empatía | `secav:ReviewFinding` formulado sobre la persona, no el artefacto; señal para `secav:CoachingIntervention` |
| Código IA sin escrutinio | `secav:HumanValidationActivity` incompleta; `secav:assistedByAI` sin validación registrada |

---

## 9. Documentos relacionados

| Documento | Relación |
|---|---|
| `coaching-governance/guides/code-review-best-practices.md` | Prácticas positivas que son el contrapunto de cada antipatrón de esta guía |
| `coaching-governance/guides/peer-review-sessions.md` | Protocolo del coach como observador silencioso en la sesión de revisión |
| `coaching-governance/guides/ai-assisted-code-review.md` | Guía completa de revisión de código asistido por IA |
| `coaching-governance/guides/formal-inspections.md` | Proceso de inspección formal para módulos críticos — mayor rigor que la revisión de pares |
| `templates/engineer-coaching-assessment.md` | Plantilla donde se registran observaciones de competencia derivadas de revisiones |
| `templates/defect-log.csv` | Registro de defectos que permite identificar patrones recurrentes por tipo y autor |