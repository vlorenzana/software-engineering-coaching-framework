# Checklist de Observación del Coach por Actividad de Ingeniería

## Propósito

Este checklist permite al coach registrar, durante cualquier sesión de observación, las conductas positivas y las señales de alerta que el equipo exhibe en cada actividad de ingeniería. Cada fila es un observable: algo que el coach puede ver, escuchar o leer directamente — no una inferencia.

**Convención de columnas:**
- ✓ Conducta positiva — registrar como `secav:Evidence` para la evaluación de competencias
- ⚠ Señal de alerta — considerar `secav:CoachingIntervention`

---

## 1. Definición de Requisitos y Criterios de Aceptación

> Actividad SECAV-O: `secav:RequirementsActivity`, `secav:AcceptanceCriteriaDefinition`

| # | Tipo | Conducta observable | Término SECAV-O |
|---|------|---------------------|-----------------|
| 1.1 | ✓ | El equipo define criterios de aceptación antes de iniciar la codificación (formato Given/When/Then u otro explícito) | `secav:AcceptanceCriteriaDefinition` |
| 1.2 | ✓ | Los criterios de aceptación producen un artefacto documentado (escenario BDD, especificación de prueba, ticket con AC completo) | `secav:AcceptanceCriteriaDefinition` → `secav:produces` → `secav:Artifact` |
| 1.3 | ✓ | Los casos límite y caminos de error están explicitados en los criterios — no solo el happy path | `secav:AcceptanceCriterion` |
| 1.4 | ✓ | El ingeniero puede explicar oralmente el requisito antes de codificar | `secav:WorkProductEvidence` |
| 1.5 | ⚠ | La historia de usuario llega al sprint sin criterios de aceptación definidos | `secav:HappyPathOnlyReview` (riesgo) |
| 1.6 | ⚠ | El equipo comienza a codificar con requisitos ambiguos sin solicitar clarificación | `secav:MissingReviewContext` (precondición) |
| 1.7 | ⚠ | Los criterios de aceptación se escriben después de la implementación (post-hoc) | ausencia de `secav:AcceptanceCriteriaDefinition` como actividad preventiva |
| 1.8 | ⚠ | No existe trazabilidad entre los criterios de aceptación y los casos de prueba automatizados | `secav:QualityCriterion` sin `secav:AutomationGate` |

---

## 2. Diseño y Contratos de API

> Actividad SECAV-O: `secav:DesignActivity`, `secav:APIContractDefinition`

| # | Tipo | Conducta observable | Término SECAV-O |
|---|------|---------------------|-----------------|
| 2.1 | ✓ | El equipo define el contrato de API (esquema, endpoints, respuestas de error) antes de implementar el cliente o el servidor | `secav:APIContractDefinition` |
| 2.2 | ✓ | Existe un artefacto de contrato versionado (OpenAPI, AsyncAPI, Protobuf, o equivalente) | `secav:APIContractArtifact` → `secav:DesignArtifact` |
| 2.3 | ✓ | Los cambios de contrato de API generan una revisión de diseño antes de ser fusionados | `secav:DesignReview` |
| 2.4 | ✓ | El arquitecto ha identificado y documentado los módulos críticos antes del inicio del desarrollo | `secav:SourceCodeArtifact` con criticidad documentada |
| 2.5 | ⚠ | Las decisiones de diseño se toman durante la revisión de código (demasiado tarde) | `secav:LateArchitecturalDiscussion` |
| 2.6 | ⚠ | El contrato de API no está documentado — el cliente infiere el comportamiento por el código del servidor | ausencia de `secav:APIContractArtifact` |
| 2.7 | ⚠ | Los cambios de interfaz se introducen en el PR sin notificación previa a los consumidores | `secav:MissingReviewContext` |
| 2.8 | ⚠ | La lista de módulos críticos no fue comunicada al coach ni al Líder Técnico al inicio del proyecto | ausencia de identificación de riesgo en `secav:DesignActivity` |

---

## 3. Implementación y Estado Cognitivo del Desarrollador

> Actividad SECAV-O: `secav:CodeImplementation`, `secav:DeveloperCognitiveState`

