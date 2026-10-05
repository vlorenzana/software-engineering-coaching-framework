# Inspecciones Formales de Módulos Críticos

## Propósito

No todos los artefactos del sistema merecen el mismo nivel de escrutinio. Las inspecciones formales son una actividad de revisión estructurada, más rigurosa que una revisión de código ordinaria, aplicada selectivamente a los módulos que concentran mayor riesgo de impacto.

Se recomienda que el arquitecto del sistema identifique los módulos críticos al inicio del proyecto, y que sobre esos módulos se planifiquen inspecciones formales guiadas por el coach y respaldadas por el Líder Técnico y la gerencia.

---

## 1. Rol del arquitecto: identificación de módulos críticos

El arquitecto es quien mejor conoce la distribución del riesgo técnico en el sistema. Su responsabilidad en este proceso es identificar, antes del inicio del desarrollo, qué módulos concentran mayor impacto potencial.

Un **módulo crítico** es aquel cuyo fallo, defecto o degradación genera consecuencias desproporcionadas sobre el sistema o el negocio. La identificación no requiere unanimidad — requiere juicio técnico documentado.

### 1.1 Criterios de criticidad

El arquitecto puede aplicar uno o más de los siguientes criterios para designar un módulo como crítico:

| Criterio | Descripción |
|---|---|
| **Impacto de fallo** | Un defecto en este módulo provoca fallos en cascada, pérdida de datos, o indisponibilidad del servicio |
| **Amplitud de uso** | El módulo es invocado por muchos otros componentes; un defecto se propaga ampliamente |
| **Complejidad estructural** | Alta complejidad ciclomática, múltiples caminos de ejecución, condiciones de borde difíciles de cubrir con pruebas automatizadas |
| **Seguridad o privacidad** | Maneja autenticación, autorización, cifrado, datos personales o información sensible |
| **Integridad de datos** | Responsable de transacciones, consistencia entre sistemas, o integridad referencial |
| **Novedad o incertidumbre** | Tecnología nueva para el equipo, patrón de diseño no probado en el contexto, o requisito ambiguo |

La lista de módulos críticos debe ser documentada y compartida con el Líder Técnico, el coach y la gerencia al inicio del proyecto.

---

## 2. La inspección formal

Una inspección formal es una revisión estructurada en la que un grupo de participantes con roles definidos examina un artefacto (`secav:SourceCodeArtifact` u otro `secav:Artifact`) contra criterios de calidad explícitos (`secav:QualityCriterion`, `secav:AcceptanceCriterion`), con el objetivo de identificar defectos antes de que avancen al siguiente fase del desarrollo.

La diferencia respecto a una revisión de código ordinaria es el grado de estructura: roles definidos, preparación individual obligatoria, reunión moderada, y registro formal de hallazgos (`secav:ReviewRecord`).

### 2.1 Fases del proceso

| Fase | Responsable | Descripción |
|---|---|---|
| **1. Planificación** | Coach + Líder Técnico | Seleccionar el módulo a inspeccionar, definir participantes, distribuir el material con anticipación (al menos 24–48 h antes de la reunión). |
| **2. Preparación individual** | Todos los participantes | Cada inspector revisa el artefacto de forma independiente y anota observaciones, preguntas y posibles defectos antes de la reunión. La preparación individual es obligatoria — no puede sustituirse por la lectura durante la reunión. |
| **3. Reunión de inspección** | Coach (moderador) | Revisión estructurada del artefacto. El autor escucha y responde preguntas; no defiende. El recorder documenta los hallazgos (`secav:ReviewFinding`). El coach mantiene el enfoque en defectos, no en preferencias de estilo. |
| **4. Rework** | Autor + Líder Técnico | El autor corrige los defectos identificados. El Líder Técnico puede orientar si la corrección requiere decisiones de diseño. |
| **5. Seguimiento** | Coach | El coach verifica que los hallazgos críticos fueron corregidos antes de que el módulo avance. Las correcciones se registran en el `secav:ReviewRecord`. |

---

## 3. Roles y responsabilidades

| Rol | Función en la inspección |
|---|---|
| **Arquitecto** | Define qué módulos son críticos y por qué. Puede participar como inspector en módulos de su dominio. |
| **Coach (moderador)** | Guía la reunión, mantiene la agenda, asegura que todos los participantes contribuyan, registra o supervisa el registro de hallazgos. No es el evaluador técnico principal — es el facilitador del proceso. |
| **Autor del módulo** | Presenta el artefacto brevemente. Escucha y responde preguntas sin defender decisiones de diseño durante la reunión. |
| **Inspectores** | Ingenieros del equipo o externos con competencia en el dominio. Revisaron el material individualmente y traen observaciones documentadas. |
| **Líder Técnico** | Resuelve ambigüedades técnicas durante la reunión y apoya al autor en la fase de rework. Garantiza que la inspección tenga el tiempo y los participantes necesarios. |
| **Gerencia** | Autoriza el tiempo de la inspección. Reconoce los hallazgos como evidencia de calidad — no los usa como instrumento de evaluación de rendimiento individual. |

