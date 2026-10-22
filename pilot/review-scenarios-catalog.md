# Catálogo de Escenarios de Revisión — Pilotos SECAV-O

## Status

Draft v0.1 — escenarios propuestos, sin resultados de piloto.

## Propósito

Este catálogo registra 50 propuestas de revisión de código clasificadas por tipo de interacción y modo de ejecución. Cada escenario es candidato a implementarse como actividad de ingeniería observable dentro del framework SECAV-O, con evidencia recolectable a través del modelo de `ReviewObservation` y `MeasurementObservation`.

Los escenarios sirven como insumo para diseñar pilotos con grupo de control y grupo experimental, permitiendo comparar prácticas actuales contra propuestas específicas antes de adoptarlas formalmente.

Fuente original: *50 Ideas de Revisiones de Código: Humano, Humano-AI, AI-AI — Framework SECAV-O* (documento de propuestas, 2026).

---

## Diseño experimental: grupo de control y grupo experimental

### Principio

El framework no presupone que ninguno de los 50 escenarios mejore la calidad del software. El propósito del diseño experimental es generar evidencia observable para cada propuesta antes de adoptarla formalmente en el proceso de ingeniería.

### Grupo de control

El grupo de control aplica las prácticas de revisión actuales del equipo sin modificación durante el período de observación. Sus resultados constituyen la `Baseline` contra la cual se comparan los hallazgos del grupo experimental.

El grupo de control:
- no adopta ningún escenario del catálogo durante el período activo del piloto;
- registra el mismo conjunto de métricas que el grupo experimental;
- puede usar las herramientas y procesos que ya utiliza normalmente.

### Grupo experimental

El grupo experimental adopta uno o más escenarios seleccionados del catálogo durante el período de observación. La selección debe justificarse antes del inicio del piloto, con criterios de aceptación y métricas acordadas con el coach.

El grupo experimental:
- incorpora el escenario seleccionado junto a sus prácticas habituales, salvo que el diseño del piloto requiera sustitución explícita;
- documenta cualquier ajuste al escenario durante la ejecución como variante observada;
- no puede cambiar de escenario a mitad del período sin documentar el cambio como evento.

### Criterios de asignación

- La asignación a cada grupo debe documentarse antes de iniciar la recolección de datos.
- Se recomiendan grupos de 2–4 ingenieros como mínimo para que los resultados sean comparables.
- El coach documenta los criterios de asignación y los posibles sesgos de selección en el registro del piloto.
- Un equipo pequeño puede ejecutar los grupos en secuencia (rollover A/B): control durante las primeras semanas, experimental después, comparando los mismos ingenieros antes/después.

### Métricas de comparación

Las métricas definidas en `pilot-protocol.md` aplican a ambos grupos. Se recomienda registrar adicionalmente:

| Métrica | Descripción |
|---|---|
| Escenario aplicado | ID y nombre del escenario |
| Tiempo de revisión por PR / artefacto | Minutos desde apertura hasta aprobación |
| Hallazgos por categoría | Seguridad, lógica, estilo, cobertura de tests |
| Hallazgos tardíos | Encontrados post-merge o en producción |
| Comprensión del revisor | ¿Puede el revisor explicar el código revisado? (evidencia observable) |
| Dependencia pasiva de AI | Proporción de aprobaciones sin verificación humana sustantiva |

Ninguna métrica debe interpretarse de forma aislada.

---

## Catálogo de escenarios

Clasificación: **H** = Humano puro · **HA** = Humano-AI · **AA** = AI-AI  
Modo: **Individual** · **Pares** · **Inspección** formal

---

### Grupo H — Humano puro (H-01 a H-10)

| ID | Modo | Escenario | Objetivo |
|---|---|---|---|
| H-01 | Individual | Self-review con checklist de seguridad OWASP antes de commit | Revisor repasa su propio diff con lista OWASP Top 10 |
| H-02 | Individual | Desk-check con traza a requisitos — sin AI | Verifica cada línea contra el requisito funcional correspondiente |
| H-03 | Pares | Walkthrough síncrono de 30 min — autor explica lógica | Par enfocado en lógica, no en estilo |
| H-04 | Inspección | Inspección Fagan formal: planning, overview, preparation, inspection, rework, follow-up | Proceso formal con roles moderador / autor / inspector |
| H-05 | Pares | Peer review asincrónico con límite de 200–400 LOC por hora | Evita fatiga de revisión; foco en defectos |
| H-06 | Individual | Lectura de código con preguntas de seguridad: ¿dónde entra el dato del usuario? | Taint analysis mental |
| H-07 | Inspección | Inspection con checklist de defectos comunes del proyecto (Known Pitfalls Doc) | Mantener documento vivo de errores pasados del equipo |
| H-08 | Pares | Review de competencia: ¿este código preserva el skill del ingeniero junior? | Evalúa si el junior comprende el código AI generado |
| H-09 | Individual | Revisión de evidencias: tests unitarios, logs, capturas — no aprobar sin evidencia observable | No aprobar sin evidencia observable registrada |
| H-10 | Inspección | Role-based inspection: security, test y domain expert revisan el mismo PR | Roles separados por área de competencia |

