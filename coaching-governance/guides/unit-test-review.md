# Unit Test Design Review Guide

## Purpose

This guide defines the technical criteria for reviewing unit tests (`secav:UnitTestDesignReview`) within the SECAV-O coaching framework. The reviewed artifact is the test code and test case design (`secav:UnitTestDesignArtifact`); findings feed the engineer's `secav:CompetencyAssessment` in `secav:TestingCompetency`.

The coach attends unit test review sessions as a **silent observer** — takes notes, does not intervene verbally, and gives feedback to the team or individually after the session. The protocol is the same as in peer reviews and formal inspections (`coaching-governance/guides/peer-review-sessions.md`, `coaching-governance/guides/formal-inspections.md`).

---

## 1. Golden Rules: FIRST Principles

The FIRST principles are `secav:QualityCriterion` applied to the `secav:UnitTestDesignArtifact`. A unit test that violates one of these principles is a `secav:ReviewFinding` that must be corrected.

| Principle | Observable criterion |
|---|---|
| **Fast** | Execution occurs in milliseconds. No real database calls, remote APIs, or filesystem. |
| **Isolated / Independent** | No test depends on the execution or result of another. They do not share mutable global state. |
| **Repeatable** | Returns exactly the same result regardless of environment, time, or date of execution. |
| **Self-Validating** | Binary result (Pass / Fail). No manual log interpretation or console review. |
| **Timely** | Written in parallel with or before the production code (TDD). |

---

## 2. Case Coverage Checklist

### A. Boundary Value Analysis

- [ ] **Numeric boundaries:** min/max of primitive types (`Integer.MAX_VALUE`, `0`, `-1`, decimal float values).
- [ ] **Collection boundaries:** empty collection (0 elements), collection with 1 element, collection at maximum capacity.
- [ ] **Strings:**
  - [ ] Empty string (`""`).
  - [ ] String with only whitespace (`"   "`).
  - [ ] Extremely long strings (buffer overflow / memory stress).
  - [ ] Single-character string.

### B. Characters, Encoding, and Injection