| # | Tipo | Conducta observable | Término SECAV-O |
|---|------|---------------------|-----------------|
| 3.1 | ✓ | El ingeniero realiza una autorrevisión del diff completo antes de abrir el PR | `secav:SelfReview` |
| 3.2 | ✓ | El ingeniero protege bloques de trabajo profundo (sin interrupciones durante la implementación de lógica compleja) | `secav:DeepWorkCondition` |
| 3.3 | ✓ | El ingeniero respeta límites de carga cognitiva — no mezcla múltiples cambios no relacionados en un solo PR | `secav:FatigueManagementCondition` |
| 3.4 | ✓ | El PR tiene un tamaño manejable (la mayoría de los cambios caben en una sesión de revisión de 60 min) | `secav:SelfReviewCondition` |
| 3.5 | ⚠ | El ingeniero muestra signos visibles de fatiga al revisar o codificar (errores básicos repetidos, respuestas lentas) | `secav:FatigueManagementCondition` (ausente) |
| 3.6 | ⚠ | El ingeniero fusiona código sin haber realizado autorrevisión — lo confirma al preguntar | ausencia de `secav:SelfReview` |
| 3.7 | ⚠ | Los PRs llegan sistemáticamente con más de 500 líneas de cambio efectivo | `secav:OversizedPullRequest` |
| 3.8 | ⚠ | El ingeniero trabaja en múltiples funcionalidades en paralelo dentro del mismo sprint sin señales de priorización | `secav:DeepWorkCondition` (comprometida) |

---

## 4. Puertas de Automatización (Pre-commit, Tipado, Cobertura)

> Actividad SECAV-O: `secav:AutomationGate`, `secav:PreCommitHook`, `secav:StrictTypingPolicy`, `secav:CodeCoverageGate`

| # | Tipo | Conducta observable | Término SECAV-O |
|---|------|---------------------|-----------------|
| 4.1 | ✓ | El repositorio tiene hooks de pre-commit activos que bloquean código con errores de estilo o secretos expuestos | `secav:PreCommitHook` |
| 4.2 | ✓ | El tipado estricto está habilitado (TypeScript strict, mypy, etc.) y el equipo lo respeta sin suprimir errores | `secav:StrictTypingPolicy` |
| 4.3 | ✓ | La cobertura de pruebas tiene un umbral definido y el pipeline rechaza PRs que lo reducen | `secav:CodeCoverageGate` con `secav:coverageThreshold` |
| 4.4 | ✓ | Los miembros del equipo pueden explicar qué comprueba cada gate y por qué existe | `secav:criterionStatement` presente y comunicado |
| 4.5 | ⚠ | El equipo desactiva o suprime gates para desbloquear un deploy ("lo arreglamos después") | ausencia efectiva de `secav:AutomationGate` |
| 4.6 | ⚠ | Existen errores de tipado suprimidos con comentarios `// @ts-ignore` o equivalentes sin justificación | `secav:StrictTypingPolicy` (comprometida) |
| 4.7 | ⚠ | La cobertura de pruebas cae sprint a sprint sin que el equipo lo mencione ni lo tome como acción | `secav:CodeCoverageGate` sin seguimiento |
| 4.8 | ⚠ | El equipo desconoce qué comprueba el pipeline de CI — solo saben "si pasa, bien" | `secav:DeterministicAnalysisActivity` sin apropiación del equipo |

---

## 5. Revisión de Código entre Pares

> Actividad SECAV-O: `secav:CodeReview`, `secav:ReviewAntipattern` y subclases