**Piloto recomendado:** H-01 a H-10 son candidatos para el grupo experimental del **Piloto 1** (mes 6–12). No requieren herramientas adicionales y son los de menor riesgo de adopción.

---

### Grupo HA — Humano-AI (HA-11 a HA-30)

| ID | Modo | Escenario | Objetivo |
|---|---|---|---|
| HA-11 | Individual | AI pre-review: Copilot / CodeRabbit hace primer pase, humano valida | AI marca estilo y bugs obvios; humano aporta juicio estratégico |
| HA-12 | Pares | Human-in-the-loop: AI genera, humano hace spot-checks de coherencia lógica | Detecta violaciones de API legacy |
| HA-13 | Inspección | AI + Checklist humano: AI genera checklist adaptado al PR, humano lo usa | Checklist dinámico por contexto de PR |
| HA-14 | Individual | Revisión de comportamiento, no solo sintaxis: ¿qué hace el código AI? | Tratar el output AI como no confiable por defecto |
| HA-15 | Pares | Known AI Pitfalls review: humano revisa lista de errores comunes de LLM (hallucinations de API) | Detectar métodos inventados por el LLM |
| HA-16 | Inspección | Secure path review: humano obligatorio para authz, pagos, PII, shell exec de salida LLM | Rutas críticas siempre con validación manual |
| HA-17 | Individual | Prompt-to-code traceability: revisar prompt que generó el código + output | Verifica si el prompt contenía constraints de seguridad |
| HA-18 | Pares | AI explains, human decides: AI explica PR en lenguaje natural, humano aprueba | Reduce LGTM superficial (Gön et al. ICSME 2024: 64.7%) |
| HA-19 | Individual | Feedback loop: humano corrige sugerencia AI, AI aprende | HITL para reducir falsos positivos acumulados |
| HA-20 | Inspección | Two-stage: Stage 1 AI — estilo/seguridad básica; Stage 2 humano — arquitectura/dominio | Divide la revisión por nivel de riesgo |
| HA-21 | Pares | AI-generated tests review: humano revisa si los tests de AI cubren edge cases reales | Los tests generados pueden ser débiles o tautológicos |
| HA-22 | Individual | Requirement conformance check: LLM juzga conforme pero overcorrige — humano verifica | Riesgo de systematic overcorrection (Jin & Chen 2026) |
| HA-23 | Inspección | SHACL/OWL validation: AI valida contra ontología SECAV-O, humano interpreta violaciones | Automatiza validación ontológica del framework |
| HA-24 | Pares | Pair programming con Copilot: uno conduce, otro observa, AI sugiere | Driver/observer + AI como tercer participante |
| HA-25 | Individual | AI debt flagging: AI marca deuda técnica, humano prioriza | Refactor continuo basado en señales AI |
| HA-26 | Inspección | Evidence gate: no merge sin evidencia de validación humana registrada contra criterios de aceptación | Criterios de aceptación SECAV-O como puerta obligatoria |
| HA-27 | Pares | Cross-file review: humano pide a AI analizar impacto cross-file que el diff no muestra | Taint analysis asistido más allá del diff |
| HA-28 | Individual | Security review pre-commit: Copilot /security-review en diff no pusheado vs CodeQL post-push | Diferencia de cobertura entre pre y post push |
| HA-29 | Pares | Competency check: ¿el junior puede explicar el código AI? Si no, requiere coaching | Preservar skill; evitar dependencia pasiva de AI |
| HA-30 | Inspección | Retrospective de reviews: medir depth (no solo comment count) y late escapes | Métricas falsables de calidad de revisión |

**Piloto recomendado:** HA-11, HA-14, HA-16, HA-18, HA-20 para **Piloto 1** (mes 6–12). HA-21 a HA-30 para **Piloto 2** (mes 12–24, 12–20 ingenieros).

---

### Grupo AA — AI-AI (AA-31 a AA-50)

