# Criterio Mínimo de Calidad por Fase

## Principio

En cada fase productiva del desarrollo de software se generan artefactos que condicionan la calidad de todas las fases siguientes. Un defecto introducido en requerimientos que no se detecta hasta pruebas de sistema puede invalidar semanas de trabajo. Un diseño de pruebas unitarias defectuoso puede pasar inadvertido indefinidamente si nadie lo inspecciona.

**El criterio de calidad mínima razonable es: los artefactos críticos de cada fase deben ser inspeccionados antes de que esa fase concluya.**

---

## Definición: calidad mínima razonable

La **calidad mínima razonable** es el umbral por debajo del cual una organización incurre en mala práctica de ingeniería — independientemente de las restricciones de tiempo o presupuesto que se invoquen para justificarlo. No es el estándar de calidad al que aspirar, sino el piso por debajo del cual el riesgo de fallo sistémico es inaceptable.

La razón de establecer un *mínimo* en lugar de un *óptimo* es que la mayoría de las organizaciones no tienen capacidad para inspeccionar todos los productos de software que genera el desarrollo: requerimientos, diseño de arquitectura, diseño detallado, código, diseño de pruebas unitarias, diseño de pruebas de sistema, diseño de pruebas de aceptación, resultados de ejecución de pruebas, y otros derivados. Inspeccionar todo es un ideal al que conviene aproximarse progresivamente; presuponer que toda organización puede lograrlo desde el inicio es irreal.

Lo que sí es alcanzable en la mayoría de los proyectos — y lo que este framework establece como mínimo razonable — es **identificar los artefactos de mayor riesgo en cada fase y asegurar que al menos esos sean revisados formalmente por más de un revisor antes de avanzar a la siguiente fase**.

| Nivel | Descripción |
|---|---|
| **Por debajo del mínimo** | Mala práctica: ningún artefacto crítico de alguna fase es inspeccionado formalmente. Los defectos se acumulan entre fases y se detectan tarde, cuando su costo de corrección es máximo. |
| **Calidad mínima razonable** | Los artefactos de mayor riesgo de cada fase son inspeccionados por más de un revisor antes de avanzar. Es el piso del framework. |
| **Calidad aspiracional** | La mayoría o todos los artefactos de cada fase son inspeccionados. Las organizaciones maduran hacia este nivel de forma incremental (`coaching-governance/guides/incremental-adoption.md`). |

Un segundo criterio que refuerza este mínimo: si la presión de tiempo lleva sistemáticamente a omitir inspecciones en alguna fase — cualquier fase — eso es una señal de que el plan de proyecto subestima el esfuerzo de calidad, no de que la inspección sea prescindible. El coach documenta estas omisiones como `secavo:QualityPlanningConcern`.

---

## Modelo de fases e inspecciones

La siguiente tabla mapea las fases productivas del desarrollo de software, los artefactos que producen, el tipo de revisión en SECAV-O, y la guía del framework que establece el protocolo.

| Fase | Artefacto inspeccionado | Actividad SECAV-O | Tipo de revisión | Guía del framework |
|---|---|---|---|---|
| **Requerimientos** | Documento de requerimientos, historias de usuario, casos de uso | `secav:RequirementsActivity` | `secav:DesignReview` sobre `secav:DesignArtifact` | `coaching-governance/guides/requirements-inspection.md` |
| **Diseño de arquitectura** | Decisiones arquitectónicas, diagramas de componentes, ADRs | `secav:ApplicationDesign` | `secav:DesignReview` sobre `secav:DesignArtifact` | `coaching-governance/guides/formal-inspections.md` |
| **Diseño detallado** | Diagramas de clases, contratos de API, especificaciones de módulo | `secav:DesignActivity` | `secav:DesignReview` sobre `secav:DesignArtifact` | `coaching-governance/guides/formal-inspections.md` |
| **Implementación de código** | Código fuente de módulos críticos | `secav:CodingActivity` | `secav:CodeReview` sobre `secav:SourceCodeArtifact` | `coaching-governance/guides/formal-inspections.md`, `coaching-governance/guides/peer-review-sessions.md` |
| **Diseño de pruebas unitarias** | Código y casos de prueba unitaria | `secav:UnitTestDesign` | `secav:UnitTestDesignReview` sobre `secav:UnitTestDesignArtifact` | `coaching-governance/guides/unit-test-review.md` |
| **Diseño de pruebas de sistema** | Plan de pruebas de sistema, casos de prueba de integración | `secav:TestingActivity` | `secav:DesignReview` sobre `secav:DesignArtifact` | *(pendiente — ver §3)* |
| **Diseño de pruebas de aceptación** | Criterios de aceptación, scripts de UAT | `secav:TestingActivity` | `secav:DesignReview` sobre `secav:DesignArtifact` | *(pendiente — ver §3)* |

---

## 1. Criterios para seleccionar qué inspeccionar

No todos los artefactos de cada fase merecen inspección formal. El criterio de selección es el mismo en todas las fases: riesgo. Un artefacto es candidato a inspección formal si cumple al menos uno de estos criterios:

| Criterio | Ejemplos |
|---|---|
| **Alcance de impacto** | El artefacto afecta a muchas funcionalidades o a muchos otros artefactos que dependen de él |
| **Amplitud de uso** | Muchos ingenieros o módulos lo consultan como referencia |
| **Complejidad estructural** | Alta ciclomática, lógica condicional anidada, múltiples casos de borde |
| **Riesgo de seguridad o privacidad** | Maneja autenticación, autorización, datos personales, criptografía |
| **Integridad de datos** | Afecta persistencia, consistencia transaccional o integridad referencial |
| **Novedad tecnológica** | Usa una tecnología, patrón o dependencia con la que el equipo tiene poca experiencia |