| # | Tipo | Conducta observable | Término SECAV-O |
|---|------|---------------------|-----------------|
| 5.1 | ✓ | El revisor valida la intención del cambio antes de leer el diff (ticket, especificación, o descripción del PR) | `secav:FormalReviewRequest` con `secav:requestDescription` |
| 5.2 | ✓ | Los comentarios de revisión se dirigen al código, no a la persona ("este bloque podría..." vs "tu código es...") | `secav:ReviewerAssertiveClosureCondition` |
| 5.3 | ✓ | El revisor distingue entre observaciones bloqueantes y sugerencias opcionales | `secav:ReviewFinding` con severidad documentada |
| 5.4 | ✓ | El revisor llega descansado y con el material leído cuando la sesión fue programada con anticipación | `secav:ReviewerEnergyCondition`, `secav:ReviewerFocusCondition` |
| 5.5 | ✓ | El equipo cierra los hilos de comentarios explícitamente — no deja conversaciones abiertas indefinidamente | ausencia de `secav:InfiniteCommentLoop` |
| 5.6 | ✓ | Los PRs incluyen descripción clara de qué cambió, por qué, y cómo probarlo | `secav:requestDescription` |
| 5.7 | ⚠ | El revisor aprueba el PR sin comentarios en menos de 2 minutos (revisión de sello de goma) | `secav:RubberStampApproval` |
| 5.8 | ⚠ | La revisión dura más de 90 minutos sin pausas — el revisor pierde concentración visible | `secav:OversizedReviewSession` |
| 5.9 | ⚠ | El PR llega sin descripción o con descripción genérica ("fixes bug") | `secav:MissingReviewContext` |
| 5.10 | ⚠ | El código llega en estado borrador (WIP) marcado como listo para revisión | `secav:PrematureReviewRequest` |
| 5.11 | ⚠ | Los revisores señalan violaciones de estilo que deberían capturarse en el linter | `secav:ManualStyleReview` |
| 5.12 | ⚠ | Un solo revisor aprueba consistentemente todos los PRs del equipo | `secav:SingleApproverBottleneck` |
| 5.13 | ⚠ | Hay hilos de revisión que llevan más de 3 sprints sin resolverse | `secav:InfiniteCommentLoop` |
| 5.14 | ⚠ | Los comentarios son punitivos o despectivos — "esto es un desastre", "¿cómo pensaste esto?" | `secav:PunitiveReviewApproach` |
| 5.15 | ⚠ | Un revisor dicta la solución en lugar de señalar el problema y dejar la decisión al autor | `secav:ReviewerDictatorship` |
| 5.16 | ⚠ | La revisión valida solo el happy path — ningún caso límite ni de error fue cuestionado | `secav:HappyPathOnlyReview` |

---

## 6. Inspecciones Formales de Módulos Críticos

> Actividad SECAV-O: `secav:CodeReview` (inspección), `secav:HumanValidationActivity`

| # | Tipo | Conducta observable | Término SECAV-O |
|---|------|---------------------|-----------------|
| 6.1 | ✓ | El material de la inspección se distribuyó al menos 24–48 h antes de la reunión | `secav:ReviewerReadiness` |
| 6.2 | ✓ | Todos los participantes llegaron a la reunión con observaciones documentadas (preparación individual realizada) | `secav:ReviewerCriticalAnalysisCondition` |
| 6.3 | ✓ | El moderador mantiene el foco en el artefacto — no en el autor ni en soluciones | `secav:ReviewFinding` producido sin personalismos |
| 6.4 | ✓ | El autor escucha y responde sin defender — no debate durante la reunión | `secav:WorkProductEvidence` (actitud observable) |
| 6.5 | ✓ | El recorder documenta hallazgos con tipo y severidad durante la reunión | `secav:ReviewFinding` con registro formal |
| 6.6 | ✓ | El coach verifica el rework de hallazgos críticos antes de que el módulo avance | `secav:ReviewRecord` actualizado |
| 6.7 | ⚠ | Algún participante no preparó el material — la inspección se convierte en lectura en vivo | ausencia de `secav:ReviewerReadiness` |
| 6.8 | ⚠ | La reunión de inspección fue cancelada o reducida sin justificación técnica | `secavo:QualityPlanningConcern` |
| 6.9 | ⚠ | El autor defiende o argumenta sus decisiones durante la reunión en lugar de escuchar | `secav:PunitiveReviewApproach` (dinámica inversa) |
| 6.10 | ⚠ | La inspección no produjo un `secav:ReviewRecord` documentado | ausencia de `secav:ReviewRecord` |
| 6.11 | ⚠ | El mismo tipo de defecto aparece en múltiples módulos inspeccionados (patrón sistémico) | `secav:CoachingIntervention` → `secavo:ImprovementAction` |
| 6.12 | ⚠ | La gerencia usa los hallazgos de la inspección para evaluar el rendimiento del autor de forma punitiva | `secavo:QualityPlanningConcern` |

