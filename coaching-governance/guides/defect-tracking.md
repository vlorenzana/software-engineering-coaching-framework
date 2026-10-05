# Seguimiento de Defectos y Rol de Asistente de Calidad

## Propósito

Cuando el equipo dispone de un sistema de seguimiento de tickets — como Jira, Azure DevOps, Linear u otro equivalente — el cierre de los tickets relacionados con defectos (bugs) es responsabilidad del coach. Esta práctica permite recoger métricas de defectos de forma consistente y trazable, que alimentan la `secavo:DefectObservation` y el `templates/defect-log.csv`.

Si el coach está sobrecargado, puede delegar esta actividad a un miembro del equipo previamente capacitado y bajo seguimiento, designándolo formalmente como **Asistente de Calidad**.

---

## 1. Por qué el coach cierra los tickets de defectos

El coach cierra los tickets de defectos — no el autor que los corrigió ni el reportador que los abrió. La razón es doble:

**Consistencia de clasificación.** Cada defecto debe registrarse con la fase en la que fue inyectado (`secavo:phaseInjected`) y la fase en la que fue detectado (`secavo:phaseDetected`). Sin un criterio único de clasificación, estas fases se registran de forma inconsistente y las métricas resultantes no son comparables entre sprints ni entre equipos.

**Integridad de las métricas.** Si quien cierra el ticket es también quien lo corrigió, existe un incentivo implícito a clasificarlo de forma favorable. El coach es un observador neutral que aplica la definición acordada de cada fase.

El coach no tiene que reproducir ni verificar técnicamente la corrección — su rol al cerrar el ticket es registrar la clasificación del defecto: tipo, severidad, fase de inyección, fase de detección, y método de detección (`secavo:detectionMethod`).

---

## 2. Datos a registrar al cerrar un ticket de defecto

| Campo | Descripción | SECAV-O |
|---|---|---|
| Fase de inyección | En qué fase del desarrollo fue introducido el defecto (requisitos, diseño, codificación, pruebas) | `secavo:phaseInjected` |
| Fase de detección | En qué fase fue encontrado (revisión de código, prueba unitaria, integración, producción) | `secavo:phaseDetected` |
| Método de detección | Cómo fue encontrado (inspección formal, revisión de pares, prueba automatizada, reporte de usuario) | `secavo:detectionMethod` |
| Severidad | Impacto funcional del defecto (crítico, mayor, menor, cosmético) | `secavo:DefectObservation` |
| Módulo o componente | Para análisis de densidad de defectos por módulo | `secav:SourceCodeArtifact` |

Estos datos se trasladan al `templates/defect-log.csv` al final de cada sprint como parte de la recolección de métricas (`secavo:collectsMetric`).

---

## 3. Métricas que se obtienen del cierre de tickets

El registro sistemático de defectos permite calcular:

| Métrica | Descripción |
|---|---|
| **Defectos por sprint** | Volumen total de defectos detectados en el ciclo |
| **Tasa de escape** | Porcentaje de defectos encontrados en producción vs. en fases previas |
| **Densidad por módulo** | Defectos por módulo — identifica componentes de mayor riesgo |
| **Efectividad de revisión** | Porcentaje de defectos detectados en revisión de código o inspección formal |
| **Distribución por fase de inyección** | Indica si los defectos se originan principalmente en diseño, codificación o requisitos |

Estas métricas se revisan en cada `secavo:SprintRetrospective` y alimentan el `templates/metrics-register.csv` y los objetivos de calidad acordados en la reunión pre-inicio (`coaching-governance/guides/project-kickoff-alignment.md`).

---

## 4. Asistente de Calidad: delegación cuando el coach está saturado

Cuando el coach no puede asumir el cierre de tickets de forma sostenida — por ejemplo, si gestiona múltiples equipos simultáneamente — puede delegar esta actividad a un miembro del equipo designado como **Asistente de Calidad**.

