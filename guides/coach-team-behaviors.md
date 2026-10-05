# Comportamientos Observables del Coach en el Equipo

## Propósito

Esta guía describe conductas concretas y verificables que el coach debe manifestar al trabajar con su equipo. A diferencia del Código de Ética (`docs/coach-code-of-ethics.md`), que establece principios, esta guía describe señales observables en la práctica diaria — indicadores que el propio coach, los miembros del equipo, y el Comité de Coaches (`docs/coach-committee.md`) pueden usar para evaluar si el rol se está ejerciendo de forma adecuada.

Estas conductas no son aspiraciones abstractas. Son indicadores concretos que pueden recogerse como `secav:Evidence` durante las retrospectivas y las supervisiones del Comité.

---

## 1. Facilitación y protagonismo del equipo

El coach facilita; no lidera. El objetivo es que el equipo desarrolle capacidad propia, no que dependa del juicio del coach para funcionar.

**Conductas observables:**

- Hace preguntas en lugar de dar respuestas directas cuando el equipo tiene la capacidad de encontrarlas. (*"¿Qué opciones ven para resolver esto?" en lugar de "La solución es X."*)
- Distribuye el tiempo de participación en reuniones: ningún individuo — incluido el coach — domina la conversación de forma sistemática.
- Cuando una idea o solución emerge del equipo, la atribuye explícitamente a quien la propuso.
- Invita a participar a los miembros más silenciosos antes de dar por cerrado un punto.
- En sesiones de planificación o revisión, abre el espacio para que el equipo llegue a sus propias conclusiones antes de compartir su propia perspectiva.

**Señales de alerta:**

- El coach habla más del 50 % del tiempo en reuniones de equipo.
- Las decisiones técnicas o de proceso se toman únicamente cuando el coach está presente.
- Los miembros del equipo esperan la aprobación del coach antes de actuar, incluso en tareas dentro de su competencia.
- Las ideas son recurrentemente atribuidas al coach, no a quien las originó.

---

## 2. Toma de decisiones: consenso y restricciones visibles

El coach impulsa el consenso como primera opción y ancla las decisiones en las restricciones reales del proyecto, no en preferencias personales.

**Conductas observables:**

- Antes de proponer una votación, agota el espacio de deliberación para buscar un acuerdo construido colectivamente.
- Hace explícitas las restricciones del proyecto — plazos, presupuesto, requisitos técnicos, políticas organizacionales — y las mantiene visibles durante la discusión.
- Cuando una decisión se toma, documenta brevemente el razonamiento y la restricción que la justificó.
- Diferencia entre decisiones que requieren consenso del equipo y decisiones que son responsabilidad individual del ingeniero en su área de competencia.
- Evita imponer su preferencia técnica cuando el equipo ha llegado a una alternativa razonable dentro de las restricciones.

**Señales de alerta:**

- Las restricciones del proyecto son conocidas por el coach pero no están comunicadas ni visibles para el equipo.
- Las decisiones se justifican con "porque yo lo digo" o con la autoridad del coach, no con criterios objetivos.
- Se fuerza una votación antes de que todos los miembros hayan tenido oportunidad de expresar su posición.
- El resultado de las discusiones coincide sistemáticamente con la posición inicial del coach, independientemente del debate.

---

## 3. Gestión participativa de riesgos

El coach guía al equipo en la identificación y mitigación de riesgos. No identifica los riesgos solo, ni asigna acciones sin involucrar al equipo.

**Conductas observables:**

- En cada `secavo:SprintRetrospective`, propone revisar el registro de riesgos (`templates/risk-register.csv`) como un punto estructurado, no ocasional.
- Abre sesiones de lluvia de ideas de riesgos con preguntas abiertas: *"¿Qué podría impedirnos completar este objetivo?"*, *"¿Qué suposición estamos haciendo que podría resultar incorrecta?"*
- No presenta la lista de riesgos como definitiva. La construye con el equipo y reconoce aportes específicos.
- Cuando un riesgo se materializa, guía al equipo a identificar y documentar una `secavo:CorrectiveAction` sin asignar culpa a personas.
- Para riesgos identificados, motiva al equipo a proponer `secavo:PreventiveAction` antes de que el coach sugiera las suyas.

**Señales de alerta:**

- El registro de riesgos es elaborado solo por el coach y presentado al equipo como información, no como construcción colectiva.
- Las sesiones de riesgos se saltan cuando el tiempo está ajustado.
- Cuando un riesgo se materializa, la discusión se centra en quién falló, no en qué se puede aprender y corregir.
- Las acciones preventivas y correctivas son asignadas por el coach sin consultar quién tiene la capacidad y disponibilidad para ejecutarlas.

---

## 4. Distribución del trabajo

El coach asigna trabajo de acuerdo a las capacidades del equipo y mantiene su propia carga de tareas al mínimo necesario. El trabajo de coaching es observar, guiar y evidenciar — no ejecutar.

**Conductas observables:**

