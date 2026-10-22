# Acciones Preventivas en el Desarrollo de Software: Guía Shift-Left

## Propósito

Esta guía describe las estrategias técnicas y bio-cognitivas que los ingenieros deben aplicar **antes** de someter su código a revisión de pares. Su objetivo es mitigar defectos en las fases más tempranas del ciclo de vida — cuando el costo de corrección es mínimo — en lugar de depender de la revisión para descubrirlos.

El coach utiliza estas acciones como señales de `secav:PreventiveAction`: su presencia o ausencia en el trabajo diario del ingeniero es evidencia observable de competencia técnica y de auto-gestión cognitiva.

> Las acciones preventivas no reemplazan la revisión de pares. Reducen el ruido en la revisión para que el revisor pueda enfocar su energía en lo que las herramientas no pueden detectar.

---

## 1. Matriz de prevención temprana (Shift-Left)

La mitigación eficiente de defectos ocurre en las fases iniciales del ciclo de vida. Intervenir tarde es costoso: un defecto encontrado en producción cuesta significativamente más que uno encontrado en la fase de requisitos.

| Fase | Acción preventiva | Impacto técnico |
|---|---|---|
| **Mapeo de requisitos** | Criterios de Aceptación Claros (BDD/TDD) | Elimina la ambigüedad lógica antes de escribir la primera línea de código |
| **Diseño arquitectónico** | Definición de Contratos e Interfaces API | Previene errores de integración y desacopla el desarrollo de módulos independientes |
| **Codificación activa** | Análisis Estático Automático en el IDE | Detecta antipatrones, problemas de tipado y posibles fugas de memoria en tiempo real |

### 1.1 Criterios de aceptación claros (BDD/TDD)

**Por qué importa para el coaching:** Si el ingeniero no puede articular los criterios de aceptación de su tarea antes de comenzar a codificar, cualquier evidencia de implementación que produzca es de valor limitado — no hay contra qué evaluarla.

**Señal observable:**
- El ingeniero formula criterios de aceptación en lenguaje verificable antes de escribir código de producción.
- Las pruebas unitarias están escritas antes o junto con el código que prueban (TDD), no después.
- El criterio de aceptación está registrado en el artefacto de la actividad (`secav:AcceptanceCriterion`).

**Señal de alerta para el coach:**
- El ingeniero inicia la implementación sin criterios de aceptación definidos.
- Las pruebas se escriben solo para alcanzar un umbral de cobertura, no para verificar comportamiento.

### 1.2 Definición de contratos e interfaces API

**Por qué importa para el coaching:** La integración es la fuente más frecuente de defectos tardíos. Un contrato definido antes de la implementación es evidencia de competencia de diseño (`secav:DesignCompetency`).

**Señal observable:**
- Las interfaces entre módulos o servicios están definidas y acordadas antes de que los equipos comiencen a implementarlos en paralelo.
- El diseño del contrato aparece como artefacto revisable (`secav:DesignArtifact`) antes de la implementación.

**Señal de alerta para el coach:**
- La integración entre módulos se resuelve en la fase de revisión o merge — señal de que el diseño fue omitido.
- Los errores de integración son recurrentes en las revisiones de código del equipo.

### 1.3 Análisis estático automático en el IDE

**Por qué importa para el coaching:** El análisis estático en tiempo real extiende la capacidad del ingeniero para detectar antipatrones, errores de tipado y fugas de memoria antes de que lleguen al pipeline de CI/CD.

**Señal observable:**
- El IDE del ingeniero tiene linters y analizadores estáticos activos y configurados según los estándares del proyecto.
- Los warnings del analizador estático se atienden antes de hacer commit, no se acumulan.

**Señal de alerta para el coach:**
- El ingeniero desactiva o ignora los warnings del IDE de forma sistemática.
- Los PR contienen violaciones de análisis estático que debieron haberse detectado localmente.

---

## 2. Protocolo de automatización en el entorno local

