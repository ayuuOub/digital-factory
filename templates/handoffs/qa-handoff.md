AGENT: qa-browser-validation-agent
PHASE: FULL QA VALIDATION
STATUS: <CHECKPOINT>  # e.g., PASS, FAIL, BLOCKED
SCOPE: <SCOPE>  # What areas are being validated (e.g., product acceptance criteria, regression, specific features)
EVIDENCE: <EVIDENCE>  # Validation results, test logs, pass/fail status
FILES_CHANGED: <FILES_CHANGED>  # Typically none, as QA does not modify product code; if any validation scripts/configs, list them
OPEN_ISSUES: <OPEN_ISSUES>  # Any defects found, blockers, or unresolved validation questions
HUMAN APPROVAL REQUIRED: NO  # Approval comes later at Final Human Validation (after QA, Security, and Documentation)
NEXT_ACTION: Proceed to security-agent for Final Implementation Security Audit (if not blocked)