- La mayor parte del trabajo técnico del sprint está asignada a los ingenieros; el coach no concentra tareas de entrega.
- Al asignar trabajo, considera el nivel de competencia actual de cada ingeniero (`secav:CompetencyAssessment`) y los objetivos de desarrollo del ciclo.
- Asigna tareas desafiantes a ingenieros cuyo objetivo de desarrollo incluye esa área — no solo a quien ya la domina.
- Distribuye el trabajo crítico entre varios miembros, evitando la concentración en el ingeniero más senior.
- Cuando el coach asume una tarea operativa, lo hace de forma explícita y temporal, con criterio claro de cuándo la devuelve al equipo.

**Señales de alerta:**

- Las tareas más visibles o técnicamente complejas recaen sistemáticamente en el mismo ingeniero (generalmente el más senior).
- El coach acumula tareas de entrega de forma rutinaria.
- Las asignaciones ignoran los objetivos de desarrollo acordados y responden solo a la urgencia.
- Ningún miembro del equipo puede describir con claridad por qué le fue asignada su tarea.

---

## 5. Respeto y cultura de equipo

El coach establece el tono cultural del equipo a través de sus propias conductas, no solo de sus palabras.

**Conductas observables:**

- **Corrige en privado, felicita en público.** Cuando un ingeniero comete un error o necesita una corrección de conducta, la conversación ocurre en un espacio individual, no frente a sus pares ni en canales grupales. Cuando un logro merece reconocimiento, se expresa en el espacio colectivo del equipo.
- Mantiene el mismo tono de respeto en comunicaciones escritas (mensajes, comentarios de código, tickets) que en conversaciones presenciales.
- Trata a todos los miembros del equipo con el mismo nivel de consideración, independientemente de su antigüedad, nivel de competencia o relación personal.
- Reconoce sus propios errores frente al equipo cuando corresponde — modela que equivocarse y corregir es parte del proceso.
- No interrumpe a los miembros del equipo mientras exponen su razonamiento.
- Distingue entre feedback sobre el trabajo y juicios sobre la persona.

**Señales de alerta:**

- Las correcciones o críticas se realizan en presencia de otros miembros del equipo o en canales donde pueden ser vistas por terceros no involucrados.
- El reconocimiento es escaso o se da de forma genérica, sin atribuir logros específicos a personas concretas.
- El tono en mensajes escritos es notablemente más cortante que en conversaciones directas.
- Existe un patrón en que ciertos miembros reciben más atención, oportunidades o feedback que otros sin justificación en los objetivos de desarrollo.

---

## 6. Lista de verificación de autoevaluación

El coach puede usar esta lista al final de cada sprint para revisar sus propias conductas. Los ítems marcados como "No" o "No aplica aún" son candidatos a una `secavo:ImprovementAction` en la retrospectiva.

| Comportamiento | Sí | Parcial | No |
|---|---|---|---|
| El equipo propuso y construyó soluciones sin esperar mis respuestas directas | | | |
| Distribuí el tiempo de participación en reuniones — no monopolicé la conversación | | | |
| Las restricciones del proyecto eran visibles y las usamos como base de las decisiones | | | |
| Buscamos consenso antes de recurrir a votación o decisión unilateral | | | |
| Revisamos el registro de riesgos en la retrospectiva | | | |
| El equipo propuso acciones preventivas — yo no las dicté | | | |
| Las asignaciones de trabajo consideraron los objetivos de desarrollo de cada ingeniero | | | |
| Mi propia carga de tareas de entrega fue mínima | | | |
| Todas las correcciones a personas se dieron en privado | | | |
| Reconocí logros específicos en el espacio colectivo del equipo | | | |

---

## 7. Integración con SECAV-O

| Conducta | Término SECAV-O |
|---|---|
| Observar actividades de ingeniería sin dirigirlas | `secav:Coach` — `secav:ReviewActivity`, `secav:EngineeringActivity` |
| Evidencia de participación del equipo en riesgos | `secavo:Risk` generado con el equipo, registrado en `secavo:SprintRetrospective` |
| Asignación de trabajo según competencia | `secav:CompetencyAssessment` como criterio de distribución |
| Acciones preventivas propuestas por el equipo | `secavo:PreventiveAction` con origen en lluvia de ideas colectiva |
| Acciones correctivas al materializar un riesgo | `secavo:CorrectiveAction` documentada sin asignación de culpa |
| Corrección de conducta del coach en retrospectiva | `secavo:ImprovementAction` (subclase de `secav:CoachingIntervention`) |
| Evidencia de conductas para supervisión del Comité | `secav:WorkProductEvidence`, `secav:ReviewFinding` |

---

## 8. Documentos relacionados

| Documento | Relación |
|---|---|
| `docs/coach-code-of-ethics.md` | Principios éticos que fundamentan estas conductas |
| `docs/coach-committee.md` | El Comité puede usar estas conductas como criterio de supervisión |
| `guides/risk-management.md` | Protocolo detallado de gestión de riesgos |
| `templates/sprint-retrospective.md` | Espacio donde se recogen y discuten estas conductas |
| `templates/coach-committee-charter.md` | Registro de supervisión y posibles mejoras del coach |
| `templates/engineer-development-record.md` | Contexto de competencias que informa la distribución de trabajo |