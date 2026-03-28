# Topic Risk & Technical Debt Assessment — Evaluation

**Analysis ID**: {task_id}-TOP-EV-02
**Session ID**: {session_id}
**Analysis Date**: {date}
**Project**: {project_name}
**Topic**: {topic_name}
**Gap Analysis Reference**: {task_id}-TOP-EV-01
**AS-IS References**: {task_id}-TOP-AS-01, {task_id}-TOP-AS-02, {task_id}-TOP-AS-03

---

## 1. Technical Risk Register

| Risk ID | Risk Description | Category | Source (Gap / AS-IS finding) | Probability | Impact | Severity | Mitigation Direction |
|---------|-----------------|----------|------------------------------|-------------|--------|----------|---------------------|
| RISK-01 | {risk_description} | {Performance / Security / Reliability / Maintainability / Data Integrity / Scalability / Operational} | {FR/NFR ID or AS-IS finding reference} | {High / Medium / Low} | {High / Medium / Low} | {🔴 / 🟡 / 🟢} | {high-level mitigation direction} |
| RISK-02 | {description} | {category} | {source} | {prob} | {impact} | {severity} | {mitigation} |

*(Document all risks identified during Phases 4–5 — no risks to omit)*

---

## 2. Technical Debt Register

| Debt ID | Debt Description | Category | Location | Interest Rate | Priority |
|---------|-----------------|----------|----------|---------------|----------|
| DEBT-01 | {debt_description} | {Design / Test / Documentation / Infrastructure / Process} | `{component_or_file}` | {High (blocking progress) / Medium (slowing velocity) / Low (cosmetic)} | {High / Medium / Low} |
| DEBT-02 | {description} | {category} | `{location}` | {interest_rate} | {priority} |

*(If none: "No significant technical debt items identified.")*

---

## 3. Systemic Vulnerability Assessment

| # | Vulnerability | Type | Affected Components | Trigger Condition | Severity |
|---|--------------|------|--------------------|--------------------|---------|
| 1 | {e.g., "Session fixation attack possible — session ID not regenerated on login"} | {Security / Reliability / Data Loss / Performance} | `{components}` | {when X happens} | {🔴 / 🟡 / 🟢} |
| 2 | {vulnerability} | {type} | `{components}` | {trigger} | {severity} |

*(If none: "No systemic vulnerabilities identified.")*

---

## 4. Risk Heat Map Summary

| | **Low Impact** | **Medium Impact** | **High Impact** |
|---|----------------|-------------------|-----------------|
| **High Probability** | {risk IDs} | {risk IDs} | {risk IDs} |
| **Medium Probability** | {risk IDs} | {risk IDs} | {risk IDs} |
| **Low Probability** | {risk IDs} | {risk IDs} | {risk IDs} |

---

## 5. Top Risks Requiring Immediate Attention

| Priority | Risk ID | Risk | Recommended Action |
|----------|---------|------|--------------------|
| 1 | {RISK-ID} | {description} | {action} |
| 2 | {RISK-ID} | {description} | {action} |
| 3 | {RISK-ID} | {description} | {action} |

---

## 6. Summary

**Total Risks Identified**: {count} (🔴 {n} critical, 🟡 {n} moderate, 🟢 {n} low)

**Total Debt Items**: {count}

**Systemic Vulnerabilities**: {count} (🔴 {n} critical)

**Overall Risk Profile**: {Low / Moderate / High / Critical}
