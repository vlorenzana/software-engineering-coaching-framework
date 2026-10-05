# Estándares de Documentación de Diseño

## Propósito

Esta guía establece qué artefactos de diseño son obligatorios en función de las características del sistema, y qué criterios de calidad aplican a cada uno. Los artefactos listados aquí son verificados durante las inspecciones formales de diseño (`secav:DesignReview`) como `secav:QualityCriterion` aplicados al `secav:DesignArtifact`.

La ausencia de un artefacto obligatorio — cuando el sistema tiene las características que lo requieren — es un `secav:ReviewFinding` que debe resolverse antes de que el diseño avance a implementación.

---

## 1. Diagramas de estados

### 1.1 Cuándo son obligatorios

Un diagrama de estados es obligatorio para cualquier entidad del sistema — clase, módulo, proceso, recurso externo, o flujo de negocio — que pueda encontrarse en más de un estado distinguible y cuyo comportamiento varíe según el estado en el que se encuentre.

Señales de que se necesita un diagrama de estados:
- El código contiene enumeraciones o constantes que representan estados: `PENDING`, `ACTIVE`, `SUSPENDED`, `CLOSED`, `PROCESSING`, etc.
- La lógica de negocio incluye condiciones del tipo "si el recurso está en estado X, entonces...".
- Una operación es válida en algunos estados del objeto pero no en otros.
- Existe un ciclo de vida del recurso con inicio y fin definidos.

### 1.2 Qué debe contener

Un diagrama de estados completo y útil para los desarrolladores incluye:

| Elemento | Descripción | Señal de omisión |
|---|---|---|
| **Estado inicial** | El estado en el que se encuentra el objeto al ser creado. Marcado visualmente con el símbolo estándar (círculo relleno → flecha). | Si no hay estado inicial explícito, los desarrolladores asumen distintos puntos de partida. |
| **Estados finales** | Los estados en los que el objeto deja de existir o ya no puede transicionar. Marcado visualmente (círculo relleno dentro de círculo vacío). | Si no hay estados finales, no queda claro cuándo el ciclo de vida concluye. |
| **Todos los estados posibles** | Cada estado distinguible que el objeto puede ocupar. | Estados implícitos en el código que no aparecen en el diagrama generan comportamientos no documentados. |
| **Transiciones** | Aristas dirigidas entre estados, etiquetadas con el evento o condición que las dispara. | Transiciones sin etiqueta son ambiguas: los desarrolladores no saben qué las activa. |
| **Condiciones de guarda** | Condiciones adicionales que deben cumplirse para que una transición ocurra (`[condición]`). | Sin guardas, los desarrolladores no saben cuándo una transición está disponible y cuándo no. |
| **Acciones de transición** | Lo que hace el sistema al ejecutar la transición (`/ acción`), si aplica. | Acciones implícitas en el código que no aparecen en el diagrama crean divergencia entre diseño e implementación. |

### 1.3 Criterios de calidad del diagrama (verificados en inspección)

Los inspectores verifican estos criterios (`secav:QualityCriterion`) durante la revisión del diseño:

| Criterio | Pregunta |
|---|---|
| **Completo** | ¿Están todos los estados que aparecen en el código o en la lógica de negocio? |
| **Estado inicial explícito** | ¿Hay exactamente un estado inicial marcado? |
| **Estados finales explícitos** | ¿Están marcados todos los estados en los que el ciclo de vida concluye? |
| **Transiciones etiquetadas** | ¿Todas las transiciones tienen etiqueta de evento o condición? |
| **Sin transiciones implícitas** | ¿Puede un desarrollador determinar, solo con el diagrama, qué estado sigue dado un evento? |
| **Consistente con el código** | ¿El diagrama refleja el comportamiento real del sistema, no el comportamiento deseado original? |

Un diagrama de estados que falla alguno de estos criterios es un `secav:ReviewFinding`. Un diagrama de estados ausente cuando el sistema tiene estados es un `secav:ReviewFinding` bloqueante para avanzar a implementación.

### 1.4 Por qué es obligatorio y no opcional

Un diagrama de estados sirve a los desarrolladores de formas que el código no puede reemplazar:

- **Visibilidad global:** el código muestra cómo se implementa cada transición individualmente; el diagrama muestra todas las transiciones del ciclo de vida simultáneamente.
- **Detección de estados trampa:** estados de los que no hay salida, o de los que solo hay salida hacia estados finales no intencionados, son visibles en el diagrama pero invisibles en el código hasta que ocurren.
- **Detección de transiciones faltantes:** si un evento puede ocurrir en un estado y el diagrama no tiene transición para ese par (estado, evento), el comportamiento está indefinido — y eso es un defecto de diseño.
- **Referencia durante mantenimiento:** cuando un desarrollador modifica el sistema meses después, el diagrama es la única forma de entender el ciclo de vida completo sin leer todo el código.

---

## 2. Rol del coach en la revisión de documentación de diseño

El coach asiste como observador silencioso durante la inspección de artefactos de diseño. Observa específicamente:

- Si los inspectores verifican la presencia de los artefactos obligatorios antes de revisar su contenido.
- Si los inspectores distinguen entre "el diagrama existe" y "el diagrama es correcto y completo".
- Si los hallazgos de ausencia o incompletitud de diagramas se registran con suficiente detalle para que el diseñador pueda corregirlos sin nueva reunión.

El coach registra como `secavo:QualityPlanningConcern` si la falta sistemática de diagramas de estados en los diseños revisados indica ausencia de un estándar de documentación acordado en el equipo.

---

## 3. Integración con SECAV-O

| Concepto | Término SECAV-O |
|---|---|
| Diagrama de estados como artefacto de diseño | `secav:DesignArtifact` |
| Revisión del diagrama | `secav:DesignReview` |
| Criterios de calidad del diagrama | `secav:QualityCriterion` |
| Ausencia del diagrama o diagrama incompleto | `secav:ReviewFinding` |
| Registro de la revisión | `secav:ReviewRecord` |
| Patrón sistémico de ausencia de diagramas | `secavo:QualityPlanningConcern` |
| Competencia desarrollada al producir diagramas completos | `secav:DesignCompetency` |
| Evaluación de competencia derivada de la revisión | `secav:CompetencyAssessment` sobre `secav:DesignCompetency` |

---

## 4. Documentos relacionados

| Documento | Relación |
|---|---|
| `coaching-governance/guides/formal-inspections.md` | Protocolo de inspección que aplica a los artefactos de diseño documentados aquí |
| `coaching-governance/guides/minimum-quality-criteria.md` | La fase de diseño de arquitectura y detalle requiere inspección de sus artefactos críticos |
| `coaching-governance/guides/requirements-inspection.md` | El glosario primario del documento de requerimientos debe definir los estados del dominio antes de que aparezcan en el diagrama de diseño |
| `coaching-governance/glossary/glossary.md` | Definiciones de módulo crítico, inspección formal, QualityPlanningConcern |