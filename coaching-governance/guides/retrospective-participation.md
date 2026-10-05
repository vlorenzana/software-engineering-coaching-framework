# Participación del Coach en la Retrospectiva

## Propósito

La retrospectiva de sprint (`secavo:SprintRetrospective`) es el espacio donde el equipo analiza los datos de calidad, revisa los riesgos y acuerda acciones de mejora. El rol del coach en este espacio depende de si el equipo cuenta con un facilitador de retrospectivas — como un Scrum Master u otro rol equivalente.

---

## 1. Dos modos de participación

### 1.1 Sin facilitador externo: el coach facilita la retrospectiva

Cuando el equipo no cuenta con un Scrum Master u otro rol que facilite la retrospectiva, el coach puede facilitar la sesión. En este modo:

- Conduce la agenda, distribuye la participación y mantiene el tiempo.
- Asegura que los datos de defectos y calidad (`secavo:DefectObservation`, `secavo:Metric`) sean presentados y analizados — no solo listados.
- Guía al equipo a derivar decisiones (`secavo:ImprovementAction`) a partir de los datos, no de opiniones.
- Registra el resultado de la sesión en la plantilla de retrospectiva (`templates/sprint-retrospective.md`) como `secavo:SprintRetrospective`.

Incluso cuando facilita, el coach toma notas de observación sobre el proceso del equipo: quién participa, cómo se debaten los datos, qué acuerdos se alcanzan. Estas notas alimentan la retroalimentación posterior.

### 1.2 Con facilitador externo: el coach es observador

Cuando el equipo cuenta con un Scrum Master u otro facilitador de retrospectivas, el coach asiste como observador silencioso — consistente con su rol en revisiones de pares (`coaching-governance/guides/peer-review-sessions.md`) e inspecciones formales (`coaching-governance/guides/formal-inspections.md`).

En este modo:

- No facilita, no dirige la agenda, no interviene verbalmente durante la sesión.
- Toma notas sobre el proceso y el contenido.
- Observa específicamente que los datos de defectos y calidad sean analizados y que el equipo tome decisiones concretas al respecto.
- Da retroalimentación después de la sesión.

> La razón de esta restricción es la misma que en revisiones de pares: si el coach interviene, el facilitador pierde autoridad y el equipo deja de dirigirse a sí mismo.

---

## 2. Qué observa el coach (en ambos modos)

Independientemente del modo, el coach presta atención a:

### 2.1 Análisis de datos de calidad y defectos

El coach verifica que la retrospectiva incluya:

- **Revisión de métricas de defectos del sprint:** volumen, tasa de escape, distribución por fase (`secavo:DefectObservation`, `secavo:phaseInjected`, `secavo:phaseDetected`).
- **Análisis de hallazgos de revisión:** resultados de revisiones de pares e inspecciones formales del sprint (`secav:ReviewFinding`).
- **Revisión del registro de riesgos:** estado de los riesgos activos y cierre de los mitigados (`secavo:Risk`).
- **Seguimiento de acciones del sprint anterior:** ¿se completaron las `secavo:ImprovementAction` acordadas?

**Señal de alerta:** si la retrospectiva se enfoca exclusivamente en el proceso y la dinámica del equipo pero omite los datos de calidad, el coach lo registra como observación y lo trata en la retroalimentación posterior.

### 2.2 Toma de decisiones basada en datos

El coach observa que el equipo no se limite a listar problemas, sino que:

- Identifica causas raíz de los defectos o hallazgos recurrentes.
- Acuerda `secavo:ImprovementAction` concretas, con responsable y plazo.
- Prioriza las acciones por impacto, no por urgencia percibida.
- Registra formalmente las decisiones en el `secavo:SprintRetrospective`.

---

## 3. Retroalimentación después de la retrospectiva

Al igual que en revisiones de pares e inspecciones, el coach da retroalimentación fuera de la sesión. La forma depende del patrón y el destinatario:

### 3.1 Retroalimentación al equipo (grupal)

Cuando el patrón observado afecta al equipo en su conjunto — por ejemplo, la retrospectiva no analizó los datos de calidad, o las decisiones tomadas no derivan de evidencia — el coach lo plantea como tema en la próxima sesión colectiva o al inicio del siguiente sprint.

### 3.2 Retroalimentación individual

Cuando la observación es específica de un participante — el Líder de Equipo que dirigió la agenda sin dar espacio a datos de calidad, o un miembro que bloqueó sistemáticamente las decisiones — el coach lo trata en sesión individual, en privado.

### 3.3 Retroalimentación a la organización

Si el patrón observado en retrospectivas sucesivas indica un problema organizacional — por ejemplo, la gerencia no actúa sobre las `secavo:ImprovementAction` acordadas, o hay presión para no registrar defectos — el coach documenta la observación y la escala siguiendo el mecanismo formal (`templates/quality-planning-dissent-and-escalation.md`), o la lleva al Comité de Coaches si aplica (`coaching-governance/docs/coach-committee.md`).

---

## 4. Integración con SECAV-O

| Concepto | Término SECAV-O |
|---|---|
| La retrospectiva como artefacto | `secavo:SprintRetrospective` |
| Datos de defectos analizados | `secavo:DefectObservation`, `secavo:phaseInjected`, `secavo:phaseDetected` |
| Hallazgos de revisión discutidos | `secav:ReviewFinding` |
| Métricas del sprint revisadas | `secavo:Metric` |
| Riesgos revisados | `secavo:Risk` |
| Decisiones de mejora acordadas | `secavo:ImprovementAction` |
| Notas de observación del coach | `secav:WorkProductEvidence` |
| Retroalimentación posterior al equipo o individuo | `secav:CoachingRecommendation` |
| Intervención si hay patrón sistémico | `secav:CoachingIntervention` |
| Escalación a organización | `secavo:QualityPlanningConcern` documentada en `secavo:SprintRetrospective` |

---

## 5. Documentos relacionados

| Documento | Relación |
|---|---|
| `templates/sprint-retrospective.md` | Plantilla donde se registra la `secavo:SprintRetrospective` |
| `coaching-governance/guides/defect-tracking.md` | Datos de defectos que deben revisarse en la retrospectiva |
| `coaching-governance/guides/peer-review-sessions.md` | Mismo protocolo de observador silencioso con retroalimentación posterior |
| `coaching-governance/guides/formal-inspections.md` | Hallazgos de inspecciones que se revisan en retrospectiva |
| `coaching-governance/guides/risk-management.md` | Protocolo de revisión de riesgos en retrospectiva |
| `coaching-governance/docs/coaching-cycle.md` | Contexto del ciclo completo donde se inserta la retrospectiva |
| `coaching-governance/docs/coach-committee.md` | Escalación de patrones organizacionales al Comité de Coaches |
| `templates/quality-planning-dissent-and-escalation.md` | Mecanismo formal de escalación a la organización |