El arquitecto identifica los artefactos críticos para cada fase al inicio del sprint o al inicio del proyecto. La lista debe ser visible y acordada con el Líder Técnico.

---

## 2. El coach en el modelo de fases

El rol del coach es consistente en todas las fases: **observador silencioso** durante la sesión de inspección, con retroalimentación posterior al equipo, al individuo o a la organización.

Lo que varía según la fase:

- **Requerimientos:** el coach presta atención especial a si los revisores comparan interpretaciones independientes, ya que la ambigüedad solo es visible cuando dos revisores llegan a interpretaciones distintas.
- **Diseño y arquitectura:** el coach observa si los revisores validan el diseño contra los criterios de aceptación del requerimiento que lo originó.
- **Código:** el coach observa si la revisión cubre tanto la corrección funcional como los criterios de calidad no funcionales (seguridad, rendimiento, mantenibilidad).
- **Diseño de pruebas unitarias:** el coach observa si los revisores evalúan los *casos* de prueba (qué se prueba) además de la *implementación* de las pruebas (cómo se prueba).
- **Diseño de pruebas de sistema y aceptación:** el coach observa si los casos de prueba cubren los criterios de aceptación del requerimiento original y los casos de borde relevantes.

En todos los casos, el coach registra sus observaciones como `secav:WorkProductEvidence` y las usa para alimentar la `secav:CompetencyAssessment` de los participantes después de la sesión.

---

## 3. Fases sin guía específica aún

El framework actualmente no tiene guías dedicadas para:

- **Diseño de pruebas de sistema** — planes de prueba que cubren integración entre módulos, interfaces externas y requisitos no funcionales.
- **Diseño de pruebas de aceptación** — criterios de aceptación ejecutables, scripts de UAT, definición de "Done" verificable por el cliente.

En ausencia de guía específica, estas fases se rigen por el protocolo general de inspección formal (`coaching-governance/guides/formal-inspections.md`), adaptando el objeto inspeccionado del artefacto de código al artefacto de diseño de pruebas.

---

## 4. Criterio de avance entre fases

Un artefacto no debería avanzar a la siguiente fase si no ha pasado su inspección de calidad mínima. Esto no requiere que todos los hallazgos estén corregidos antes de avanzar — sí requiere que:

1. Los hallazgos estén documentados en el `secav:ReviewRecord`.
2. Los hallazgos críticos o bloqueantes estén asignados con responsable y plazo.
3. El coach verifique en el seguimiento (Fase 5 de la inspección) que los hallazgos bloqueantes fueron resueltos.

La presión de tiempo que lleva a omitir inspecciones es la causa más frecuente de acumulación de deuda técnica y de defectos de fase tardía. El coach documenta las omisiones como `secavo:QualityPlanningConcern` y las escala si el patrón es recurrente.

---

## 5. Integración con SECAV-O

| Concepto | Término SECAV-O |
|---|---|
| Fase de requerimientos | `secav:RequirementsActivity` |
| Fase de diseño (arquitectura, detalle, pruebas) | `secav:DesignActivity`, `secav:ApplicationDesign`, `secav:UnitTestDesign` |
| Fase de implementación de código | `secav:CodingActivity`, `secav:CodeImplementation` |
| Fase de pruebas (sistema, aceptación) | `secav:TestingActivity` |
| Artefacto de diseño o requerimiento | `secav:DesignArtifact` |
| Artefacto de código | `secav:SourceCodeArtifact` |
| Artefacto de prueba unitaria | `secav:UnitTestDesignArtifact` |
| Revisión de diseño (requerimientos, arquitectura, pruebas de sistema/aceptación) | `secav:DesignReview` |
| Revisión de código | `secav:CodeReview` |
| Revisión de prueba unitaria | `secav:UnitTestDesignReview` |
| Criterios de selección de artefactos críticos | `secav:QualityCriterion` |
| Criterio de avance entre fases | `secav:AcceptanceCriterion` |
| Hallazgo de la inspección | `secav:ReviewFinding` |
| Registro de la inspección | `secav:ReviewRecord` |
| Notas del coach | `secav:WorkProductEvidence` |
| Omisión de inspección documentada | `secavo:QualityPlanningConcern` |
| Evaluación de competencia derivada | `secav:CompetencyAssessment` |

---

## 6. Documentos relacionados

| Documento | Relación |
|---|---|
| `coaching-governance/guides/requirements-inspection.md` | Protocolo de inspección para la fase de requerimientos |
| `coaching-governance/guides/formal-inspections.md` | Protocolo base de inspección formal — aplicable a diseño, arquitectura y código |
| `coaching-governance/guides/peer-review-sessions.md` | Revisiones de pares — complemento de las inspecciones formales en fase de código |
| `coaching-governance/guides/unit-test-review.md` | Protocolo de revisión para la fase de diseño de pruebas unitarias |
| `coaching-governance/guides/defect-tracking.md` | Los defectos encontrados en cada fase se registran con `phaseInjected` correspondiente |
| `coaching-governance/guides/project-kickoff-alignment.md` | La cobertura de inspecciones por fase debe incluirse en los objetivos de calidad del proyecto |
| `coaching-governance/docs/metrics-model.md` | Métricas de defectos por fase — distribución de `phaseInjected` como indicador de cobertura de inspecciones |