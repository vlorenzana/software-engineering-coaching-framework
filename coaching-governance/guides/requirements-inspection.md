# Inspección de Requerimientos

## Propósito

Los defectos introducidos en la fase de requerimientos son los más costosos de corregir: cuanto más tarde se detectan, más trabajo invalidan. Una inspección formal de requerimientos (`secav:DesignReview` sobre un `secav:DesignArtifact`) permite detectar ambigüedades, vaguedades e inconsistencias antes de que se traduzcan en código incorrecto.

El coach asiste a estas inspecciones como observador — toma notas y da retroalimentación después de la sesión, siguiendo el mismo protocolo que en inspecciones formales de código (`coaching-governance/guides/formal-inspections.md`) y revisiones de pares (`coaching-governance/guides/peer-review-sessions.md`).

---

## 1. Por qué se necesitan múltiples revisores

Algunos tipos de defectos en requerimientos **solo pueden detectarse cuando hay más de un revisor**. La ambigüedad es el caso más claro: un requerimiento es ambiguo cuando admite dos o más interpretaciones válidas. Un revisor único no puede generar por sí solo dos interpretaciones distintas del mismo texto — simplemente lo leerá de una forma y no verá el problema.

La inspección con múltiples revisores que trabajan de forma independiente y luego comparan sus interpretaciones es la técnica que hace visibles estas ambigüedades:

```
Revisor A lee el requerimiento → Interpretación A
Revisor B lee el requerimiento → Interpretación B
          ↓
  Interpretación A ≠ Interpretación B
          ↓
  El requerimiento es ambiguo → defecto detectado
```

Esto hace que la preparación individual previa a la reunión sea especialmente crítica en inspecciones de requerimientos: los revisores deben anotar su interpretación del requerimiento **antes** de escuchar la de los demás. Una vez que se conoce la interpretación del compañero, el sesgo de confirmación impide ver la propia con independencia.

---

## 2. Tipos de defectos que detecta la inspección

| Tipo de defecto | Descripción | ¿Requiere múltiples revisores para detectarse? |
|---|---|---|
| **Ambigüedad** | El requerimiento admite dos o más interpretaciones válidas | Sí — comparación de interpretaciones independientes |
| **Vaguedad** | Lenguaje impreciso sin definición operacional: "rápido", "fácil de usar", "eficiente" | No necesariamente, pero se detecta mejor con múltiples perspectivas |
| **Incompletitud** | Faltan casos, condiciones de borde, escenarios de error | No — un revisor con experiencia puede detectarla |
| **Inconsistencia** | Dos requerimientos que se contradicen entre sí | Útil tener revisores de distintas áreas para ver la contradicción entre dominios |
| **Inverificabilidad** | El requerimiento no puede probarse — no hay criterio observable de cumplimiento | No — pero se detecta mejor con quienes van a escribir las pruebas |
| **Inviabilidad** | El requerimiento no puede implementarse como está descrito | Requiere revisor técnico que conozca las restricciones del sistema |

---

## 3. Proceso de inspección de requerimientos

El proceso sigue las mismas cinco fases que la inspección formal de código (`coaching-governance/guides/formal-inspections.md`), con adaptaciones al objeto de revisión.

| Fase | Responsable | Descripción |
|---|---|---|
| **1. Planificación** | Líder Técnico / Arquitecto | Seleccionar los requerimientos a inspeccionar. Priorizar los de mayor riesgo: requerimientos que afectan muchas funcionalidades, que involucran integración con sistemas externos, o que han generado preguntas frecuentes. Distribuir el material con al menos 24–48 h de anticipación. |
| **2. Preparación individual** | Todos los inspectores | Cada inspector lee los requerimientos de forma independiente y registra: (a) su interpretación de cada requerimiento, (b) términos que considera vagos o sin definición, (c) casos o condiciones que el requerimiento no cubre. La preparación es obligatoria — es el paso que hace posible detectar ambigüedades. |
| **3. Reunión de inspección** | Moderador designado | Los inspectores comparan sus interpretaciones punto a punto. El moderador registra cada discrepancia como un `secav:ReviewFinding`. El coach asiste como observador silencioso — no interviene verbalmente. |
| **4. Rework** | Autor del requerimiento | El autor revisa y reescribe los requerimientos donde se encontraron defectos, con apoyo del Líder Técnico o el Arquitecto para decisiones de alcance. |
| **5. Seguimiento** | Coach | Verifica que los requerimientos marcados como defectuosos fueron corregidos antes de que avancen a diseño o implementación, revisando el `secav:ReviewRecord` actualizado. |

---

## 4. Criterios de calidad de un requerimiento

Los inspectores evalúan cada requerimiento contra estos criterios (`secav:QualityCriterion`):