---

## 7. Pruebas y Diseño de Pruebas Unitarias

> Actividad SECAV-O: `secav:TestingActivity`

| # | Tipo | Conducta observable | Término SECAV-O |
|---|------|---------------------|-----------------|
| 7.1 | ✓ | Las pruebas tienen nombres que describen comportamiento, no implementación ("should return 404 when user not found") | `secav:WorkProductEvidence` |
| 7.2 | ✓ | Cada prueba tiene un único punto de fallo identificable (principio FIRST: Independent) | `secav:QualityCriterion` |
| 7.3 | ✓ | Las pruebas cubren caminos de error y valores límite, no solo el flujo exitoso | `secav:HappyPathOnlyReview` ausente |
| 7.4 | ✓ | Las pruebas se ejecutan en milisegundos — sin dependencias de red o filesystem en pruebas unitarias | `secav:QualityCriterion` (FIRST: Fast) |
| 7.5 | ✓ | El equipo sabe el umbral de cobertura del proyecto y puede justificarlo | `secav:CodeCoverageGate` con `secav:coverageThreshold` conocido |
| 7.6 | ⚠ | Las pruebas solo validan el happy path — no hay pruebas de valores nulos, vacíos o fuera de rango | `secav:HappyPathOnlyReview` |
| 7.7 | ⚠ | Las pruebas unitarias tienen dependencias externas (base de datos, API, reloj del sistema sin inyección) | `secav:QualityCriterion` (FIRST: Fast violado) |
| 7.8 | ⚠ | Múltiples pruebas fallan cuando falla una sola condición — alto acoplamiento entre tests | `secav:QualityCriterion` (FIRST: Independent violado) |
| 7.9 | ⚠ | El equipo aumenta la cobertura con pruebas triviales para pasar el gate, sin evaluar casos reales | `secav:CodeCoverageGate` comprometido en calidad |
| 7.10 | ⚠ | Los PR no incluyen pruebas para la lógica nueva (solo código de producción) | ausencia de `secav:TestingActivity` asociada |

---

## 8. Revisión de Código Asistida por IA

> Actividad SECAV-O: `secav:AIAssistedActivity`, `secav:HumanValidationActivity`, `secav:AIReviewPromptConfiguration`

| # | Tipo | Conducta observable | Término SECAV-O |
|---|------|---------------------|-----------------|
| 8.1 | ✓ | El pipeline de revisión aplica herramientas deterministas (linter, scanner estático) antes de la revisión humana | `secav:DeterministicAnalysisActivity` → `secav:precedes` → revisión humana |
| 8.2 | ✓ | El equipo configura el tool de IA con contexto del proyecto (framework, versión, convenciones de seguridad) | `secav:AIReviewPromptConfiguration` con `secav:hasContextDefinition` |
| 8.3 | ✓ | La configuración incluye análisis de impacto, evaluación de seguridad y generación de casos de prueba | `secav:hasImpactAnalysisInstruction`, `secav:hasSecurityEvaluationInstruction`, `secav:hasTestGenerationInstruction` |
| 8.4 | ✓ | Los revisores auditan las sugerencias de IA antes de aplicarlas — verifican que los métodos existen en la versión en uso | `secav:HumanValidationActivity` activa |
| 8.5 | ✓ | Los PRs de código generado por IA son clasificados por riesgo antes de enrutarse (rutinario / atención / crítico) | `secav:ReviewRiskLevel` |
| 8.6 | ✓ | El equipo monitorea falsos negativos — PRs de alto riesgo que pasaron como rutinarios | `secav:ReviewObservation` |
| 8.7 | ⚠ | El equipo acepta sugerencias de la IA sin revisión crítica — no verifica que los métodos propuestos existan | `secav:InsufficientAICodeScrutiny` |
| 8.8 | ⚠ | La IA es usada para aprobar o bloquear cambios de forma autónoma, sin revisión humana | violación de `secav:requiresHumanValidation` |
| 8.9 | ⚠ | Los falsos positivos del tool de IA son altos y el equipo los ignora en lugar de ajustar la configuración | `secav:ReviewObservation` (alerta fatiga) |
| 8.10 | ⚠ | El código generado por IA llega sin el historial de decisiones que explica el diseño | `secav:MissingReviewContext` |
| 8.11 | ⚠ | Los módulos críticos con código generado por IA no reciben inspección formal adicional | ausencia de `secav:HumanValidationActivity` para `secav:AIAssistedActivity` en módulo crítico |
| 8.12 | ⚠ | El equipo no cuestiona el código de IA porque "compila y los tests pasan" | `secav:RubberStampApproval` aplicado a código IA |

