# Análisis de Causa Raíz de Defecto (RCA)

<!-- Completa una instancia de esta plantilla por cada defecto de severidad P1 (Crítico) o P2 (Mayor).
     Para defectos menores, registra directamente en defect-log.csv sin RCA completo. -->

## Encabezado

- **Código de incidente:** INC-`AAAA`-`XXXX`
- **Fecha del reporte:** DD/MM/AAAA
- **Líder del análisis:** [Nombre]
- **Coach responsable:** [Nombre]
- **Severidad:** [ ] P1 — Crítico  [ ] P2 — Mayor
- **Sprint / Ciclo:** [ID del sprint]

---

## 1. Metadatos del entorno de desarrollo

| Campo | Valor |
|---|---|
| Repositorio / Microservicio | ej. `github.com/org/payment-gateway` |
| Rama / Branch afectada | ej. `main` / `release/v2.4.0` |
| Commit defectuoso (SHA) | ej. `a1b2c3d4e5f6...` |
| Commit de rollback / fix | ej. `f7e6d5c4b3a2...` |
| Ambiente impactado | [ ] Producción  [ ] Staging  [ ] Beta |
| Pull Request asociado | PR #`NNN` |

**SECAV-O:** El commit defectuoso es el `secav:SourceCodeArtifact` que originó el `secav:DefectRecord`. El PR asociado es el `secav:FormalReviewRequest` que lo introdujo al repositorio principal.

---

## 2. Resumen del impacto

- **Descripción del fallo:**
  > ej. El endpoint `/v1/charge` respondió con errores 500 de forma masiva, bloqueando el procesamiento de pagos.

- **Tiempo de inactividad (downtime):** ___ horas, ___ minutos
- **Usuarios / clientes afectados:** ej. 15 % de los usuarios activos en la plataforma web
- **Fase de inyección** (`secavo:phaseInjected`): [ ] Requisitos  [ ] Diseño  [ ] Codificación  [ ] Pruebas
- **Fase de detección** (`secavo:phaseDetected`): [ ] Revisión de código  [ ] Prueba unitaria  [ ] Integración  [ ] Producción
- **Método de detección** (`secavo:detectionMethod`): [ ] Inspección formal  [ ] Revisión de pares  [ ] Prueba automatizada  [ ] Alerta de monitoreo  [ ] Reporte de usuario

---

## 3. Línea de tiempo del ciclo de vida del software

Registra los eventos clave desde la aprobación del cambio hasta la resolución. Usa formato `HH:MM (Día N)`.

| Hora | Evento | Responsable |
|---|---|---|
| HH:MM (Día 1) | **Aprobación de PR** — el PR #NNN es aprobado en revisión de pares sin observaciones críticas | Revisor |
| HH:MM (Día 1) | **Pipeline CI/CD** — el build automatizado se ejecuta; las pruebas unitarias pasan exitosamente | CI/CD |
| HH:MM (Día 1) | **Despliegue** — el commit defectuoso se despliega a Producción | CI/CD |
| HH:MM (Día 1) | **Detección** — las métricas de APM (Datadog / New Relic) registran un pico anómalo de excepciones | Monitor |
| HH:MM (Día 1) | **Mitigación temporal** — el equipo ejecuta un rollback al commit anterior estable | [Nombre] |
| HH:MM (Día N) | **Fix permanente** — se despliega la corrección definitiva | [Nombre] |

> Agrega o elimina filas según la cronología real del incidente.

---

## 4. Análisis de causa raíz — 5 Porqués de ingeniería

Responde cada pregunta de forma concreta. Si la cadena termina antes del quinto porqué, la causa raíz está identificada en ese punto.

**¿Por qué falló el sistema en producción?**

> Respuesta: _

**¿Por qué ocurrió esa condición de fallo?**

> Respuesta: _

**¿Por qué el código no manejó ese caso de forma segura?**

> Respuesta: _

**¿Por qué las pruebas automatizadas en CI/CD no detectaron la vulnerabilidad?**

> Respuesta: _

**¿Por qué se aprobó el Pull Request con esta debilidad lógica? ← Causa raíz**

> Respuesta: _

**Causa raíz identificada (resumen en una oración):**

> _

**Categoría de la causa raíz:**

