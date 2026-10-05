# Guía de Revisión de Diseño de Pruebas Unitarias

## Propósito

Esta guía define los criterios técnicos para la revisión de pruebas unitarias (`secav:UnitTestDesignReview`) dentro del framework de coaching SECAV-O. El artefacto revisado es el código de prueba y el diseño de casos de prueba (`secav:UnitTestDesignArtifact`); los hallazgos alimentan la `secav:CompetencyAssessment` del ingeniero en `secav:TestingCompetency`.

El coach asiste a las sesiones de revisión de pruebas unitarias como **observador silencioso** — toma notas, no interviene verbalmente, y da retroalimentación al equipo o de forma individual después de la sesión. El protocolo es el mismo que en revisiones de pares e inspecciones formales (`coaching-governance/guides/peer-review-sessions.md`, `coaching-governance/guides/formal-inspections.md`).

---

## 1. Reglas de Oro: Principios FIRST

Los principios FIRST son `secav:QualityCriterion` aplicados al `secav:UnitTestDesignArtifact`. Una prueba unitaria que viola uno de estos principios es un `secav:ReviewFinding` que debe ser corregido.

| Principio | Criterio observable |
|---|---|
| **Fast (Rápidas)** | La ejecución ocurre en milisegundos. Sin llamadas a bases de datos reales, APIs remotas ni sistema de archivos. |
| **Isolated / Independent (Aisladas)** | Ninguna prueba depende de la ejecución o resultado de otra. No comparten estado global mutable. |
| **Repeatable (Repetibles)** | Devuelven exactamente el mismo resultado independientemente del entorno, hora o fecha de ejecución. |
| **Self-Validating (Autovalidables)** | Resultado binario (Pass / Fail). Sin interpretación manual de logs ni revisión de consolas. |
| **Timely (Oportunas)** | Escritas en paralelo o antes del código de producción (TDD). |

---

## 2. Checklist de Cobertura de Casos

### A. Valores Límite y De Frontera (Boundary Value Analysis)

- [ ] **Límites numéricos:** min/max de tipos primitivos (`Integer.MAX_VALUE`, `0`, `-1`, valores flotantes decimales).
- [ ] **Límites de colecciones:** colección vacía (0 elementos), colección con 1 elemento, colección en capacidad máxima.
- [ ] **Cadenas de texto:**
  - [ ] Cadena vacía (`""`).
  - [ ] Cadena con solo espacios en blanco (`"   "`).
  - [ ] Cadenas extremadamente largas (desbordamiento de buffer / estrés de memoria).
  - [ ] Cadena de un solo carácter.

### B. Caracteres, Codificación e Inyección

