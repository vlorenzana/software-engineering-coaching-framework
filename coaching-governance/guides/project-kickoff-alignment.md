# Alineación de Objetivos de Proyecto: Reunión Pre-Inicio

## Propósito

Antes de iniciar un proyecto, se recomienda una reunión entre el **Líder Técnico**, el **Coach** y el **responsable de alta gerencia** para establecer los objetivos medibles que definirán el éxito del proyecto. Esta reunión fija el punto de referencia contra el que se medirán el avance del equipo y los resultados del coaching.

Sin esta alineación explícita, los objetivos quedan implícitos o dispersos; el equipo optimiza para lo que percibe que se le evaluará, y el coach no tiene una base acordada para orientar las intervenciones de coaching.

---

## 1. Participantes

| Rol | Función en la reunión |
|---|---|
| **Responsable de alta gerencia** | Define y valida los objetivos organizacionales del proyecto (`secavo:InstitutionalObjective`, `secavo:ProjectObjective`). Autoriza los compromisos de recursos y plazos. |
| **Líder Técnico** | Traduce los objetivos organizacionales a metas técnicas y operativas alcanzables. Señala restricciones técnicas que afecten la definición de metas. |
| **Coach** | Verifica que los objetivos sean medibles y trazables. Propone al menos un objetivo de calidad de software si ninguno ha sido incluido. Conecta los objetivos del proyecto con el plan de coaching del ciclo (`secavo:AnnualCoachingPlan`). |

---

## 2. Criterios para los objetivos del proyecto

### 2.1 Pocos, pero significativos

Los objetivos del proyecto deben ser pocos — suficientes para guiar el trabajo sin dispersar el foco. Un número excesivo de objetivos diluyye la atención y hace imposible la rendición de cuentas real.

### 2.2 Medibles y verificables

Cada objetivo debe poder evaluarse con datos observables al cierre del proyecto:

- ¿Qué métrica lo representa? (`secavo:Metric`)
- ¿Cuál es el umbral de éxito?
- ¿Cómo y cuándo se mide? (`secavo:MeasurementObservation`)

### 2.3 Al menos un objetivo de calidad de software

Se recomienda que al menos uno de los objetivos acordados con gerencia esté relacionado explícitamente con defectos o calidad de software. Ejemplos medibles:

| Objetivo de calidad | Término SECAV-O |
|---|---|
| Tasa de defectos encontrados en producción por debajo de un umbral | `secavo:DefectObservation` + umbral en `secavo:Metric` |
| Porcentaje de cambios cubiertos por revisión de código | `secavo:ReviewObservation` + umbral en `secavo:Metric` |
| Porcentaje de defectos detectados en revisión (vs. en producción) | `secavo:DefectObservation` por fase (`templates/defect-log.csv`) |
| Tiempo medio de resolución de defectos críticos | `secavo:Metric` de tiempo; observado en `secavo:MeasurementObservation` |

Incluir un objetivo de calidad garantiza que la calidad de ingeniería tenga representación explícita en los compromisos del proyecto — no solo como deuda técnica que se gestiona después.

---

## 3. Objetivos del equipo

Una vez establecidos los objetivos con gerencia, el equipo puede fijar sus propios objetivos internos. Estos **pueden ser más agresivos** que los compromisos con gerencia — son metas de excelencia, no el piso del contrato.

El coach facilita esta sesión y verifica que:

- Los objetivos del equipo estén alineados con los compromisos de gerencia y los alcancen o superen.
- **El coach no permite objetivos de equipo menos exigentes que los acordados con gerencia.** Si el equipo propone metas más débiles, el coach señala la discrepancia y facilita la revisión.
- El equipo comprende la diferencia entre el compromiso organizacional (mínimo acordado) y su aspiración interna (meta de excelencia).

---

## 4. Objetivos individuales

De forma análoga, cada ingeniero puede establecer objetivos individuales alineados con los del equipo. Estos también pueden ser más agresivos — metas de desarrollo personal conectadas con las competencias que el proyecto va a demandar.

El coach es responsable de:

- Verificar que los objetivos individuales estén conectados con las competencias requeridas por el proyecto (`secav:CompetencyAssessment` como línea base).
- **No permitir objetivos individuales menos exigentes que la contribución esperada al equipo.** Si un objetivo individual está por debajo del aporte mínimo esperado, el coach lo señala en la sesión de planificación individual.
- Documentar los objetivos individuales en el plan de coaching del ciclo (`secavo:AnnualCoachingPlan`, `secavo:CoachingObjective`).

---

## 5. Rol del coach en la reunión con gerencia

El coach no es un espectador en esta reunión. Sus responsabilidades específicas son:

- **Verificar que cada objetivo propuesto sea medible.** Si un objetivo no puede responderse con datos observables, lo señala en el momento — no después.
- **Proponer o solicitar al menos un objetivo de calidad.** Si ninguno de los objetivos propuestos incluye una dimensión de defectos o calidad de software, el coach lo introduce como requisito del framework.
- **Registrar los objetivos acordados** como `secavo:CoachingObjective` vinculados a `secavo:ProjectObjective` mediante `secavo:alignsWithProjectObjective`, y a `secavo:InstitutionalObjective` mediante `secavo:alignsWithInstitutionalObjective`.
- **No permitir la dilución de objetivos.** Si durante la reunión los compromisos se debilitan sin justificación técnica válida, el coach puede documentar una preocupación formal de planificación (`secavo:QualityPlanningConcern`) siguiendo el mecanismo de `templates/quality-planning-dissent-and-escalation.md`.

---

## 6. Outputs esperados de la reunión

| Output | Dónde se registra |
|---|---|
| Objetivos organizacionales del proyecto (pocos, medibles, con al menos uno de calidad) | `templates/annual-coaching-plan.md` §Institutional alignment |
| Métricas y umbrales de éxito para cada objetivo | `templates/metrics-register.csv` |
| Objetivos de equipo (igual o más agresivos que los organizacionales) | `templates/annual-coaching-plan.md` §Team objectives |
| Objetivos individuales por ingeniero | `templates/engineer-development-record.md` §Competency plan |
| Registro de preocupación formal si objetivos se diluyeron | `templates/quality-planning-dissent-and-escalation.md` |

---

## 7. Integración con SECAV-O

| Concepto | Término SECAV-O |
|---|---|
| Objetivo organizacional del proyecto | `secavo:ProjectObjective` |
| Objetivo institucional (nivel organización) | `secavo:InstitutionalObjective` |
| Objetivo de coaching derivado del proyecto | `secavo:CoachingObjective` |
| Alineación objetivo coaching ↔ proyecto | `secavo:alignsWithProjectObjective` |
| Alineación objetivo coaching ↔ institucional | `secavo:alignsWithInstitutionalObjective` |
| Métrica de éxito | `secavo:Metric` |
| Medición de defectos como objetivo de calidad | `secavo:DefectObservation` (subClase de `secavo:MeasurementObservation`) |
| Medición de revisiones de código | `secavo:ReviewObservation` (subClase de `secavo:MeasurementObservation`) |
| Línea base individual de competencias | `secav:CompetencyAssessment` |
| Preocupación formal si objetivos se diluyen | `secavo:QualityPlanningConcern` |
| Plan de coaching actualizado | `secavo:AnnualCoachingPlan` |
| Decisión de planificación documentada | `secavo:PlanningDecision` |

---

## 8. Documentos relacionados

| Documento | Relación |
|---|---|
| `coaching-governance/docs/project-planning-participation.md` | Participación formal del coach en planificación y escalación |
| `coaching-governance/docs/institutional-alignment.md` | Método para conectar objetivos de coaching con objetivos institucionales |
| `templates/annual-coaching-plan.md` | Plan donde se registran los objetivos acordados |
| `templates/quality-planning-dissent-and-escalation.md` | Mecanismo formal si los objetivos se diluyen sin justificación |
| `templates/metrics-register.csv` | Registro de métricas y umbrales acordados |
| `templates/defect-log.csv` | Registro de defectos para objetivos de calidad |
| `templates/engineer-development-record.md` | Registro de objetivos individuales por ingeniero |