| Categoría | ¿Aplica? | Antipatrón SECAV-O asociado |
|---|---|---|
| Revisión bajo fatiga cognitiva | [ ] | `secav:OversizedReviewSession`, `secav:ReviewerEnergyCondition` |
| Pruebas incompletas (solo happy path) | [ ] | `secav:HappyPathOnlyReview` |
| PR demasiado grande para revisar | [ ] | `secav:OversizedPullRequest` |
| Aprobación sin lectura real | [ ] | `secav:RubberStampApproval` |
| Discusión arquitectónica tardía | [ ] | `secav:LateArchitecturalDiscussion` |
| Falta de contexto en el PR | [ ] | `secav:MissingReviewContext` |
| Análisis estático sin configurar | [ ] | `secav:ManualStyleReview`, `secav:AutomationGate` ausente |
| Otra causa | [ ] | — |

---

## 5. Plan de acciones correctivas (SMART)

Cada acción debe ser: Específica, Medible, Asignable, Realista y con Fecha límite.

| ID | Acción técnica obligatoria | Responsable | Fecha límite | Estado |
|---|---|---|---|---|
| SOFT-01 | Implementar validación defensiva del campo/caso afectado y subir el fix | [Nombre] | DD/MM/AAAA | [ ] Pendiente |
| SOFT-02 | Agregar pruebas de integración que simulen payloads corruptos o vacíos para el caso afectado | [Nombre] | DD/MM/AAAA | [ ] Pendiente |
| SOFT-03 | Configurar regla en linter / SonarQube / analizador estático para forzar verificación del tipo de dato afectado | [Nombre] | DD/MM/AAAA | [ ] Pendiente |

**SECAV-O:** Cada fila es una `secavo:CorrectiveAction` vinculada al `secav:DefectRecord` de este incidente. Las filas SOFT-02 y SOFT-03 pueden derivar adicionalmente en `secav:PreventiveAction` si se incorporan como estándares del equipo.

---

## 6. Acciones preventivas sistémicas

Si la causa raíz revela una brecha de proceso o cultura que puede repetirse, registra aquí las acciones para que no ocurra de nuevo en otros módulos o equipos.

| ID | Acción preventiva | Responsable | Fecha límite | Estado |
|---|---|---|---|---|
| PREV-01 | | [Nombre] | DD/MM/AAAA | [ ] Pendiente |
| PREV-02 | | [Nombre] | DD/MM/AAAA | [ ] Pendiente |

**SECAV-O:** Cada fila es una `secav:PreventiveAction` orientada a evitar la clase de defecto, no solo la instancia. Se registra en `secavo:SprintRetrospective` como `secavo:ImprovementAction`.

---

## 7. Intervención de coaching derivada

El coach completa esta sección al cerrar el RCA. No se comparte con gerencia como evaluación de rendimiento individual.

- **Competencia afectada** (`secav:Competency`): [ ] ReviewCompetency  [ ] TestingCompetency  [ ] SecurityCompetency  [ ] DesignCompetency
- **Patrón observado:** _
- **Intervención planificada** (`secav:CoachingIntervention`): _
- **Sesión individual programada:** DD/MM/AAAA

---

## 8. Cierre y verificación

- **Fecha de cierre del RCA:** DD/MM/AAAA
- **Fix verificado en producción:** [ ] Sí  [ ] No  — Fecha: DD/MM/AAAA
- **Acciones correctivas completadas:** [ ] Todas  [ ] Parcial — pendientes: ___
- **Acciones preventivas completadas:** [ ] Todas  [ ] Parcial — pendientes: ___
- **Defecto registrado en** `templates/defect-log.csv`: [ ] Sí
- **RCA archivado en el registro de coaching del ingeniero** (`templates/engineer-coaching-assessment.md`): [ ] Sí

---

## Documentos relacionados

| Documento | Relación |
|---|---|
| `templates/defect-log.csv` | Registro estructurado del defecto; este RCA complementa cada fila de severidad P1/P2 |
| `coaching-governance/guides/defect-tracking.md` | Protocolo del coach para clasificar y cerrar tickets de defectos |
| `coaching-governance/guides/peer-review-antipatterns.md` | Antipatrones de revisión que este RCA puede identificar como causa raíz |
| `coaching-governance/guides/shift-left-prevention.md` | Acciones preventivas que reducen la probabilidad de este tipo de defecto |
| `templates/sprint-retrospective.md` | Las acciones preventivas sistémicas (§6) se incorporan como ImprovementActions en la retrospectiva |
| `templates/engineer-coaching-assessment.md` | La intervención de coaching (§7) se registra en la evaluación del ingeniero |