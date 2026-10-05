# Revisiones de Pares: Protocolo de Observación del Coach

## Propósito

Esta guía describe el protocolo de presencia del coach durante las revisiones de pares (`secav:CodeReview`, `secav:DesignReview`). El coach asiste pero no es un participante activo — su rol es observar, tomar notas y recoger evidencia. La revisión la conducen los ingenieros.

---

## 1. Rol del coach: observador silencioso

**El coach está presente pero no participa.**

Esto significa:

- No da su opinión técnica durante la sesión.
- No aprueba ni rechaza hallazgos.
- No media activamente en desacuerdos.
- No corrige a los ingenieros en voz alta durante la reunión.

El coach toma notas. Sus observaciones se convierten en `secav:ReviewFinding` y `secav:WorkProductEvidence` que informan la `secav:CompetencyAssessment` posterior, y pueden derivar en una `secav:CoachingIntervention` en la sesión individual, no en la revisión misma.

> La razón de esta restricción es estructural: si el coach interviene, los ingenieros dejan de resolver y esperan su juicio. La revisión deja de ser de pares.

---

## 2. Principio central: revisar el producto, no a la persona

Desde el inicio de la sesión, los ingenieros deben enfocar la revisión en el artefacto — el código, el diseño, el documento — no en el autor.

Indicadores de que el foco está en el producto:

- Los comentarios se formulan sobre el artefacto: *"Este bloque no maneja el caso nulo"*, no *"nunca manejas los casos nulos"*.
- Las preguntas se dirigen al código: *"¿Qué sucede aquí si el valor es negativo?"*
- El autor escucha sin ponerse a la defensiva, porque el objeto de evaluación es el artefacto.
- El desacuerdo técnico se trata como una pregunta abierta sobre el producto, no como un juicio sobre la competencia del autor.

El coach anota cuando los comentarios derivan hacia juicios sobre la persona. Esa observación alimenta una conversación posterior con quien corresponda — fuera de la sesión.

---

## 3. Disciplina de foco: observación del coach cuando el equipo se desvía

Si el coach nota que los ingenieros se están desenfocando — debatiendo temas ajenos al artefacto, derivando hacia diseño de nuevas funcionalidades, discutiendo procesos no relacionados, o prolongando un punto sin avanzar — el coach lo registra como observación.

**El coach no interviene verbalmente.** Puede usar una señal acordada previamente con el equipo (por ejemplo, una tarjeta visible, un gesto establecido) para indicar que el tiempo del punto está consumiéndose, si el equipo así lo solicitó al inicio. Fuera de eso, no interrumpe.

El patrón de desvíos sistemáticos es una señal de coaching: puede indicar que los criterios de revisión no están claros, que la sesión está mal acotada, o que el equipo necesita práctica en la disciplina de revisión. El coach lleva esto a la próxima sesión individual o retrospectiva.

---

## 4. Desacuerdos no resueltos: punto pendiente y escalación al Líder de Proyecto

Cuando los ingenieros no llegan a un acuerdo en un punto de la revisión y consideran que ya lo han debatido suficientemente, el procedimiento es:

1. **Marcar el punto como pendiente** — no seguir debatiendo. El punto se registra en el `secav:ReviewRecord` como hallazgo sin resolución.
2. **Continuar con el resto de la revisión** — no bloquear toda la sesión por un único punto en disputa.
3. **Al final de la sesión**, el equipo notifica al **Líder de Proyecto** sobre los puntos pendientes para que los resuelva o escale a quien corresponda.

El coach anota los puntos pendientes durante la sesión. No decide ni desempata — eso es responsabilidad del Líder de Proyecto.

### Criterio para declarar un punto "suficientemente debatido"

Un punto está suficientemente debatido cuando:
- Las dos posiciones han sido expresadas con sus argumentos técnicos.
- Ninguna nueva evidencia o argumento ha emergido en las últimas rondas de intercambio.
- El debate ha superado un tiempo proporcional a la importancia del punto (orientativo: más de 5–10 minutos en un punto sin avance es señal de escalación).

---

## 5. Notas del coach: qué registrar

Durante la sesión el coach registra:

| Qué observar | Por qué importa |
|---|---|
| Quién participa y quién no | Distribución de participación — señal de dominio o inhibición |
| Cómo se formulan los comentarios (producto vs. persona) | Indicador de cultura de revisión |
| Puntos donde el debate se extiende sin resolución | Candidatos a escalación; posible ambigüedad de criterios |
| Desvíos de foco | Señal de que los criterios de revisión no son suficientemente claros |
| Decisiones técnicas acordadas | Evidencia de razonamiento colectivo |
| Puntos marcados como pendientes | A trasladar al Líder de Proyecto |
| Hallazgos técnicos significativos | `secav:ReviewFinding` que informan `secav:CompetencyAssessment` |

Las notas del coach son internas al proceso de coaching. No se comparten con la gerencia como evaluación de rendimiento individual.

---

## 6. Después de la sesión: uso de las observaciones

Las observaciones del coach se usan en tres contextos, todos fuera de la sesión de revisión:

1. **Sesión individual con cada ingeniero** — feedback específico sobre su rol en la revisión (cómo formuló comentarios, cómo respondió al feedback, participación).
2. **Retrospectiva del sprint** — si el patrón de desvíos o desacuerdos es sistemático, el coach lo introduce como tema de mejora del proceso de revisión del equipo (`secavo:ImprovementAction`).
3. **Evaluación de competencias** — los hallazgos técnicos y de proceso informan la `secav:CompetencyAssessment` de cada ingeniero en las dimensiones de `secav:ReviewCompetency`.

---

## 7. Integración con SECAV-O

| Concepto | Término SECAV-O |
|---|---|
| La revisión de pares como actividad | `secav:CodeReview` o `secav:DesignReview` (subclases de `secav:ReviewActivity`) |
| Registro de la sesión | `secav:ReviewRecord` (subclase de `secav:Artifact` y `secav:Evidence`) |
| Hallazgos documentados | `secav:ReviewFinding` (subclase de `secav:Evidence`) |
| Punto no resuelto registrado | `secav:ReviewFinding` con estado "pendiente" |
| Notas de observación del coach | `secav:WorkProductEvidence` |
| Evaluación de competencias posterior | `secav:CompetencyAssessment` sobre `secav:ReviewCompetency` |
| Feedback posterior al ingeniero | `secav:CoachingRecommendation` |
| Intervención si hay patrón sistémico | `secav:CoachingIntervention`, `secavo:ImprovementAction` |

---

## 8. Documentos relacionados

| Documento | Relación |
|---|---|
| `guides/code-review-best-practices.md` | Prácticas de revisión para autor y revisor; complementa este protocolo |
| `guides/formal-inspections.md` | Proceso más riguroso para módulos críticos; el coach tiene rol de moderador (no observador silencioso) |
| `guides/coach-team-behaviors.md` | Comportamientos del líder de equipo que el coach observa, incluyendo en sesiones de revisión |
| `templates/sprint-retrospective.md` | Espacio para introducir patrones de revisión como tema de mejora |
| `templates/engineer-coaching-assessment.md` | Plantilla donde se registran las observaciones de competencia derivadas |
| `templates/engineer-development-record.md` | Registro longitudinal que acumula la evidencia de revisiones por ciclo |