Esta delegación no es automática. Requiere:

1. **Capacitación previa** — el coach entrena al asistente en la clasificación de defectos: definición de fases, criterios de severidad, método de detección, y uso del sistema de tickets.
2. **Seguimiento inicial** — durante al menos dos sprints, el coach revisa y valida los cierres realizados por el asistente antes de darlos por definitivos.
3. **Designación formal** — el coach documenta la designación del Asistente de Calidad en el plan de coaching del ciclo (`templates/annual-coaching-plan.md`), incluyendo el alcance de la delegación y el período de seguimiento.

### 4.1 Responsabilidades del Asistente de Calidad

| Responsabilidad | Descripción |
|---|---|
| Cierre de tickets de defectos | Aplica los criterios de clasificación acordados; no cierra si tiene dudas sobre la fase o la causa |
| Registro en el defect log | Traslada los datos al `templates/defect-log.csv` al final de cada sprint |
| Consulta al coach | Escala al coach cualquier defecto que no encaje claramente en los criterios establecidos |
| Reporte de anomalías | Informa al coach si detecta patrones inusuales en el volumen o tipo de defectos |

### 4.2 Lo que el Asistente de Calidad NO hace

- No define ni modifica los criterios de clasificación — eso es responsabilidad del coach.
- No cierra tickets que no sean defectos (tareas, mejoras, solicitudes de cambio).
- No toma decisiones sobre la severidad de defectos críticos sin consultar al coach.
- No reporta métricas directamente a gerencia — el coach consolida y comunica.

### 4.3 El asistente como oportunidad de desarrollo

La designación como Asistente de Calidad es también una intervención de coaching. El ingeniero que asume este rol desarrolla competencias en:

- Comprensión del ciclo de vida de defectos y su impacto en la calidad del producto.
- Análisis de patrones de defectos — señal de `secav:ReviewCompetency` y `secav:DesignCompetency`.
- Disciplina en el registro y clasificación de evidencia (`secav:DefectRecord`).

El coach puede usar la experiencia del asistente como evidencia para la `secav:CompetencyAssessment` del ciclo.

---

## 5. Integración con SECAV-O

| Concepto | Término SECAV-O |
|---|---|
| Defecto registrado al cerrar el ticket | `secav:DefectRecord` (subclase de `secav:Evidence`) |
| Observación de defecto con fase y método | `secavo:DefectObservation` (subclase de `secavo:MeasurementObservation`) |
| Fase de inyección del defecto | `secavo:phaseInjected` |
| Fase de detección del defecto | `secavo:phaseDetected` |
| Método de detección | `secavo:detectionMethod` |
| Métrica de defectos del sprint | `secavo:Metric`; recolectada en `secavo:CoachingSprint` |
| Recolección de métricas | `secavo:collectsMetric` (dominio: `secavo:CoachingSprint`) |
| Módulo donde se originó el defecto | `secav:SourceCodeArtifact` |
| Capacitación del asistente de calidad | `secav:CoachingIntervention` |
| Competencias desarrolladas por el asistente | `secav:CompetencyAssessment` sobre `secav:ReviewCompetency`, `secav:DesignCompetency` |

---

## 6. Documentos relacionados

| Documento | Relación |
|---|---|
| `templates/defect-log.csv` | Registro donde se consolidan los datos de cada ticket cerrado |
| `templates/metrics-register.csv` | Métricas de defectos por sprint |
| `templates/annual-coaching-plan.md` | Donde se documenta la designación del Asistente de Calidad |
| `coaching-governance/guides/project-kickoff-alignment.md` | Los objetivos de calidad acordados definen los umbrales de las métricas de defectos |
| `coaching-governance/guides/formal-inspections.md` | Las inspecciones formales son un método de detección de defectos antes de producción |
| `coaching-governance/docs/metrics-model.md` | Modelo completo de métricas de defectos, revisiones e inspecciones |