La automatización actúa como la primera línea de defensa, bloqueando errores mecánicos antes de que alcancen el repositorio compartido. El coach observa si el equipo tiene esta infraestructura activa y si los ingenieros la respetan.

### 2.1 Hooks de Git pre-commit

**Configuración recomendada:** Bloquear los commits locales si el código no supera las pruebas unitarias básicas o si contiene variables de entorno expuestas.

**Señal observable:**
- El repositorio tiene hooks pre-commit configurados y activos para todos los miembros del equipo.
- Los ingenieros no desactivan los hooks para omitir el control (`--no-verify`).

**Señal de alerta para el coach:**
- Commits frecuentes que introducen variables de entorno expuestas o pruebas que fallan — señal de que el hook no está activo o se omite sistemáticamente.
- El equipo percibe los hooks como obstáculos en lugar de como una red de seguridad.

### 2.2 Políticas estrictas de tipado

**Configuración recomendada:** Configurar el compilador para prohibir tipos implícitos (p. ej., `noImplicitAny` en TypeScript), reduciendo drásticamente los errores en tiempo de ejecución.

**Señal observable:**
- La configuración del compilador tiene el modo estricto activo y el proyecto compila sin warnings de tipado.
- Los ingenieros resuelven los errores de tipado en el momento en que aparecen, no los suprimen con `any` o equivalentes.

**Señal de alerta para el coach:**
- Uso sistemático de `any`, casts sin justificación, o supresiones de warnings de tipado — señal de que la política no está siendo interiorizada como práctica de calidad.

### 2.3 Pruebas unitarias automatizadas con umbral de cobertura

**Configuración recomendada:** Definir un umbral mínimo de cobertura de código (Code Coverage > 80 %) aplicado localmente antes de permitir un push.

**Señal observable:**
- El pipeline local tiene configurada la verificación de cobertura como condición de push.
- Las pruebas están escritas para verificar comportamiento, no solo para alcanzar el umbral numéricamente.

**Señal de alerta para el coach:**
- La cobertura es alta pero las pruebas son triviales — prueban getters/setters en lugar de lógica de negocio.
- El ingeniero escribe pruebas al final del sprint para cumplir la métrica, no mientras desarrolla.

---

## 3. Infraestructura cognitiva del desarrollador

El estado mental del ingeniero influye directamente en la densidad de defectos introducidos en el código. El coach observa si el equipo opera bajo condiciones cognitivas que favorecen la calidad o si trabaja sistemáticamente en condiciones que la degradan.

### 3.1 Bloques de trabajo enfocado (Deep Work)

**Práctica recomendada:** Programar intervalos de codificación compleja de 45 a 60 minutos sin notificaciones externas (Slack, Teams, correo) para mantener el mapa mental de la lógica.

**Señal observable:**
- Los ingenieros tienen bloques protegidos en su calendario para trabajo técnico profundo.
- El equipo tiene acuerdos explícitos sobre tiempos de respuesta en canales síncronos durante bloques de desarrollo.

**Señal de alerta para el coach:**
- Los ingenieros reportan que no pueden trabajar más de 20 minutos sin ser interrumpidos.
- Los defectos recurrentes corresponden a casos de borde que se detectan fácilmente con concentración sostenida — señal de que el trabajo se realiza de forma fragmentada.

### 3.2 Límites de fatiga mental

**Práctica recomendada:** Establecer descansos obligatorios tras bloques extensos de desarrollo. La fatiga acumulada deteriora la capacidad de identificar *edge cases* lógicos.

**Señal observable:**
- El ingeniero hace pausas activas entre bloques de trabajo intenso en lugar de encadenarlos.
- El equipo no programa tareas cognitivamente exigentes al final de jornadas ya saturadas.

**Señal de alerta para el coach:**
- Los defectos más frecuentes aparecen en código escrito en horarios de baja energía (tardes tarde, últimas horas del sprint).
- Los ingenieros reportan agotamiento sistemático o no pueden explicar decisiones tomadas bajo presión.