- [ ] **Unicode / UTF-8:** multibyte characters, emojis, accented characters (`á, é, í, ó, ú, ñ`), non-Latin scripts (Cyrillic, Chinese, Arabic).
- [ ] **Control characters:** `\n`, `\r`, `\t`, `\0` (null byte).
- [ ] **Injection and parsing characters:** `<script>`, `'`, `"`, `;`, `--`, `&`, `%`, `\` — common vectors of parsing and security errors [4].
- [ ] **Padding and trimming:** spaces before, in the middle, and at the end of the input string.

### C. Null State and Non-Existence

- [ ] **`null` / `undefined` values:** pass `null` in arguments and verify the class responds with controlled exceptions (`IllegalArgumentException`, controlled `NullPointerException`, etc.).
- [ ] **Optional / Wrappers:** proper handling of `Optional.empty()` or equivalents.
- [ ] **Not found:** searches returning zero results or non-existent IDs.

### D. Time, Dates, and Concurrency

- [ ] **Clock injection (Clock abstraction):** use of `Clock` or simulated time providers (mocks) instead of `System.currentTimeMillis()` or `Instant.now()`.
- [ ] **Temporal boundary cases:** year change, leap years (February 29), UTC vs. local time transitions.

### E. Exception and Error Handling

- [ ] **Expected exception:** the test validates that the correct exception is thrown on a business or validation failure.
- [ ] **Error message:** the test verifies not just the exception class but also the message or internal error code.

---

## 3. Test Code Structure and Quality

### A. AAA / GWT Pattern

- [ ] **Arrange / Given:** clear setup of input data and mock behavior.
- [ ] **Act / When:** execution of the method under test, preferably in a single line.
- [ ] **Assert / Then:** explicit verification of the expected result.

### B. Mocks, Stubs, and Fakes

- [ ] **Strict isolation:** all external dependencies are simulated (DAOs, repositories, HTTP services, message queues).
- [ ] **Proportional verification:** do not overuse `verify(...)` for internal implementation details — verify only the final result or key communication contracts [5].
- [ ] **Clean mocks:** mock state is reset between tests (`@BeforeEach`, `@AfterEach`, or explicit reset).

### C. Maintainability and Naming

- [ ] **Descriptive names:** the test name describes the scenario and expected result.
  - Example: `givenInvalidEmail_whenRegisterUser_thenThrowValidationException`
- [ ] **No complex logic:** absence of `for` loops, `if`/`switch` statements inside the test. If the test has control flow, the case design is incorrect [1][2].
- [ ] **No `Thread.sleep()`:** use asynchronous wait libraries (`Awaitility` or equivalents) instead of manually pausing the thread.

---

## 4. Coach's Role in the Review

The coach attends as a silent observer. They do not comment on technical findings during the session — that is the reviewers' responsibility.

**During the session, the coach observes and notes:**

| What to observe | Why it matters |
|---|---|
| Whether the review covers test cases (what is tested) or only implementation (how it is tested) | Case coverage is `secav:UnitTestDesign`; implementation is `secav:UnitTestDesignImplementation` — both deserve review |
| Whether reviewers apply FIRST principles as explicit criteria | Consistent use of the agreed `secav:QualityCriterion` |
| Whether missing boundary cases or uncovered injection scenarios are detected | `secav:ReviewFinding` that must be recorded |
| Participation distribution among reviewers | Signal of mastery or inhibition — feeds `secav:CompetencyAssessment` |
| Systemic pattern: whether the same type of omission appears in multiple tests | Signal of need for team-level intervention, not individual |

**After the session, the coach gives feedback:**

- **Group** — if the pattern affects the team's test design in general (e.g., systematic absence of null or boundary cases).
- **Individual in private** — if the observation is specific to an engineer (e.g., tests with recurring complex conditional logic).
- **Organizational** — if the test review is not included in the project plan or is systematically omitted under time pressure.

---

## 5. SECAV-O Integration

| Concept | SECAV-O term |
|---|---|
| Test code under review | `secav:UnitTestDesignArtifact` |
| Review as activity | `secav:UnitTestDesignReview` (subclass of `secav:ReviewActivity` and `secav:UnitTestDesign`) |
| FIRST principles as criteria | `secav:QualityCriterion` applied to the test artifact |
| Test execution result | `secav:TestResult` (subclass of `secav:Artifact` and `secav:Evidence`) |
| Review record | `secav:ReviewRecord` |
| Finding (omitted case, FIRST violation, logic in test) | `secav:ReviewFinding` |
| Coach observation notes | `secav:WorkProductEvidence` |
| Competency assessed | `secav:TestingCompetency` |
| Subsequent competency assessment | `secav:CompetencyAssessment` on `secav:TestingCompetency` |
| Subsequent coach feedback | `secav:CoachingRecommendation` |
| Intervention if systemic pattern | `secav:CoachingIntervention`, `secavo:ImprovementAction` |
| Test defect recorded when closing ticket | `secav:DefectRecord`; `secavo:DefectObservation` with `secavo:phaseInjected = "unit-test-design"` |

---

## 6. Related documents

| Document | Relationship |
|---|---|
| `coaching-governance/guides/peer-review-sessions.md` | Coach's silent observation protocol during the session |
| `coaching-governance/guides/formal-inspections.md` | Formal inspection process applicable to critical test modules |
| `coaching-governance/guides/defect-tracking.md` | Test defects found are recorded with `phaseInjected = "unit-test-design"` |
| `coaching-governance/docs/metrics-model.md` | Unit test coverage and quality metrics |
| `templates/engineer-coaching-assessment.md` | Review findings feed the `secav:TestingCompetency` assessment |

---

## References

[1] Martin, R. C. (2008). *Clean Code: A Handbook of Agile Software Craftsmanship.* Prentice Hall. Chapter 9: Unit Tests — source of the F.I.R.S.T. principles and clean design rules for unit tests.

[2] Koskela, L. (2013). *Effective Unit Testing: A guide for Java developers.* Manning Publications. Fundamentals on test case refinement, testing antipatterns, and proper handling of test doubles.

[3] Beizer, B. (1990). *Software Testing Techniques* (2nd ed.). Van Nostrand Reinhold. Formal methodology of Boundary Value Analysis (BVA) and Equivalence Partitioning for systematic identification of boundary cases.

[4] OWASP Foundation. *OWASP Testing Guide.* https://owasp.org/www-project-web-security-testing-guide/. Recommendations on test vectors with malicious data, injection, and encoding handling.

[5] Meszaros, G. (2007). *xUnit Test Patterns: Refactoring Test Code.* Addison-Wesley. Structuring the AAA / Given-When-Then pattern, isolation with mocks/stubs/test doubles, and test suite maintainability.