| Criterio | Pregunta que responde |
|---|---|
| **Unívoco** | ¿Todos los lectores lo interpretan de la misma forma? |
| **Verificable** | ¿Existe un criterio observable que confirme si está cumplido? (`secav:AcceptanceCriterion`) |
| **Completo** | ¿Cubre los casos normales, los casos de error y los casos límite? |
| **Consistente** | ¿Contradice algún otro requerimiento del sistema? |
| **Factible** | ¿Puede implementarse dentro de las restricciones técnicas y de negocio conocidas? |
| **Rastreable** | ¿Puede vincularse a una necesidad de negocio o a un objetivo del proyecto? |

---

## 5. Rol del coach

El coach asiste a la reunión de inspección como **observador silencioso**, consistente con el protocolo establecido para todas las reuniones de revisión:

- No participa verbalmente durante la sesión.
- Toma notas de observación sobre el proceso: cómo comparan los inspectores sus interpretaciones, qué requerimientos generan más discrepancia, si los hallazgos se registran correctamente.
- Verifica que el `secav:ReviewRecord` se está completando con los datos necesarios.
- Da retroalimentación después de la sesión — grupal, individual, o a la organización — siguiendo el mismo criterio que en peer reviews e inspecciones formales.

### 5.1 Qué observa el coach específicamente

- **Preparación individual:** ¿vinieron los inspectores con sus anotaciones previas? Si no, el moderador debería reprogramar — el coach lo registra como señal de alerta.
- **Profundidad del análisis:** ¿los inspectores están comparando interpretaciones o solo leyendo el requerimiento en voz alta sin contrastar?
- **Registro de hallazgos:** ¿se están documentando los defectos con suficiente detalle para que el autor pueda corregirlos sin nueva reunión?
- **Patrón de defectos:** si el mismo tipo de defecto (ej. vaguedad) aparece en la mayoría de los requerimientos, es una señal de proceso — no de un autor individual.

### 5.2 Retroalimentación posterior

| Destinatario | Cuándo | Qué |
|---|---|---|
| **Equipo (grupal)** | Si el patrón afecta al proceso colectivo de escritura de requerimientos | Tipo de defecto más frecuente, recomendaciones de mejora del proceso |
| **Individual (privado)** | Si la observación es específica de un participante | Preparación insuficiente, dificultad para articular interpretaciones, etc. |
| **Organización** | Si los requerimientos presentan defectos sistémicos que reflejan ausencia de un proceso de elicitación o criterios de aceptación | Escalación formal o recomendación al Comité de Coaches |

---

## 6. Integración con SECAV-O

| Concepto | Término SECAV-O |
|---|---|
| Documento de requerimientos inspeccionado | `secav:DesignArtifact` |
| La inspección de requerimientos como actividad | `secav:DesignReview` (subclase de `secav:ReviewActivity` y `secav:DesignActivity`) |
| Criterios de calidad evaluados | `secav:QualityCriterion` |
| Criterio de verificabilidad del requerimiento | `secav:AcceptanceCriterion` |
| Registro de la inspección | `secav:ReviewRecord` |
| Hallazgo (ambigüedad, vaguedad, inconsistencia) | `secav:ReviewFinding` |
| Defecto registrado al cerrar | `secav:DefectRecord`; `secavo:DefectObservation` con `secavo:phaseInjected = "requirements"` |
| Fase de detección | `secavo:phaseDetected = "requirements review"` |
| Notas de observación del coach | `secav:WorkProductEvidence` |
| Retroalimentación posterior del coach | `secav:CoachingRecommendation` |
| Competencias desarrolladas en inspección | `secav:DesignCompetency`, `secav:ReviewCompetency` |
| Intervención si hay patrón sistémico | `secav:CoachingIntervention`, `secavo:ImprovementAction` |

---

## 7. Documentos relacionados

| Documento | Relación |
|---|---|
| `coaching-governance/guides/formal-inspections.md` | Protocolo base de inspecciones formales — el mismo proceso aplicado a código |
| `coaching-governance/guides/peer-review-sessions.md` | Mismo protocolo de observador silencioso para el coach |
| `coaching-governance/guides/defect-tracking.md` | Los defectos encontrados en inspección de requerimientos se registran con phaseInjected = "requirements" |
| `coaching-governance/docs/project-planning-participation.md` | La inspección de requerimientos debe ser incluida en el plan del proyecto |
| `coaching-governance/guides/project-kickoff-alignment.md` | Los objetivos de calidad pueden incluir métricas de defectos encontrados en fase de requerimientos |
| `templates/engineer-coaching-assessment.md` | La participación en inspecciones de requerimientos es evidencia de DesignCompetency |