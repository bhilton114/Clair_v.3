# Clair V3.3

**Clair is a private cognitive AI prototype focused on governed reasoning, memory, verification, and self-correction.**

Clair is being developed as a solo-built, correction-first cognitive system. The core implementation is currently private while patent, licensing, and safety options are evaluated.

This public repository is used to share safe project summaries, benchmark-style results, development direction, and high-level design goals without exposing the internal source code or construction methods.

---

## Current Restoration Status

Project Clair is currently in a V3 restoration phase focused on rebuilding Clair as a reusable resourcefulness-based cognitive reasoner rather than a benchmark-shaped answer system.

The current architecture centers on the following path:

NeedDetector → CapabilityPlanner → ResourcefulnessCoordinator → Tool/Source Fetch → EvidenceScorer → AnswerGate → ReasoningEngine → Memory/Reflection

### Latest Completed Milestone

RESTORE-011 has been completed.

Clair can now answer supported headquarters lookup questions through the restored resourcefulness pipeline. The verified end-to-end path is:

NeedDetector → CapabilityPlanner → ResourcefulnessCoordinator → source fetch → EvidenceScorer → AnswerGate

Confirmed example:

> OpenAI is headquartered at 1455 3rd Street, San Francisco, California, U.S.

### Regression Coverage Confirmed

The current regression set includes:

- Headquarters lookup
- France population lookup
- Python version lookup
- Apple CEO lookup
- Claim verification
- Direct math
- Owner safe-failure behavior

### Current Restoration Rule

Every fix must teach Clair a reusable method for solving a class of problems. Clair should not be patched with benchmark-specific shortcuts, hardcoded answers, or one-off task logic.

### Next Target

RESTORE-012: Owner Attribute Validation

Goal:

Make “Who owns X now?” work through the same source-supported attribute path while rejecting founder, CEO, investor, parent-company, and partner confusion.
 → Verify evidence
 → Apply governance
 → Answer or refuse
 → Reflect and learn
