# Glosario del Framework SECAV-O

Este glosario reúne los términos introducidos o redefinidos por el framework de coaching SECAV-O. Los términos de ingeniería de software de uso general (retrospectiva, sprint, requerimiento, prueba unitaria, etc.) no están incluidos salvo que el framework les dé un significado especializado.

---

## Índice temático

- [Calidad y criterios mínimos](#calidad-y-criterios-mínimos)
- [Documentación y glosarios](#documentación-y-glosarios)
- [Roles del framework](#roles-del-framework)
- [Actividades de revisión e inspección](#actividades-de-revisión-e-inspección)
- [Pruebas unitarias](#pruebas-unitarias)
- [Ciclo de coaching](#ciclo-de-coaching)
- [Métricas y trazabilidad de defectos](#métricas-y-trazabilidad-de-defectos)
- [Adopción incremental](#adopción-incremental)
- [Gestión de riesgos](#gestión-de-riesgos)

---

## Calidad y criterios mínimos

### Calidad mínima razonable
*Fuente: `coaching-governance/guides/minimum-quality-criteria.md`*

El umbral por debajo del cual una organización incurre en mala práctica de ingeniería, independientemente de las restricciones de tiempo o presupuesto que se invoquen para justificarlo. No es el estándar de calidad al que aspirar, sino el piso por debajo del cual el riesgo de fallo sistémico es inaceptable.

El criterio operativo es: los artefactos críticos de cada fase productiva deben ser inspeccionados por más de un revisor antes de que esa fase concluya.

Contrasta con la [calidad aspiracional](#calidad-aspiracional), que es el nivel al que las organizaciones maduran progresivamente.

**Término SECAV-O asociado:** `secav:QualityCriterion`, `secavo:QualityPlanningConcern`

---

### Calidad aspiracional
*Fuente: `coaching-governance/guides/minimum-quality-criteria.md`*

El nivel de calidad en el que la mayoría o todos los artefactos producidos en cada fase son inspeccionados formalmente. Es el ideal al que conviene aproximarse de forma incremental; presuponer que toda organización puede lograrlo desde el inicio es irreal.

Las organizaciones maduran hacia este nivel usando el modelo de adopción incremental (`coaching-governance/guides/incremental-adoption.md`).

---

### Criterio de avance entre fases
*Fuente: `coaching-governance/guides/minimum-quality-criteria.md`*

Condición que un artefacto debe cumplir antes de avanzar a la siguiente fase del desarrollo: (1) los hallazgos de la inspección están documentados en el `secav:ReviewRecord`; (2) los hallazgos críticos o bloqueantes están asignados con responsable y plazo; (3) el coach verifica en el seguimiento que los hallazgos bloqueantes fueron resueltos.

La presión de tiempo que lleva a omitir este criterio se registra como `secavo:QualityPlanningConcern`.

---

### Módulo crítico
*Fuente: `coaching-governance/guides/formal-inspections.md`*

Aquel cuyo fallo, defecto o degradación genera consecuencias desproporcionadas sobre el sistema o el negocio. El arquitecto identifica los módulos críticos usando al menos uno de estos seis criterios de riesgo:

| Criterio | Descripción |
|---|---|
| Impacto de fallo | Su fallo afecta funcionalidades centrales o genera daño irreversible |
| Amplitud de uso | Es utilizado o referenciado por muchos otros módulos o equipos |
| Complejidad estructural | Alta complejidad ciclomática, lógica condicional anidada, muchos casos de borde |
| Seguridad / privacidad | Maneja autenticación, autorización, datos personales o criptografía |
| Integridad de datos | Afecta persistencia, consistencia transaccional o integridad referencial |
| Novedad / incertidumbre | Usa una tecnología o patrón con el que el equipo tiene poca experiencia |

**Término SECAV-O asociado:** `secav:SourceCodeArtifact`, `secav:QualityCriterion`

---

### QualityPlanningConcern (Preocupación de planificación de calidad)
*Fuente: `coaching-governance/guides/formal-inspections.md`, `coaching-governance/guides/minimum-quality-criteria.md`*

Artefacto de escalación generado por el coach cuando una actividad de calidad obligatoria — inspección formal, revisión de pares, revisión de pruebas unitarias u otra — es omitida o reducida significativamente sin justificación técnica.

El coach documenta el artefacto, lo comunica al Líder Técnico y a la gerencia, y si el patrón es recurrente, lo lleva al Comité de Coaches.

**Término SECAV-O asociado:** `secavo:QualityPlanningConcern`

---

## Documentación y glosarios

### Glosario primario
*Fuente: `coaching-governance/guides/requirements-inspection.md`*

Glosario ubicado al **inicio** de un documento de requerimientos (o de cualquier documento técnico) que contiene los términos sin los cuales el lector no puede interpretar correctamente el documento. Si un término del glosario primario es ambiguo, todos los requerimientos que lo usan heredan esa ambigüedad.

Los términos del glosario primario son productos de trabajo inspeccionables con el mismo rigor que un requerimiento: **deben ser discutidos por dos o más revisores de forma independiente** antes de ser aceptados. Un término que dos revisores interpretan de forma distinta es un `secav:ReviewFinding` que debe resolverse antes de aprobar los requerimientos que lo usan.

Criterios de calidad de un término del glosario primario: interpretación unívoca entre revisores, definición operacional (permite decidir si algo pertenece o no al concepto), consistencia con otros términos, y correspondencia con el uso del dominio de negocio.

Contrasta con el [glosario secundario](#glosario-secundario).

**Término SECAV-O asociado:** `secav:DesignArtifact` (parte del documento), `secav:QualityCriterion`, `secav:ReviewFinding`

---

### Diagrama de estados
*Fuente: `coaching-governance/guides/design-documentation-standards.md`*

Artefacto de diseño obligatorio (`secav:DesignArtifact`) para cualquier entidad del sistema — clase, módulo, proceso, recurso o flujo de negocio — cuyo comportamiento varía según el estado en el que se encuentre. Su función es hacer visible simultáneamente todo el ciclo de vida del objeto: estados posibles, estado inicial, estados finales, transiciones, condiciones de guarda y acciones.

Un diagrama de estados completo debe incluir: estado inicial explícito (marcado con símbolo estándar), todos los estados posibles, estados finales explícitos, transiciones etiquetadas con el evento o condición que las dispara, condiciones de guarda, y acciones de transición cuando aplique.

La ausencia de un diagrama de estados cuando el sistema tiene estados, o un diagrama incompleto que omite estados finales o transiciones, es un `secav:ReviewFinding` bloqueante para avanzar a implementación.

**Término SECAV-O asociado:** `secav:DesignArtifact`, `secav:DesignReview`, `secav:QualityCriterion`, `secav:ReviewFinding`, `secav:DesignCompetency`

---

### Glosario secundario
*Fuente: `coaching-governance/guides/requirements-inspection.md`*

Glosario ubicado al **final** de un documento de requerimientos que contiene términos de apoyo: acrónimos, referencias a sistemas externos, convenciones de nomenclatura, y términos técnicos que aparecen ocasionalmente pero no son centrales para la comprensión del documento.

A diferencia del [glosario primario](#glosario-primario), los términos del glosario secundario tienen menor riesgo de propagar ambigüedad y no requieren el mismo nivel de inspección formal, aunque sí deben ser revisados por al menos un revisor adicional al autor.

---

## Roles del framework

### Asistente de Calidad
*Fuente: `coaching-governance/guides/defect-tracking.md`*

Miembro del equipo designado para cerrar tickets de defectos en el sistema de tracking cuando el coach no puede asumir esta actividad de forma sostenida. La designación requiere: capacitación previa impartida por el coach, al menos dos sprints de seguimiento supervisado con validación explícita, y registro formal de la designación en el plan de coaching.

El rol tiene alcance delimitado: solo puede clasificar y cerrar defectos con los criterios acordados; no toma decisiones sobre umbrales de calidad ni sobre qué defectos escalar. El rol también es una oportunidad de desarrollo en `secav:ReviewCompetency` y `secav:DesignCompetency`.

**Término SECAV-O asociado:** `secav:Engineer`, `secav:CoachingIntervention` (capacitación), `secav:CompetencyAssessment`

---

### Coach
*Fuente: `ontology/secav-o.ttl`, framework general*

Stakeholder (`secav:Coach`, subclase de `secav:Stakeholder`) responsable de observar actividades de ingeniería, recopilar evidencia, producir evaluaciones de competencia y generar intervenciones de coaching. En el contexto del framework, el coach actúa como [observador silencioso](#observador-silencioso) en reuniones de revisión e inspección, y da retroalimentación después de la sesión.

---

### Comité de Coaches (Coach Committee)
*Fuente: `coaching-governance/docs/coach-committee.md`*

Estructura de gobernanza que se forma cuando una organización tiene más de un coach. El comité coordina las prácticas de coaching, genera el plan de coaching organizacional, asegura la aplicación consistente del framework entre equipos, y gestiona la escalación de problemas que ningún coach individual puede resolver.

No es una jerarquía que reemplace la autonomía del coach en su equipo; es un órgano de coordinación y estándares.

**Término SECAV-O asociado:** `secavo:CoachCommittee` *(propuesto, no declarado aún en TTL)*

---

### Lead Coach (Coach Líder)
*Fuente: `coaching-governance/docs/coach-committee.md`*

Coordinador designado del Comité de Coaches. Responsable de la gobernanza del plan de coaching organizacional, del manejo de escalaciones inter-equipo, y de la comunicación externa con gerencia o recursos humanos. La designación puede hacerla la gerencia o el consenso del comité.

**Término SECAV-O asociado:** `secavo:LeadCoach` *(propuesto, no declarado aún en TTL)*

---

### Observador silencioso
*Fuente: `coaching-governance/guides/peer-review-sessions.md`, `coaching-governance/guides/formal-inspections.md`, `coaching-governance/guides/retrospective-participation.md`*

Rol que adopta el coach en todas las reuniones de revisión, inspección y retrospectiva (cuando hay facilitador externo). El coach:
- No da su opinión técnica durante la sesión.
- No aprueba ni rechaza hallazgos.
- No media activamente en desacuerdos.
- No corrige a los ingenieros en voz alta.
- Toma notas de observación como `secav:WorkProductEvidence`.
- Da retroalimentación — grupal, individual o a la organización — después de la sesión.

**Razón:** si el coach interviene durante la sesión, los ingenieros dejan de resolver por sí mismos y esperan su juicio. La revisión deja de ser de pares.

---

## Actividades de revisión e inspección

### ImprovementAction (Acción de mejora)
*Fuente: `coaching-governance/guides/retrospective-participation.md`, `coaching-governance/guides/peer-review-sessions.md`, `coaching-governance/guides/formal-inspections.md`*

Acción de mejora concreta acordada en una retrospectiva, con responsable y plazo definidos, derivada de datos observados (hallazgos de revisión, métricas de defectos, riesgos) en lugar de opiniones. Es una especialización de `secav:CoachingIntervention`.

**Término SECAV-O asociado:** `secavo:ImprovementAction` (subclase de `secav:CoachingIntervention`)

---

### Inspección formal
*Fuente: `coaching-governance/guides/formal-inspections.md`*

Revisión estructurada en la que un grupo de participantes con roles definidos examina un artefacto contra criterios de calidad explícitos, con el objetivo de identificar defectos antes de que avancen a la siguiente fase del desarrollo.

Se diferencia de una revisión de código ordinaria por el grado de estructura: roles definidos (moderador designado, recorder, inspectores), preparación individual obligatoria previa a la reunión, reunión moderada con agenda, y registro formal de hallazgos en un `secav:ReviewRecord`.

El coach asiste como [observador silencioso](#observador-silencioso). El moderador es un inspector designado, no el coach.

**Término SECAV-O asociado:** `secav:CodeReview` / `secav:DesignReview` / `secav:UnitTestDesignReview`, `secav:ReviewRecord`, `secav:ReviewFinding`

---

### Punto pendiente
*Fuente: `coaching-governance/guides/peer-review-sessions.md`*

Desacuerdo no resuelto en una revisión de pares que ha sido "suficientemente debatido": ambas posiciones fueron expresadas con argumentos técnicos, no emerge nueva evidencia, y el debate consumió tiempo desproporcionado. Se registra en el `secav:ReviewRecord` como hallazgo sin resolución y se escala al Líder de Proyecto después de la sesión, no durante ella.

---

### Revisión de pares (Peer review)
*Fuente: `coaching-governance/guides/peer-review-sessions.md`*

Sesión de revisión estructurada en la que los ingenieros — no el coach — examinan un artefacto de código o diseño. Se distingue de la inspección formal por menor estructura: no requiere protocolo de preparación individual obligatoria ni rol de recorder. El coach asiste como [observador silencioso](#observador-silencioso).

**Término SECAV-O asociado:** `secav:CodeReview` / `secav:DesignReview`

---

## Pruebas unitarias

### Análisis de valores límite (Boundary Value Analysis — BVA)
*Fuente: `coaching-governance/guides/unit-test-review.md`*

Técnica sistemática de diseño de casos de prueba que identifica los valores en los extremos de cada partición de equivalencia: límites numéricos (mínimo, máximo, cero, negativo), límites de colecciones (vacía, un elemento, capacidad máxima), y límites de cadenas (vacía, espacio, un carácter, muy larga). Fuente: Beizer, *Software Testing Techniques* (1990).

---

### Patrón AAA / GWT (Arrange-Act-Assert / Given-When-Then)
*Fuente: `coaching-governance/guides/unit-test-review.md`*

Estructura de tres partes para pruebas unitarias:
- **Arrange / Given:** configuración de datos de entrada y comportamiento de mocks.
- **Act / When:** ejecución del método bajo prueba, preferentemente en una sola línea.
- **Assert / Then:** verificación explícita del resultado esperado.

Una prueba que tiene lógica de control de flujo (`if`, `for`) en la sección Act o Assert tiene un defecto de diseño de casos. Fuente: Meszaros, *xUnit Test Patterns* (2007).

---

### Principios FIRST
*Fuente: `coaching-governance/guides/unit-test-review.md`*

Cinco criterios de calidad (`secav:QualityCriterion`) que toda prueba unitaria debe cumplir:

| Principio | Criterio |
|---|---|
| **Fast (Rápida)** | Ejecución en milisegundos; sin I/O real (bases de datos, red, sistema de archivos) |
| **Isolated (Aislada)** | Ninguna prueba depende del resultado de otra; sin estado global mutable compartido |
| **Repeatable (Repetible)** | Mismo resultado en cualquier entorno, fecha u hora de ejecución |
| **Self-Validating (Autovalidable)** | Resultado binario Pass / Fail; sin interpretación manual de logs |
| **Timely (Oportuna)** | Escrita en paralelo o antes del código de producción (TDD) |

Fuente: Martin, *Clean Code* (2008), capítulo 9.

---

## Ciclo de coaching

### Baseline de crecimiento inicial
*Fuente: `coaching-governance/docs/coaching-cycle.md`*

Perfil de competencia de un ingeniero establecido al inicio del ciclo de coaching o inmediatamente después del lanzamiento del equipo. Incluye: competencia demostrada, autonomía, evidencia de revisiones e inspecciones, patrones de defectos, historial de capacitación relevante y restricciones contextuales. No es un ranking punitivo: es el punto de comparación para medir el crecimiento longitudinal.

**Término SECAV-O asociado:** `secav:CompetencyAssessment`, `secav:WorkProductEvidence`

---

### Plan anual de coaching
*Fuente: `coaching-governance/docs/coaching-cycle.md`*

Artefacto que define las prioridades de desarrollo de competencias para el año, establece el baseline inicial, fija objetivos y resultados esperados, selecciona métricas y fuentes de evidencia, e identifica las actividades y artefactos que el coach observará. Es el marco dentro del cual se ejecutan los sprints de coaching.

**Término SECAV-O asociado:** `secavo:AnnualCoachingPlan`

---

### Plan de coaching organizacional
*Fuente: `coaching-governance/docs/coach-committee.md`*

Plan generado por el Comité de Coaches que agrega y coordina los planes individuales de cada equipo. Incluye objetivos de coaching a nivel organizacional, baseline de competencias entre equipos, registro de riesgos organizacionales, matriz de asignación de coaches y calendario compartido de actividades de coaching.

**Término SECAV-O asociado:** `secavo:AnnualCoachingPlan` (alcance organizacional)

---

### Preparación de miembro
*Fuente: `coaching-governance/docs/coaching-cycle.md`*

Actividad que ocurre antes del lanzamiento del equipo o al incorporarse un nuevo miembro, en la que el ingeniero recibe: propósito y objetivos del proyecto, modelo de entrega, prácticas de ingeniería, expectativas de calidad, riesgos conocidos, artefactos clave, expectativas de revisiones e inspecciones, prácticas de pruebas, responsabilidades de validación humana en trabajo asistido por IA, y métricas que se recopilarán. Su enfoque es de desarrollo, no de evaluación de idoneidad.

---

### Sprint de coaching
*Fuente: `coaching-governance/docs/coaching-cycle.md`*

Iteración acotada de coaching que: revisa el plan anual, selecciona objetivos de competencia para el sprint, observa actividades de ingeniería y recopila evidencia, aplica intervenciones de coaching, y retrospecciona. La duración no está prescrita; debe ser suficientemente larga para producir evidencia observable y suficientemente corta para permitir replanificación oportuna.

**Término SECAV-O asociado:** `secavo:CoachingSprint`

---

## Métricas y trazabilidad de defectos

### detectionMethod (Método de detección)
*Fuente: `coaching-governance/guides/defect-tracking.md`*

Propiedad de datos de `secavo:DefectObservation` que registra cómo fue encontrado el defecto: inspección formal, revisión de pares, prueba automatizada, prueba manual, reporte de usuario, u otro. Permite calcular la efectividad relativa de cada técnica de detección.

**Término SECAV-O asociado:** `secavo:detectionMethod`

---

### Densidad de defectos por módulo
*Fuente: `coaching-governance/guides/defect-tracking.md`*

Métrica que cuenta el número de defectos registrados por módulo o componente en un período dado. Identifica los componentes de mayor riesgo que deberían ser candidatos prioritarios a inspección formal.

**Término SECAV-O asociado:** `secavo:Metric`, `secavo:DefectObservation`

---

### Efectividad de revisión
*Fuente: `coaching-governance/guides/defect-tracking.md`*

Porcentaje de defectos detectados en actividades de revisión de código o inspección formal respecto al total de defectos registrados en el período. Un valor bajo indica que las revisiones no están capturando defectos antes de que escapen a fases posteriores.

**Término SECAV-O asociado:** `secavo:Metric`, `secavo:ReviewObservation`

---

### phaseDetected (Fase de detección)
*Fuente: `coaching-governance/guides/defect-tracking.md`*

Propiedad de datos de `secavo:DefectObservation` que registra en qué fase del desarrollo fue encontrado el defecto: revisión de código, inspección formal, prueba unitaria, integración, sistema, aceptación, producción. Junto con `phaseInjected` permite calcular el costo relativo de detección tardía.

**Término SECAV-O asociado:** `secavo:phaseDetected`

---

### phaseInjected (Fase de inyección)
*Fuente: `coaching-governance/guides/defect-tracking.md`*

Propiedad de datos de `secavo:DefectObservation` que registra en qué fase del desarrollo fue introducido el defecto: requerimientos, diseño de arquitectura, diseño detallado, codificación, diseño de pruebas unitarias, diseño de pruebas de sistema, diseño de pruebas de aceptación. La distribución de `phaseInjected` a lo largo de los sprints indica qué fases generan más defectos y deben priorizarse para inspección.

**Término SECAV-O asociado:** `secavo:phaseInjected`

---

### Tasa de escape (Escape rate)
*Fuente: `coaching-governance/guides/defect-tracking.md`*

Porcentaje de defectos encontrados en producción o en fases tardías (integración, sistema, aceptación) respecto al total de defectos registrados. Una tasa de escape alta indica que las inspecciones y revisiones de fases tempranas no son efectivas o no están ocurriendo.

**Término SECAV-O asociado:** `secavo:Metric`, `secavo:DefectObservation`

---

## Adopción incremental

### Decisión Go / Pivot / Stop
*Fuente: `coaching-governance/guides/incremental-adoption.md`*

Tres posibles resultados de la evaluación de una iteración piloto del framework:

| Decisión | Condición |
|---|---|
| **Go (Escalar)** | La evidencia es consistente, la cadena completa está documentada, no hay bloqueantes de gobernanza |
| **Pivot (Corregir)** | Se detectó fricción sistemática; se aplica una corrección y se reitera |
| **Stop (Detener)** | Un supuesto fundacional es inválido e incorregible; se documentan los hallazgos para evitar una inversión mayor en algo que no funciona en este contexto |

---

### Fail Fast (Falla rápido)
*Fuente: `coaching-governance/guides/incremental-adoption.md`*

Filosofía de adopción incremental cuyo objetivo es hacer visibles los supuestos incorrectos, cuellos de botella y restricciones técnicas o de gobernanza en la etapa más temprana posible, cuando el costo de corrección es mínimo. Un fallo controlado con datos empíricos es un resultado de aprendizaje exitoso, no un fracaso.

---

### Proof of Concept — PoC
*Fuente: `coaching-governance/guides/incremental-adoption.md`*

Experimento mínimo que responde una sola pregunta: ¿Es esto factible en este contexto? En el contexto del framework: ejecutar una actividad de ingeniería con un coach y un ingeniero antes de lanzar un piloto completo, para verificar si los mecanismos básicos de observación y evidencia funcionan.

---

### Trazador de extremo a extremo (End-to-end tracer)
*Fuente: `coaching-governance/guides/incremental-adoption.md`*

Rebanada vertical delgada pero completa del sistema de coaching: un ciclo completo desde la selección de actividad hasta la recopilación de evidencia, `secav:CompetencyAssessment`, `secav:CoachingIntervention` y `secavo:SprintRetrospective`, antes de ampliar el alcance. Permite verificar que la cadena completa funciona antes de invertir en escalar.

---

## Gestión de riesgos

### Acción correctiva / de contingencia
*Fuente: `coaching-governance/guides/risk-management.md`*

Acción definida de antemano que se ejecuta cuando un riesgo se materializa. Ejemplos: cambiar el objetivo del sprint, agregar un revisor independiente, escalar una dependencia bloqueada, revisar el baseline.

**Término SECAV-O asociado:** `secavo:CorrectiveAction`

---

### Acción preventiva
*Fuente: `coaching-governance/guides/risk-management.md`*

Acción definida de antemano para reducir la probabilidad de que un riesgo ocurra. Ejemplos: clarificar criterios de aceptación, agendar revisiones de pares, proporcionar capacitación, aumentar la frecuencia de inspecciones en módulos de alto riesgo.

**Término SECAV-O asociado:** `secavo:PreventiveAction`