---

## 9. Adopción Organizacional del Nuevo Modelo de Trabajo

> Actividad SECAV-O: `secav:AdoptionBehavior` y sus siete subclases, agrupadas por `secav:AdoptionPillar`
>
> **Contexto:** Este grupo observa si los líderes, equipos e individuos han internalizado el nuevo modelo de trabajo en sus comportamientos cotidianos. No es supervisión individual — es una señal colectiva de adopción cultural. El facilitador del cambio (`secav:ChangeAgent`) es quien activa intervenciones cuando aparecen señales de alerta sistémicas.
>
> **Frecuencia recomendada:** evaluación quincenal o mensual. Usar observación directa en rituales + pulso eNPS (`secav:PulseSurveyMeasurement`, `secav:DirectRitualObservation`).

### Pilar 1 — Liderazgo y Modelado (Líderes / PMs)

| # | Tipo | Conducta observable | Término SECAV-O |
|---|------|---------------------|-----------------|
| 9.1 | ✓ | Los líderes y PMs usan las nuevas herramientas digitales como canal principal de comunicación — no el correo tradicional | `secav:LeaderDigitalToolAdoption` |
| 9.2 | ✓ | Los líderes reconocen públicamente (en reuniones o canales institucionales) a colaboradores que aplican las nuevas conductas y metodologías | `secav:PublicRecognitionOfNewBehaviors` |
| 9.3 | ⚠ | Los líderes continúan usando el correo electrónico como canal principal, manteniendo ambigüedad de proceso dual | ausencia de `secav:LeaderDigitalToolAdoption` |
| 9.4 | ⚠ | Los reconocimientos públicos señalan errores o incumplimientos — los comportamientos nuevos nunca se celebran | ausencia de `secav:PublicRecognitionOfNewBehaviors` |

### Pilar 2 — Colaboración Eficiente (Equipos)

| # | Tipo | Conducta observable | Término SECAV-O |
|---|------|---------------------|-----------------|
| 9.5 | ✓ | El equipo mantiene la documentación del proyecto centralizada y actualizada en plataformas compartidas (repositorio único por proyecto) | `secav:CentralizedDocumentationPractice` |
| 9.6 | ✓ | El equipo reemplaza reuniones largas de seguimiento por sincronizaciones breves centradas en bloqueantes | `secav:FocusedSynchronizationPractice` |
| 9.7 | ⚠ | La documentación existe en silos — archivos locales, hilos de correo, chats privados — sin acceso centralizado | ausencia de `secav:CentralizedDocumentationPractice` |
| 9.8 | ⚠ | Las reuniones de seguimiento semanales continúan con el mismo formato largo sin transición hacia syncs cortos orientados a bloqueantes | ausencia de `secav:FocusedSynchronizationPractice` |

### Pilar 3 — Comunicación Abierta (Equipos)

| # | Tipo | Conducta observable | Término SECAV-O |
|---|------|---------------------|-----------------|
| 9.9 | ✓ | Los miembros del equipo expresan dudas, errores y bloqueantes de forma temprana y transparente — los registros de riesgos e impedimentos se actualizan pronto | `secav:EarlyTransparentCommunication` |
| 9.10 | ⚠ | Los miembros retienen dudas o errores hasta que escalan — los problemas emergen tarde, en producción o en la retrospectiva | ausencia de `secav:EarlyTransparentCommunication` |