- [ ] **Unicode / UTF-8:** caracteres multibyte, emojis, caracteres acentuados (`á, é, í, ó, ú, ñ`), scripts no latinos (cirílico, chino, árabe).
- [ ] **Caracteres de control:** `\n`, `\r`, `\t`, `\0` (null byte).
- [ ] **Caracteres de inyección y parsing:** `<script>`, `'`, `"`, `;`, `--`, `&`, `%`, `\` — vectores comunes de errores de parsing y seguridad [4].
- [ ] **Rellenos y trimming:** espacios antes, en medio y al final de la cadena de entrada.

### C. Estado Nulo e Inexistencia

- [ ] **Valores `null` / `undefined`:** pasar `null` en argumentos y verificar que la clase responde con excepciones controladas (`IllegalArgumentException`, `NullPointerException` controlada, etc.).
- [ ] **Optional / Wrappers:** manejo adecuado de `Optional.empty()` o equivalentes.
- [ ] **Elementos no encontrados:** búsquedas que retornan cero resultados o IDs inexistentes.

### D. Tiempo, Fechas y Concurrencia

- [ ] **Inyección de reloj (Clock abstraction):** uso de `Clock` o proveedores de tiempo simulados (mocks) en lugar de `System.currentTimeMillis()` o `Instant.now()`.
- [ ] **Casos de frontera temporal:** cambio de año, años bisiestos (29 de febrero), transiciones UTC vs. horario local.

### E. Manejo de Excepciones y Errores

- [ ] **Excepción esperada:** la prueba valida que se lance la excepción correcta ante un fallo de negocio o validación.
- [ ] **Mensaje de error:** la prueba verifica no solo la clase de la excepción sino el mensaje o código de error interno.

---

## 3. Estructura y Calidad del Código de Prueba

### A. Patrón AAA / GWT

- [ ] **Arrange / Given:** configuración clara de datos de entrada y comportamiento de mocks.
- [ ] **Act / When:** ejecución del método bajo prueba, preferentemente en una sola línea.
- [ ] **Assert / Then:** verificación explícita del resultado esperado.

### B. Mocks, Stubs y Fakes

- [ ] **Aislamiento estricto:** todas las dependencias externas están simuladas (DAOs, repositorios, servicios HTTP, colas de mensajes).
- [ ] **Verificación proporcional:** no sobreutilizar `verify(...)` para detalles de implementación interna — verificar solo el resultado final o los contratos de comunicación clave [5].
- [ ] **Mocks limpios:** el estado de los mocks se reinicia entre pruebas (`@BeforeEach`, `@AfterEach` o reset explícito).

### C. Mantenibilidad y Nomenclatura

- [ ] **Nombres descriptivos:** el nombre de la prueba describe el escenario y el resultado esperado.
  - Ejemplo: `givenInvalidEmail_whenRegisterUser_thenThrowValidationException`
- [ ] **Sin lógica compleja:** ausencia de bucles `for`, sentencias `if`/`switch` dentro de la prueba. Si la prueba tiene control de flujo, el diseño de casos está incorrecto [1][2].
- [ ] **Sin `Thread.sleep()`:** uso de librerías de espera asíncrona (`Awaitility` o equivalentes) en lugar de pausar el hilo manualmente.

---

## 4. Rol del Coach en la Revisión

El coach asiste como observador silencioso. No comenta los hallazgos técnicos durante la sesión — eso es responsabilidad de los revisores.

**Durante la sesión, el coach observa y anota:**

| Qué observar | Por qué importa |
|---|---|
| Si la revisión cubre casos de prueba (qué se prueba) o solo la implementación (cómo se prueba) | La cobertura de casos es `secav:UnitTestDesign`; la implementación es `secav:UnitTestDesignImplementation` — ambas merecen revisión |
| Si los revisores aplican los principios FIRST como criterios explícitos | Uso consistente de los `secav:QualityCriterion` acordados |
| Si se detectan casos límite omitidos o escenarios de inyección no cubiertos | `secav:ReviewFinding` que debe quedar registrado |
| Distribución de la participación entre revisores | Señal de dominio o inhibición — alimenta la `secav:CompetencyAssessment` |
| Patrón sistémico: si el mismo tipo de omisión aparece en múltiples pruebas | Señal de necesidad de intervención a nivel equipo, no individual |

**Después de la sesión, el coach da retroalimentación:**

- **Grupal** — si el patrón afecta al diseño de pruebas del equipo en general (ej. ausencia sistemática de casos nulos o de frontera).
- **Individual en privado** — si la observación es específica de un ingeniero (ej. pruebas con lógica condicional compleja recurrente).
- **Organizacional** — si la revisión de pruebas no está incluida en el plan del proyecto o se omite sistemáticamente bajo presión de tiempo.

---

## 5. Integración con SECAV-O

| Concepto | Término SECAV-O |
|---|---|
| Código de prueba bajo revisión | `secav:UnitTestDesignArtifact` |
| La revisión como actividad | `secav:UnitTestDesignReview` (subclase de `secav:ReviewActivity` y `secav:UnitTestDesign`) |
| Principios FIRST como criterios | `secav:QualityCriterion` aplicado al artefacto de prueba |
| Resultado de ejecución de pruebas | `secav:TestResult` (subclase de `secav:Artifact` y `secav:Evidence`) |
| Registro de la revisión | `secav:ReviewRecord` |
| Hallazgo (caso omitido, violación FIRST, lógica en prueba) | `secav:ReviewFinding` |
| Notas de observación del coach | `secav:WorkProductEvidence` |
| Competencia evaluada | `secav:TestingCompetency` |
| Evaluación de competencia posterior | `secav:CompetencyAssessment` sobre `secav:TestingCompetency` |
| Retroalimentación posterior del coach | `secav:CoachingRecommendation` |
| Intervención si hay patrón sistémico | `secav:CoachingIntervention`, `secavo:ImprovementAction` |
| Defecto de prueba registrado al cerrar ticket | `secav:DefectRecord`; `secavo:DefectObservation` con `secavo:phaseInjected = "unit-test-design"` |

---

## 6. Documentos relacionados

| Documento | Relación |
|---|---|
| `coaching-governance/guides/peer-review-sessions.md` | Protocolo de observación silenciosa del coach durante la sesión |
| `coaching-governance/guides/formal-inspections.md` | Proceso formal de inspección aplicable a módulos de prueba críticos |
| `coaching-governance/guides/defect-tracking.md` | Los defectos de prueba encontrados se registran con `phaseInjected = "unit-test-design"` |
| `coaching-governance/docs/metrics-model.md` | Métricas de cobertura y calidad de pruebas unitarias |
| `templates/engineer-coaching-assessment.md` | Los hallazgos de revisión alimentan la evaluación de `secav:TestingCompetency` |

---

## Referencias

[1] Martin, R. C. (2008). *Clean Code: A Handbook of Agile Software Craftsmanship.* Prentice Hall. Capítulo 9: Unit Tests — fuente de los principios F.I.R.S.T. y las reglas de diseño limpio para pruebas unitarias.

[2] Koskela, L. (2013). *Effective Unit Testing: A guide for Java developers.* Manning Publications. Fundamentos sobre refinamiento de casos de prueba, antipatrones de testing y manejo adecuado de test doubles.

[3] Beizer, B. (1990). *Software Testing Techniques* (2nd ed.). Van Nostrand Reinhold. Metodología formal de Boundary Value Analysis (BVA) y Equivalence Partitioning para la identificación sistemática de casos límite.

[4] OWASP Foundation. *OWASP Testing Guide.* https://owasp.org/www-project-web-security-testing-guide/. Recomendaciones sobre vectores de prueba con datos maliciosos, inyección y manejo de codificación.

[5] Meszaros, G. (2007). *xUnit Test Patterns: Refactoring Test Code.* Addison-Wesley. Estructuración del patrón AAA / Given-When-Then, aislamiento con mocks/stubs/test doubles y mantenibilidad del suite de pruebas.