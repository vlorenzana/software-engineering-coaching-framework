# Criterios de Proceso Robusto

> **Estado:** criterios CR-1 a CR-5 definidos — criterios adicionales pendientes de incorporación (ver tabla de resumen).

## Principio

Un proceso de desarrollo puede cumplir el criterio de calidad mínima razonable (`coaching-governance/guides/minimum-quality-criteria.md`) y aun así presentar señales de fragilidad: revisiones que no encuentran nada, diseño de comportamiento implícito no documentado, defectos que no se registran. El **proceso robusto** es el nivel siguiente: aquel en que las prácticas de calidad producen evidencia consistente, verificable y autoexplicativa de que están funcionando.

La distinción fundamental entre calidad mínima y proceso robusto es que el proceso robusto genera su propia evidencia de efectividad. No basta con realizar las prácticas; las prácticas deben producir hallazgos observables que confirmen que se ejecutaron con rigor.

---

## Criterios

### CR-1 — Las inspecciones se realizan sobre los productos críticos

Los artefactos de mayor riesgo de cada fase productiva son inspeccionados formalmente por más de un revisor antes de que la fase concluya, siguiendo los criterios de selección definidos en `coaching-governance/guides/minimum-quality-criteria.md` §1.

En un proceso robusto esto no es opcional ni dependiente de la presión de tiempo: si un artefacto crítico no fue inspeccionado, el coach documenta una `secavo:QualityPlanningConcern` y escala si el patrón se repite.

**Evidencia que el coach observa:**

- `secav:ReviewRecord` existente por cada artefacto crítico identificado en el sprint.
- Participación de al menos dos revisores en cada inspección.
- Ausencia de inspección sobre artefacto crítico → `secavo:QualityPlanningConcern` documentada.

**SECAV-O:** `secav:DesignReview`, `secav:CodeReview`, `secav:UnitTestDesignReview`, `secav:ReviewRecord`, `secavo:QualityPlanningConcern`.

---

### CR-2 — El comportamiento dinámico se diseña con diagramas UML de actividad o de secuencia

Toda lógica cuyo comportamiento varía según el flujo de control, la interacción entre actores o el orden de mensajes entre componentes debe estar modelada explícitamente mediante al menos uno de los siguientes diagramas UML:

- **Diagrama de actividad / flujo:** para lógica de proceso, flujos de trabajo, algoritmos con ramificaciones y bucles.
- **Diagrama de secuencia:** para interacciones entre componentes, servicios, actores o capas en un orden temporal definido.

La ausencia de estos diagramas cuando el comportamiento es dinámico equivale a diseño implícito: los ingenieros deben inferir el comportamiento del código, lo que eleva el riesgo de defectos de integración, interpretaciones divergentes y dificultad de revisión.

Este criterio complementa el estándar de diagramas de estado de `coaching-governance/guides/design-documentation-standards.md`, que ya establece el requisito de diagramas de estado para entidades con comportamiento variable por estado.

**Cuándo aplica cada diagrama:**

| Situación | Diagrama requerido |
|---|---|
| Lógica de proceso con ramificaciones (if/else, bucles, condiciones de guarda) | Actividad / flujo |
| Interacción entre dos o más componentes, servicios o actores con orden de mensajes | Secuencia |
| Entidad con comportamiento que depende de su estado interno | Estado (`design-documentation-standards.md`) |
| Combinaciones de las anteriores | Uno o más de los anteriores, según aplique |

**Criterios de calidad del diagrama:**

Un diagrama de actividad o secuencia es válido como artefacto de diseño inspeccionable si cumple:

1. Es consistente con el código o la especificación que modela — no es decorativo ni está desactualizado.
2. Cubre los flujos principales y los flujos alternativos o de error más relevantes.
3. En diagramas de actividad: los puntos de decisión tienen condiciones de guarda explícitas en todas las ramas.
4. En diagramas de secuencia: cada mensaje incluye el nombre de la operación o evento; los retornos relevantes están representados.
5. Es legible sin necesidad de consultar el código para interpretar el flujo.