---

## 4. Rol del coach

El coach no evalúa la calidad técnica del módulo directamente — facilita el proceso para que los ingenieros lo hagan. Sus responsabilidades específicas son:

- **Antes de la reunión:** verificar que la preparación individual se realizó. Si algún participante no preparó el material, reprogramar la reunión antes de comenzar.
- **Durante la reunión:** moderar el tiempo, distribuir la participación, redirigir debates de preferencia hacia la identificación de defectos objetivos. Clasificar cada hallazgo por tipo y severidad en el `secav:ReviewRecord`.
- **Después de la reunión:** verificar que los hallazgos críticos fueron corregidos antes del avance. Usar los hallazgos como evidencia de competencia (`secav:ReviewFinding` → `secav:CompetencyAssessment`).
- **Si la inspección revela un patrón sistémico** (el mismo tipo de defecto aparece en varios módulos): documentar una `secav:CoachingIntervention` o `secavo:ImprovementAction` dirigida al equipo, no al autor individual.

---

## 5. Soporte de gerencia y Líder Técnico

Las inspecciones formales solo son efectivas si cuentan con respaldo explícito de la gerencia y el Líder Técnico:

**Gerencia:**
- Incluir las inspecciones en el plan del proyecto como actividades de calidad con tiempo asignado.
- No tratar los hallazgos de una inspección como indicadores de rendimiento negativo del autor — los defectos encontrados antes de producción son éxitos del proceso, no fallos del individuo.
- Si la gerencia omite las inspecciones planeadas sin justificación técnica, el coach puede documentar una `secavo:QualityPlanningConcern`.

**Líder Técnico:**
- Participar en al menos la fase de planificación y la reunión de los módulos de mayor riesgo.
- Asegurar que el equipo tenga capacidad para la preparación individual — la preparación no se realiza dentro de la reunión.
- Orientar el rework cuando los hallazgos implican decisiones de diseño más amplias.

---

## 6. Outputs de la inspección

| Output | Descripción | SECAV-O |
|---|---|---|
| Registro de inspección | Artefacto, participantes, hallazgos, severidad, estado de corrección | `secav:ReviewRecord` |
| Hallazgos documentados | Lista de defectos clasificados por tipo y severidad | `secav:ReviewFinding` |
| Evidencia de competencia | Hallazgos usados para informar la evaluación del autor e inspectores | `secav:ReviewFinding` → `secav:CompetencyAssessment` |
| Intervención de coaching | Si hay un patrón sistémico en los hallazgos | `secav:CoachingIntervention`, `secavo:ImprovementAction` |
| Preocupación de calidad | Si la inspección fue omitida o reducida sin justificación | `secavo:QualityPlanningConcern` |

---

## 7. Integración con SECAV-O

| Concepto | Término SECAV-O |
|---|---|
| Módulo crítico bajo inspección | `secav:SourceCodeArtifact` (o `secav:Artifact`) |
| La inspección como actividad | `secav:CodeReview` (inspección formal de código); `secav:DesignReview` (inspección de diseño) |
| Criterios de calidad evaluados | `secav:QualityCriterion`, `secav:AcceptanceCriterion` |
| Registro de la inspección | `secav:ReviewRecord` (subclase de `secav:Artifact` y `secav:Evidence`) |
| Hallazgos documentados | `secav:ReviewFinding` (subclase de `secav:Evidence`) |
| Evidencia adicional producida | `secav:WorkProductEvidence` |
| Evaluación de competencias derivada | `secav:CompetencyAssessment` |
| Intervención por patrón sistémico | `secav:CoachingIntervention`, `secavo:ImprovementAction` |
| Recomendación al equipo | `secav:CoachingRecommendation` |
| Preocupación si inspección fue omitida | `secavo:QualityPlanningConcern` |
| Riesgo documentado si no se realizan | `secavo:Risk` |

---

## 8. Documentos relacionados

| Documento | Relación |
|---|---|
| `guides/project-kickoff-alignment.md` | Las inspecciones formales deben incluirse como actividades de calidad en los objetivos de proyecto |
| `docs/project-planning-participation.md` | El coach puede levantar una `QualityPlanningConcern` si las inspecciones se omiten del plan |
| `guides/code-review-best-practices.md` | Base para revisiones ordinarias; las inspecciones formales aplican un estándar más riguroso |
| `guides/ai-assisted-code-review.md` | Módulos críticos con código generado por IA requieren inspección formal adicional |
| `templates/quality-planning-dissent-and-escalation.md` | Mecanismo de escalación si la gerencia elimina inspecciones planeadas |
| `templates/engineer-coaching-assessment.md` | Los hallazgos de inspección alimentan la evaluación de competencias |