| ID | Modo | Escenario | Objetivo |
|---|---|---|---|
| AA-31 | Individual | AI linter + AI security scanner: ESLint AI + Semgrep AI rules | Dos AIs con perspectivas diferentes sobre el mismo código |
| AA-32 | Pares | AI-AI peer: CodeRabbit revisa PR generado por Copilot | Doble LLM como capa de revisión automatizada |
| AA-33 | Inspección | CodeQL (deterministic) + Copilot Autofix (LLM) = detección + fix propuesto | GitHub Advanced Security integrado |
| AA-34 | Individual | Snyk Code (static) + Snyk DeepCode AI (semantic) cross-check | Seguridad; dos motores complementarios sobre el mismo código |
| AA-35 | Pares | SonarQube AI Quality Gate + Sonar AI vulnerability detection | Quality + security en pipeline CI |
| AA-36 | Inspección | AI chain: AI-1 genera, AI-2 genera tests, AI-3 revisa tests vs requisitos | Pipeline AI multi-agente con validación cruzada |
| AA-37 | Individual | LLM self-critique: mismo LLM revisa su propio código con prompt diferente (self-refine) | Self-review; evalúa límites de autocorrección de LLM |
| AA-38 | Pares | AI-AI adversarial: AI atacante intenta explotar código, AI defensor parchea | Red team automatizado |
| AA-39 | Inspección | Pixee / Corgea auto-remediation: scanner AI + fixer AI abre PR borrador | Auto-fix con revisión humana pendiente obligatoria |
| AA-40 | Individual | Veracode ML-enhanced scanning + LLM explanation | Escaner enterprise con explicación en lenguaje natural |
| AA-41 | Pares | Claude Code review loops con cap (evitar >50 rounds) — medir human approvals por PR | Método Anthropic; cap de iteraciones para evitar loops sin fin |
| AA-42 | Inspección | Tool calling: Copilot code review con CodeQL + ESLint integrado (GitHub 2025) | Deterministic + LLM combinados en una sola herramienta |
| AA-43 | Individual | AI coverage check: AI verifica que cada requisito tiene test, otro AI verifica calidad del test | Cobertura de requisitos con doble capa AI |
| AA-44 | Pares | AI format gate: Prettier AI + AI commit message review | Higiene de código y mensajes de commit |
| AA-45 | Inspección | AI secret scanning: GitHub secret scanning AI + AI false positive filter | Detección de secretos con filtro AI de falsos positivos |
| AA-46 | Individual | Performance AI: AI predice regresión de performance, otro AI sugiere optimización | Prevención de degradación de rendimiento |
| AA-47 | Pares | AI documentation sync: AI detecta código sin doc, AI genera doc, AI verifica doc vs código | Sincronización continua de documentación |
| AA-48 | Inspección | Dependency AI: Dependabot AI + Snyk AI evalúan riesgo de dependencias AI-generadas | Supply chain de dependencias generadas por AI |
| AA-49 | Individual | AI policy enforcement: OPA policy + LLM explica violación en lenguaje natural | Policy as code con explicación legible para el ingeniero |
| AA-50 | Inspección | Full pipeline SECAV-O: OWL validator AI + SHACL AI + Evidence recorder AI + Report AI | Pipeline completo y automatizado del framework |

**Piloto recomendado:** AA-33, AA-34, AA-42 para **Piloto 2** (mes 12–24). AA-50 es el objetivo de producción a largo plazo. Los escenarios AA requieren siempre un HA gate final para rutas críticas (authz, pagos, PII); no deben ejecutarse como única capa de revisión.

---

## Mapa de pilotos

| Piloto | Período orientativo | Tamaño del equipo | Escenarios recomendados (experimental) | Grupo de control |
|---|---|---|---|---|
| Piloto 1 | Mes 6–12 | 4–6 ingenieros | H-01 a H-10 + HA-11, HA-14, HA-16, HA-18, HA-20 | Prácticas actuales sin cambio |
| Piloto 2 | Mes 12–24 | 12–20 ingenieros | HA-21 a HA-30 + AA-33, AA-34, AA-42 | Resultados de Piloto 1 como nueva línea base |
| Producción | Mes 24+ | Escala | AA-31 a AA-50 con HA gate obligatorio | Métricas de Piloto 2 como referencia |

---

## Alineación ontológica (SECAV-O)

Cada escenario del catálogo se instancia como una `QualityActivityRequirement` dentro de un `CoachingSprint`. Los hallazgos recolectados se registran como `ReviewObservation` (subclase de `MeasurementObservation` → `Evidence`).

El grupo de control y el grupo experimental producen `Baseline` distintos comparables a través de `CompetencyTrend`. La diferencia entre las dos `Baseline` es la evidencia observable del efecto del escenario.

Los escenarios HA-23 y AA-50 aplican directamente el modelo OWL/SHACL de SECAV-O como mecanismo de verificación automatizada, cerrando el ciclo entre framework conceptual y herramienta de validación.

---

## Fuentes

- NIST SP 800-218 / 218A (SSDF)
- OWASP Code Review Guide / OWASP Top 10 for LLM Apps
- Gön et al., ICSME 2024 — LGTM study (64.7% superficial approval rate)
- Jin & Chen 2026 — systematic overcorrection in LLM-based code review
- GitHub Copilot Code Review docs (2024–2025)
- CodeQL / GitHub Advanced Security docs
- Anthropic Claude Code review method (cap <50 rounds)
- SonarQube AI / Snyk Code / Semgrep / Pixee / Corgea / Veracode