La ausencia de un diagrama requerido es un hallazgo bloqueante en la revisión del artefacto de diseño (`secav:ReviewFinding` de tipo `missingRequiredDiagram`). La omisión sistemática a lo largo de varios sprints activa una `secavo:QualityPlanningConcern`.

**Evidencia que el coach observa:**

- `secav:DesignArtifact` incluye diagrama de actividad o secuencia cuando el comportamiento es dinámico.
- El diagrama es inspeccionado como parte del `secav:ReviewRecord` del artefacto de diseño.
- Hallazgos de revisión referenciando inconsistencias o ausencias en los diagramas.

**SECAV-O:** `secav:DesignArtifact`, `secav:DesignReview`, `secav:ReviewFinding`, `secav:DesignActivity`, `secav:DesignCompetency`, `secavo:QualityPlanningConcern`.

---

### CR-3 — Los defectos resultantes de inspecciones y revisiones se documentan

Cada hallazgo generado en una inspección o revisión se registra en el sistema de seguimiento con los campos mínimos requeridos por el modelo de métricas:

- categoría del defecto;
- severidad;
- fase donde fue inyectado (`phaseInjected`);
- fase donde fue detectado (`phaseDetected`);
- artefacto afectado;
- actividad de ingeniería asociada;
- acción de corrección asignada con responsable.

La documentación de defectos no es un trámite administrativo: es la fuente de datos que permite identificar patrones de inyección, evaluar la efectividad de las revisiones y calibrar los objetivos del coaching. Un proceso que realiza revisiones pero no documenta los hallazgos no puede demostrar que las revisiones funcionan.

**SECAV-O:** `secavo:DefectObservation` con `secavo:phaseInjected` y `secavo:phaseDetected`, `secav:ReviewFinding`, `secav:ReviewRecord`, `coaching-governance/guides/defect-tracking.md`.

---

### CR-4 y CR-5 — Las revisiones individuales generan hallazgos; donde no los generan, el coach emite un waiver justificado

#### CR-4 — Las revisiones producen hallazgos

Una revisión individual que no produce ningún hallazgo es, en la mayoría de los casos, una señal de revisión superficial o de preparación insuficiente — no de un artefacto perfecto. La ausencia sistemática de hallazgos en revisiones individuales es el indicador más claro de que la práctica se está ejecutando como formalidad y no como actividad de calidad.

En un proceso robusto, se espera que las revisiones produzcan hallazgos. La cantidad esperada depende de la complejidad del artefacto, la experiencia del revisor y el estado del proceso, pero **cero hallazgos repetidos en revisiones sucesivas sin justificación** es un patrón que el coach debe intervenir.

El coach observa los `secav:ReviewRecord` de cada revisor individual y evalúa si el número y tipo de hallazgos son consistentes con la complejidad del artefacto revisado.

#### CR-5 — Waiver del coach cuando la revisión no genera hallazgos

Cuando una revisión individual legítimamente no produce hallazgos — porque el artefacto fue corregido exhaustivamente antes de la revisión, porque el revisor tiene evidencia objetiva de que el artefacto cumple todos los criterios de aceptación, o porque el artefacto es de baja complejidad y alcance acotado — el coach emite un **waiver** que justifica la ausencia de hallazgos.

El waiver documenta:

1. **Identidad del artefacto y del revisor.**
2. **Justificación objetiva:** por qué se considera que la ausencia de hallazgos es legítima en este caso (no es una opinión; debe referenciarse evidencia: historial de correcciones previas, complejidad reducida, alcance acotado, etc.).
3. **Criterio de validez:** qué criterios de aceptación fueron verificados y cómo.
4. **Firma del coach** y fecha.

El waiver no exime al revisor de la preparación requerida; confirma que el coach verificó que la ausencia de hallazgos tiene una explicación objetiva. Un waiver sin justificación objetiva es inválido.

**Cuándo NO emitir waiver:**

