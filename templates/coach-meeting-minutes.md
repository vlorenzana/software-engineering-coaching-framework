# Minuta de Junta de Coaching

<!-- Completa una instancia de esta plantilla en cada junta formal que facilite el coach.
     Distribuye el borrador a los participantes dentro de las 24 horas posteriores a la reunión.
     Cada acuerdo es una instancia de secav:MeetingAgreement rastreable en siguientes juntas. -->

> **ELEMENTOS MÍNIMOS OBLIGATORIOS — la minuta solo es válida si contiene los tres:**
>
> | # | Elemento | Sección | Sin esto... |
> |---|----------|---------|-------------|
> | 1 | **Participantes** — nombre y rol de cada asistente | § 1 | No hay trazabilidad de quién tomó los acuerdos |
> | 2 | **Temas tratados** — al menos un tema con su resultado o decisión | § 2 | No hay registro de qué se discutió |
> | 3 | **Acuerdos con fecha** — al menos un acuerdo con responsable y fecha límite explícita | § 3 | No hay compromiso rastreable ni seguimiento posible |
>
> Una minuta que omite cualquiera de estos tres elementos no puede cerrar la junta y debe completarse antes de distribuirse.

---

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
- **Sprint / Ciclo:** [ID del sprint o periodo]

**SECAV-O:** Esta minuta es una instancia de `secav:MeetingMinutes`, producida en una `secav:CoachingMeeting` y vinculada al `secav:CoachingIntervention` del ciclo actual.

---

## 1. Participantes

> **Obligatorio.** Registra a todos los asistentes. Una junta sin participantes documentados no tiene trazabilidad.

| Nombre | Rol | Asistencia |
|--------|-----|------------|
| [Nombre] | [Rol] | [ ] Presente  [ ] Excusa justificada |
| [Nombre] | [Rol] | [ ] Presente  [ ] Excusa justificada |
| [Nombre] | [Rol] | [ ] Presente  [ ] Excusa justificada |

---

## 2. Contexto y Propósito

> ¿Por qué se realizó esta junta? ¿Qué situación, observación o artefacto motivó la convocatoria?

_

---

## 3. Temas Tratados

> **Obligatorio.** Registra al menos un tema con su resultado o decisión. Sin esto no hay registro de lo que se discutió.

| # | Tema | Decisión / Resultado | Término SECAV-O |
|---|------|----------------------|-----------------|
| 1 | | | |
| 2 | | | |
| 3 | | | |

> Agrega o elimina filas según los temas discutidos.

---

## 4. Acuerdos y Compromisos

> **Obligatorio.** Cada acuerdo debe tener responsable y fecha límite explícita. Sin fecha no hay seguimiento posible.
>
> Los acuerdos abiertos se revisan **siempre al inicio de la próxima junta** de este tipo.

Cada fila es un `secav:MeetingAgreement` con responsable, fecha límite y estado de seguimiento.

| ID | Acuerdo / Compromiso | Responsable | **Fecha límite** | Estado |
|----|----------------------|-------------|------------------|--------|
| ACU-01 | | [Nombre] | **DD/MM/AAAA** | [ ] Abierto |
| ACU-02 | | [Nombre] | **DD/MM/AAAA** | [ ] Abierto |
| ACU-03 | | [Nombre] | **DD/MM/AAAA** | [ ] Abierto |

**Escalamiento de acuerdos:**
- Si un acuerdo requiere acompañamiento individual → registrar `secav:CoachingIntervention` en `templates/engineer-coaching-assessment.md`
- Si un acuerdo genera una mejora de proceso sistémica → registrar como `secavo:ImprovementAction` en `templates/sprint-retrospective.md`
- Si un acuerdo deriva en un análisis de causa raíz → iniciar `templates/rca-defect-analysis.md`

---

## 5. Revisión de Acuerdos de Juntas Anteriores

| ID anterior | Acuerdo | Responsable | Estado al cierre |
|-------------|---------|-------------|------------------|
| ACU-XX | [descripción del acuerdo previo] | [Nombre] | [ ] Completado  [ ] Pendiente  [ ] Cancelado |

---

## 6. Puntos Abiertos

Temas que requieren información adicional, análisis o una próxima sesión para resolverse.

| # | Punto abierto | Próximo paso | Responsable |
|---|---------------|--------------|-------------|
| 1 | | | [Nombre] |
| 2 | | | [Nombre] |

---

## 7. Próxima Junta

- **Fecha propuesta:** DD/MM/AAAA
- **Hora:** HH:MM
- **Agenda tentativa:**
  1. Revisión de acuerdos (ACU-01, ACU-02, ...)
  2. [Tema 1]
  3. [Tema 2]

---

## Cierre y Distribución

> Antes de distribuir, verifica que la minuta cumpla los tres elementos obligatorios:
> - [ ] § 1 completada — todos los participantes registrados con nombre y rol
> - [ ] § 3 completada — al menos un tema con decisión o resultado
> - [ ] § 4 completada — al menos un acuerdo con responsable y **fecha límite explícita**

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