### Pilar 4 — Adaptabilidad Continuada (Todos)

| # | Tipo | Conducta observable | Término SECAV-O |
|---|------|---------------------|-----------------|
| 9.11 | ✓ | Los miembros aplican guías y materiales de capacitación de forma autónoma antes de escalar consultas básicas | `secav:AutonomousGuideApplication` |
| 9.12 | ⚠ | Los miembros escalan consultas básicas sin consultar primero las guías o materiales disponibles, generando sobrecarga de soporte | ausencia de `secav:AutonomousGuideApplication` |

### Pilar 5 — Feedback e Innovación (Todos)

| # | Tipo | Conducta observable | Término SECAV-O |
|---|------|---------------------|-----------------|
| 9.13 | ✓ | Los miembros contribuyen propuestas constructivas sobre el nuevo modelo en las sesiones de retrospectiva — las propuestas se implementan | `secav:ConstructiveRetrospectiveFeedback` |
| 9.14 | ⚠ | Las retrospectivas no producen propuestas de ajuste del equipo — el formato es declarativo o de queja sin acción | ausencia de `secav:ConstructiveRetrospectiveFeedback` |

---

## 10. Conductas de Liderazgo Técnico (Engineering Managers y Tech Leads)

> Actividad SECAV-O: `secav:LeaderBehavior` y subclases, agrupadas por `secav:TechnicalLeadershipDimension`
>
> **Contexto:** Este grupo observa los comportamientos del líder técnico (Engineering Manager o Tech Lead) en sus tres dimensiones estratégicas: personas, arquitectura y estrategia. No evalúa la habilidad técnica individual, sino la capacidad de multiplicar el talento colectivo y alinear las soluciones con los objetivos del negocio.
>
> **Frecuencia recomendada:** mensual o por sprint, con revisión trimestral de los cuatro indicadores de evaluación (10.12–10.15).

### Dimensión 1 — Personas y Mentoría (35% del peso del liderazgo)

| # | Tipo | Conducta observable | Término SECAV-O |
|---|------|---------------------|-----------------|
| 10.1 | ✓ | El líder realiza sesiones 1-on-1 con cadencia regular y foco en el crecimiento profesional — no solo en el status del sprint | `secav:ActiveMentorship` |
| 10.2 | ✓ | Los post-mortems de producción terminan con acciones de proceso o herramienta — nunca señalando a individuos | `secav:PsychologicalSafetyPromotion` |
| 10.3 | ✓ | El líder define el "qué" y el "por qué" del cambio, pero otorga al equipo autonomía para decidir el "cómo" | `secav:EffectiveDelegation` |
| 10.4 | ✓ | El líder entrega feedback constructivo al equipo en tiempo real y reconoce públicamente el trabajo bien hecho | `secav:ContinuousFeedbackBehavior` |
| 10.5 | ⚠ | El líder revisa y aprueba cada decisión técnica menor — los ingenieros esperan instrucciones en lugar de tomar iniciativa | ausencia de `secav:EffectiveDelegation` (micromanagement) |
| 10.6 | ⚠ | Los post-mortems terminan en señalamiento de individuos o en silencio — no se producen acciones de mejora | ausencia de `secav:PsychologicalSafetyPromotion` |
| 10.7 | ⚠ | No existe cadencia de 1-on-1 — la interacción del líder con los ingenieros ocurre solo en reuniones grupales o cuando hay problemas | ausencia de `secav:ActiveMentorship` |

### Dimensión 2 — Arquitectura y Código (30% del peso del liderazgo)

| # | Tipo | Conducta observable | Término SECAV-O |
|---|------|---------------------|-----------------|
| 10.8 | ✓ | Las decisiones de arquitectura significativas están documentadas en ADRs accesibles a todo el equipo | `secav:ArchitectureDecisionDocumentation` |
| 10.9 | ✓ | El equipo destina entre 15–20% del esfuerzo del sprint a salud de código (deuda técnica, refactoring, mantenimiento) — negociado con Product | `secav:TechnicalDebtNegotiation` |
| 10.10 | ⚠ | Las decisiones de arquitectura se toman de forma informal o en conversaciones efímeras — no quedan registradas ni son revisables | ausencia de `secav:ArchitectureDecisionDocumentation` |
| 10.11 | ⚠ | La deuda técnica nunca se presenta a Product como trabajo prioritario — se acumula sprint tras sprint sin negociación | ausencia de `secav:TechnicalDebtNegotiation` |