### 3.3 Auto-revisión antes del commit (Self-Review)

**Práctica recomendada:** Tomar un descanso breve de 5 minutos antes de revisar los propios cambios locales, permitiendo detectar errores evidentes con una mirada fresca antes de someterlos a revisión de pares.

**Señal observable:**
- Los PR del ingeniero tienen baja densidad de defectos triviales (typos, código comentado, imports sin usar) — señal de que hubo auto-revisión antes del envío.
- El ingeniero puede describir qué revisó en su propio código antes de solicitar la revisión formal.

**Señal de alerta para el coach:**
- Los revisores reportan que los PR llegan con errores que el propio autor hubiera detectado con una segunda lectura.
- El ingeniero nunca hace pausa entre "terminar el código" y "abrir el PR".

---

## 4. Lista de verificación por sprint: acciones preventivas

El coach revisa esta lista con el equipo al inicio de cada sprint o en la retrospectiva para evaluar si la infraestructura preventiva está activa.

| Acción preventiva | Activo | Parcial | Ausente |
|---|---|---|---|
| Criterios de aceptación definidos antes de codificar | | | |
| Contratos e interfaces API acordados antes de implementación paralela | | | |
| Análisis estático automático activo en el IDE de todos los miembros | | | |
| Hooks pre-commit configurados y respetados | | | |
| Política de tipado estricto activa y sin supresiones injustificadas | | | |
| Umbral de cobertura de pruebas unitarias activo en el pipeline local | | | |
| Bloques de trabajo enfocado protegidos en el calendario del equipo | | | |
| Acuerdos de equipo sobre límites de fatiga y descansos | | | |
| Auto-revisión antes de abrir PR (práctica individual) | | | |

---

## 5. Integración con SECAV-O

| Acción preventiva | Término SECAV-O |
|---|---|
| Criterio de aceptación definido antes de codificar | `secav:AcceptanceCriterion` asociado a `secav:RequirementsActivity` |
| Contrato de API como artefacto de diseño | `secav:DesignArtifact` producido en `secav:DesignActivity` |
| Análisis estático automático | `secav:Measurement` asociado a `secav:CodeImplementation` |
| Hook pre-commit activo | Precondición de `secav:CodeImplementation`; violación es `secav:DefectRecord` |
| Cobertura de pruebas > 80 % | `secav:AcceptanceCriterion` de `secav:TestingActivity` |
| Ausencia de acción preventiva como señal de coaching | `secav:ReviewFinding` o `secav:WorkProductEvidence` que activa `secav:CoachingIntervention` |
| Acción preventiva acordada tras intervención | `secav:PreventiveAction` en `secav:SprintRetrospective` |
| Estado cognitivo del ingeniero como precondición | Análogo a `secav:ReviewerReadiness` en `secav:CodeImplementation` |

---

## 6. Documentos relacionados

| Documento | Relación |
|---|---|
| `coaching-governance/guides/peer-review-antipatterns.md` | Antipatrones en la revisión que estas acciones preventivas buscan evitar |
| `coaching-governance/guides/code-review-best-practices.md` | Prácticas de revisión; las acciones preventivas reducen la carga de la revisión |
| `coaching-governance/guides/unit-test-review.md` | Guía de revisión de diseño de pruebas unitarias |
| `coaching-governance/guides/defect-tracking.md` | Registro de defectos que permite identificar si la prevención está funcionando |
| `templates/sprint-retrospective.md` | Espacio donde el coach introduce el estado de la infraestructura preventiva como punto de mejora |
| `templates/engineer-coaching-assessment.md` | Evaluación de competencias donde las acciones preventivas son evidencia observable |
| `pilot/pilot-protocol.md` | El piloto puede usar la densidad de defectos pre-merge como métrica para evaluar el impacto de estas acciones |