- El revisor no preparó individualmente el artefacto antes de la sesión.
- El artefacto es de alta complejidad y no hay evidencia de preparación exhaustiva.
- El patrón de cero hallazgos se repite en el mismo revisor en múltiples sprints sin justificación cambiante.

En esos casos, el coach registra una `secav:CoachingIntervention` dirigida al desarrollo de la competencia de revisión del ingeniero.

**SECAV-O (CR-4):** `secav:ReviewRecord`, `secav:ReviewFinding`, `secav:CompetencyAssessment`, `secav:ReviewCompetency`, `secav:CoachingIntervention`.

**SECAV-O (CR-5):** `secavo:CoachWaiver` *(término propuesto — ver §SECAV-O)*, `secav:ReviewRecord`.

---

## SECAV-O — término propuesto

El criterio CR-5 introduce un concepto nuevo que requiere representación en la ontología:

| Término propuesto | Clase / Property | Descripción |
|---|---|---|
| `secavo:CoachWaiver` | Clase | Documento emitido por el coach que justifica objetivamente la ausencia de hallazgos en una revisión individual. |
| `secavo:waiverJustification` | Data property (`xsd:string`) | Texto de justificación objetiva del waiver. |
| `secavo:waiverIssuedBy` | Object property → `secav:Coach` | Coach que emite el waiver. |
| `secavo:waiverForReviewRecord` | Object property → `secav:ReviewRecord` | El registro de revisión al que aplica el waiver. |
| `secavo:waiverDate` | Data property (`xsd:date`) | Fecha de emisión. |

> Estos términos son propuestos y deben añadirse a `ontology/secav-o-coaching-governance-extension.ttl` cuando se incorpore el criterio al baseline del framework.

---

## Resumen de criterios (estado actual)

| ID | Criterio | Estado |
|---|---|---|
| CR-1 | Inspecciones sobre productos críticos | Definido |
| CR-2 | Comportamiento dinámico diseñado con diagramas UML de actividad o secuencia | Definido |
| CR-3 | Defectos resultantes de revisiones documentados | Definido |
| CR-4 | Las revisiones individuales generan hallazgos | Definido |
| CR-5 | Waiver del coach justificado cuando la revisión no genera hallazgos | Definido |
| CR-6… | *(pendientes de incorporación)* | Pendiente |

---

## Relación con la escala de calidad del framework

| Nivel | Descripción |
|---|---|
| **Por debajo del mínimo** | No se inspeccionan artefactos críticos. Los defectos se acumulan entre fases. |
| **Calidad mínima razonable** (`minimum-quality-criteria.md`) | Los artefactos críticos de cada fase son inspeccionados por más de un revisor. |
| **Proceso robusto** *(este documento)* | Las prácticas de calidad producen evidencia verificable de su efectividad: hallazgos documentados, diseño de comportamiento explícito, waivers justificados cuando las revisiones no generan hallazgos. |
| **Calidad aspiracional** | Definida en `coaching-governance/guides/minimum-quality-criteria.md` — la mayoría o todos los artefactos de cada fase son inspeccionados; las organizaciones maduran hacia este nivel de forma incremental. |

---

## Documentos relacionados

| Documento | Relación |
|---|---|
| `coaching-governance/guides/minimum-quality-criteria.md` | Nivel de calidad previo — piso del framework |
| `coaching-governance/guides/design-documentation-standards.md` | Estándar de diagramas de estado — CR-2 lo complementa con actividad y secuencia |
| `coaching-governance/guides/formal-inspections.md` | Protocolo de inspección formal — base de CR-1 |
| `coaching-governance/guides/peer-review-sessions.md` | Protocolo de revisión de pares — base de CR-4 y CR-5 |
| `coaching-governance/guides/requirements-inspection.md` | Inspección de requerimientos — instancia de CR-1 |
| `coaching-governance/guides/defect-tracking.md` | Registro de defectos — base de CR-3 |
| `coaching-governance/docs/metrics-model.md` | Modelo de métricas — interpretación de hallazgos y tendencias |