### Dimensión 3 — Estrategia e Impacto (35% del peso del liderazgo)

| # | Tipo | Conducta observable | Término SECAV-O |
|---|------|---------------------|-----------------|
| 10.12 | ✓ | El líder actúa como filtro frente a interrupciones externas — los ingenieros tienen bloques de trabajo profundo protegidos | `secav:TeamShielding` |
| 10.13 | ✓ | Los despliegues tienen ritmos sostenibles — no hay rush de último momento que comprometa la estabilidad técnica | `secav:DeliveryConsistencyBehavior` |
| 10.14 | ✓ | El líder comprende las métricas de negocio que el equipo impacta con su código | `secav:HolisticProductVisionBehavior` |
| 10.15 | ✓ | El líder integra perspectivas técnicas diversas en las decisiones — los ingenieros junior y senior contribuyen en igualdad de condiciones | `secav:TechnicalDiversityBehavior` |
| 10.16 | ⚠ | Los ingenieros reciben interrupciones directas de stakeholders y cambian de contexto constantemente — el líder no actúa como filtro | ausencia de `secav:TeamShielding` |
| 10.17 | ⚠ | El líder favorece sistemáticamente una perspectiva técnica sin abrir espacio a otras voces del equipo | ausencia de `secav:TechnicalDiversityBehavior` |

---

## Resumen de uso del checklist

| Cuándo usar cada grupo | Actividad / Sprint |
|---|---|
| Grupos 1–2 | Inicio de sprint, refinement, sesiones de diseño |
| Grupo 3 | Cualquier sesión de trabajo — observación en contexto |
| Grupo 4 | Revisión de pipeline CI/CD; onboarding de nuevos miembros |
| Grupos 5–6 | Durante o inmediatamente después de sesiones de revisión / inspección |
| Grupo 7 | Revisión de PR con cambios de pruebas; revisión de cobertura sprint |
| Grupo 8 | PRs con código asistido por IA; configuración de herramientas IA del equipo |
| Grupo 9 | Quincenalmente o mensualmente — evaluación de adopción cultural del nuevo modelo de trabajo |
| Grupo 10 | Mensualmente o por sprint — observación del líder técnico; revisión trimestral de indicadores 10.12–10.15 |

Las señales ✓ se registran como `secav:WorkProductEvidence` o `secav:ReviewFinding` y alimentan la `secav:CompetencyAssessment` del ciclo.

Las señales ⚠ que aparecen más de una vez en el sprint deben escalar a `secav:CoachingIntervention`. Si aparecen en múltiples miembros del equipo, documentar una `secavo:ImprovementAction` en la retrospectiva.

Para el Grupo 9, las señales ⚠ sistémicas (presentes en más de la mitad del equipo en dos evaluaciones consecutivas) deben derivar en una intervención del `secav:ChangeAgent` responsable — no solo del coach técnico.

---

## Documentos relacionados

| Documento | Relación |
|---|---|
| `coaching-governance/guides/coach-attitudes.md` | Actitudes del coach durante la observación |
| `coaching-governance/guides/peer-review-antipatterns.md` | Detalle de antipatrones de revisión (grupos 5 y 8) |
| `coaching-governance/guides/shift-left-prevention.md` | Contexto de los grupos 1–4 (prevención shift-left) |
| `coaching-governance/guides/formal-inspections.md` | Protocolo completo del grupo 6 |
| `coaching-governance/guides/ai-assisted-code-review.md` | Contexto completo del grupo 8 |
| `templates/rca-defect-analysis.md` | Cuando una señal ⚠ deriva en un defecto P1/P2 |
| `templates/engineer-coaching-assessment.md` | Las evidencias ✓ alimentan la evaluación de competencias |