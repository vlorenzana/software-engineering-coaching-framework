# Minuta de Junta de Coaching

<!-- Completa una instancia de esta plantilla en cada junta formal que facilite el coach.
     Distribuye el borrador a los participantes dentro de las 24 horas posteriores a la reunión.
     Cada acuerdo es una instancia de secav:MeetingAgreement rastreable en siguientes juntas. -->

## Encabezado

- **Código de minuta:** MIN-`AAAA`-`XXXX`
- **Fecha:** DD/MM/AAAA
- **Hora de inicio / fin:** HH:MM – HH:MM
- **Tipo de junta:**
  - [ ] Kick-off de proyecto
  - [ ] Planificación de sprint
  - [ ] Retrospectiva
  - [ ] Sesión 1-on-1
  - [ ] Revisión técnica / inspección
  - [ ] Seguimiento de acuerdos previos
  - [ ] Ad-hoc / urgente
- **Facilitador (coach):** [Nombre]
- **Participantes:** [Nombre — Rol, Nombre — Rol, ...]
- **Sprint / Ciclo:** [ID del sprint o periodo]

**SECAV-O:** Esta minuta es una instancia de `secav:MeetingMinutes`, producida en una `secav:CoachingMeeting` y vinculada al `secav:CoachingIntervention` del ciclo actual.

---

## 1. Contexto y Propósito

> ¿Por qué se realizó esta junta? ¿Qué situación, observación o artefacto motivó la convocatoria?

_

---

## 2. Temas Tratados

| # | Tema | Decisión / Resultado | Término SECAV-O |
|---|------|----------------------|-----------------|
| 1 | | | |
| 2 | | | |
| 3 | | | |

> Agrega o elimina filas según los temas discutidos.

---

## 3. Acuerdos y Compromisos

Cada fila es un `secav:MeetingAgreement` con responsable, fecha límite y estado de seguimiento.
Los acuerdos abiertos se revisan **siempre al inicio de la próxima junta** de este tipo.

| ID | Acuerdo / Compromiso | Responsable | Fecha límite | Estado |
|----|----------------------|-------------|--------------|--------|
| ACU-01 | | [Nombre] | DD/MM/AAAA | [ ] Abierto |
| ACU-02 | | [Nombre] | DD/MM/AAAA | [ ] Abierto |
| ACU-03 | | [Nombre] | DD/MM/AAAA | [ ] Abierto |

**Escalamiento de acuerdos:**
- Si un acuerdo requiere acompañamiento individual → registrar `secav:CoachingIntervention` en `templates/engineer-coaching-assessment.md`
- Si un acuerdo genera una mejora de proceso sistémica → registrar como `secavo:ImprovementAction` en `templates/sprint-retrospective.md`
- Si un acuerdo derivan en un análisis de causa raíz → iniciar `templates/rca-defect-analysis.md`

---

## 4. Revisión de Acuerdos de Juntas Anteriores

| ID anterior | Acuerdo | Responsable | Estado al cierre |
|-------------|---------|-------------|------------------|
| ACU-XX | [descripción del acuerdo previo] | [Nombre] | [ ] Completado  [ ] Pendiente  [ ] Cancelado |

---

## 5. Puntos Abiertos

Temas que requieren información adicional, análisis o una próxima sesión para resolverse.

| # | Punto abierto | Próximo paso | Responsable |
|---|---------------|--------------|-------------|
| 1 | | | [Nombre] |
| 2 | | | [Nombre] |

---

## 6. Próxima Junta

- **Fecha propuesta:** DD/MM/AAAA
- **Hora:** HH:MM
- **Agenda tentativa:**
  1. Revisión de acuerdos (ACU-01, ACU-02, ...)
  2. [Tema 1]
  3. [Tema 2]

---

## Distribución y Confirmación

Esta minuta fue distribuida a los participantes el: DD/MM/AAAA

| Participante | Rol | Confirmación de recepción |
|---|---|---|
| [Nombre] | [Rol] | [ ] Recibido |
| [Nombre] | [Rol] | [ ] Recibido |

> El coach archiva las minutas en el canal o repositorio acordado con el equipo. No se distribuyen fuera del equipo sin consentimiento de los participantes.

---

## Documentos relacionados

| Documento | Relación |
|---|---|
| `templates/sprint-retrospective.md` | Acuerdos que mejoran el proceso se registran como ImprovementActions |
| `templates/engineer-coaching-assessment.md` | Intervenciones de coaching individuales derivadas de esta junta |
| `templates/rca-defect-analysis.md` | Si la junta analizó un defecto P1/P2 |
| `templates/annual-coaching-plan.md` | Acuerdos de largo plazo que impactan el plan de coaching del ciclo |
| `coaching-governance/guides/coach-observation-checklist.md` | Observaciones del coach que motivaron esta junta |
| `coaching-governance/guides/coach-attitudes.md` | Actitudes del coach durante la facilitación |