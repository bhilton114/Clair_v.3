# Governed Experience Reuse in a Local-First Cognitive Agent: Architecture, Authority Boundaries, and Preliminary Regression Evidence

**Blake Hilton**  
Project Clair, independent research  
**Manuscript version:** 0.1 (technical preprint draft)  
**Date:** October 12, 2026  
**Status:** Author manuscript, not peer reviewed. Results are developer-reported and await independent reproduction.

## Abstract

Long-lived AI agents may accumulate records of previous interactions, attempted actions, retrieved evidence, and subsequent corrections. Reusing these records can create a failure mode: a past answer or tool output can be elevated into an authoritative fact without sufficient evidence. This paper describes a local-first prototype architecture, Project Clair, in which experience reuse is separated from evidence admissibility and final answer authority. We present a design for bounded experience persistence, selection, and consumption, with explicit denial of conflicted, rejected, blocked, superseded, and other ineligible states. The architecture treats optional large language models as candidate generators while reserving decision authority for independent rules, verification, and memory-policy components. We summarize preliminary, developer-reported regression checkpoints, including a 20/20 authority-boundary test pass recorded October 9, 2026. These results support the narrower claim that selected denial cases were handled as expected in a local test environment; they do not establish general reasoning superiority, continuous self-improvement, formal safety, or full end-to-end experience learning.

**Keywords:** AI agents; local-first systems; epistemic governance; experience reuse; provenance; memory admission; authority boundaries; retrieval safety

## 1. Problem statement

An assistant that persists interactions beyond a single session must distinguish (a) records of what happened, (b) claims supported by evidence, and (c) knowledge permitted to influence future decisions. A simple history or vector retrieval implementation may return a previously generated statement even when that statement was later corrected or explicitly rejected. The design problem studied here is therefore not merely durable storage. It is **admissible reuse**: under which conditions may prior experience inform a later answer or action?

We distinguish three classes of events:

1. **Observation:** a request, tool result, response, or other recorded event.
2. **Assessment:** evidence, provenance, uncertainty, and conflict status attached to that event or claim.
3. **Admission:** a policy decision allowing some derived material to influence future retrieval, reasoning, planning, or memory.

The core hypothesis is architectural: separating these transitions can reduce specific classes of authority confusion. Establishing that it actually reduces error rates requires controlled comparison against alternatives.

## 2. System context and trust boundaries

Project Clair is an experimental cognitive agent designed to execute locally, with optional tool and language-model assistance. Its reported architecture includes perception and routing, structured memory, planning/simulation, a reasoning engine, verification gates, and reflection/experience handling.

The principal trust boundary is between **proposed content** and **authorized content**. A model completion or retrieved history item may be useful without becoming a verified fact. Similarly, a successful past tool call is not automatically evidence that the same answer applies to a new context.

A conceptual processing path is:

```text
User input
  -> perception and task routing
  -> retrieval / capability planning / candidate generation
  -> evidence assessment
  -> reasoning and simulation
  -> answer / decision governance
  -> response
  -> reflection and experience recording
  -> admission-controlled later reuse
```

This is a conceptual abstraction. It does not imply that every named step executes for every request, or that each module is publicly available for inspection.

## 3. Governed experience model

### 3.1 Persistence is not promotion

Storing an event is different from declaring the event reliable. An experience record may preserve context for debugging, audit, or later analysis while remaining ineligible to supply factual authority. The architecture aims to avoid automatic promotion of model outputs and unverified external text into trusted memory.

### 3.2 Eligibility and provenance

A candidate experience consumer should check at minimum:

- provenance and origin of the record;
- the original claim's evaluation state and later amendments;
- whether the record has been rejected, disputed, blocked, excluded, contested, superseded, or conflicted;
- the intended downstream use (narrative context, factual evidence, planning hint, or tool proposal);
- resource and recursion limits;
- the authority of the current policy and verification path.

The exact data schema and implementation details of the private V4 development tree are outside the scope of this public paper.

### 3.3 Denial must survive retrieval

A critical requirement is that retrieving a record cannot erase a previous denial decision. A denied record may remain visible for audit or conflict explanation, but it should not silently become a supporting fact simply because it has reappeared in a search result.

### 3.4 Model and tool roles

An optional LLM may propose candidate wording, interpretations, or solution paths. Tool outputs likewise supply candidate observations. Neither role, by itself, should create authority to overwrite governance state. Admission rules remain outside candidate-generation components.

## 4. Prototype development checkpoints

The following observations are drawn from local Project Clair development reports. The associated executable source revisions, test fixtures, environmental manifests, and complete raw outputs are not published with this manuscript. **They are not independent verification.**

| Date / checkpoint | Developer-reported observation | Interpretation limit |
| --- | --- | --- |
| Earlier V3 public restoration | 416 passed, 1 skipped | Historical smoke tests; different codebase scope |
| August 2026 REIL adapter-era checkpoint | 2,854 passed, 4 skipped | Broad smoke count, not an experience-learning benchmark |
| October 7, 2026 combined checkpoint | 62 passed | Targeted regression subset |
| October 9, 2026 EXP-003 R16 | 20/20 checks passed | Authority-boundary regression, not full generalization |
| October 9, 2026 local-network tester | Health HTTP 200 and identity verified | Connectivity/identity evidence, not cognition evidence |

The October 9 authority regression reportedly denied multiple disallowed categories, including rejected, disputed, blocked, superseded, contested, excluded, conflicting and nested-rejected records; two fallback cases were preserved. Categories can overlap and the reported 20 checks should not be interpreted as 20 statistically independent experiments.

As of October 12, 2026, the experience consumer integration and its end-to-end operational impact remain under investigation. A successful boundary test does not prove that a complete agent consistently selects, consumes, and learns from past experience.

## 5. Proposed experimental evaluation

A stronger evaluation should compare at least two configurations on identical prompts and seeded histories:

- **Baseline:** retrieval of past episodes without downstream authority-state enforcement.
- **Governed:** identical candidate retrieval with explicit provenance, state, and admissibility enforcement.

Measure (1) false admission of denied evidence; (2) legitimate retrieval retention; (3) contradiction handling after correction; (4) performance across restarts; (5) latency and memory overhead; and (6) answer quality on held-out tasks. Report denominators, uncertainty, and failures, not merely passing counts. Include adversarial cases where a plausible, repeatedly retrieved false statement is later rejected.

For replicability, future releases should provide commit hashes, environment versions, fixture generators, test scripts, redacted event traces, and a mapping between expected outcomes and policy decisions. The experiment should distinguish structural gating from semantic correctness: denying a flagged item does not prove that accepted evidence is true.

## 6. Threats to validity

**Internal validity:** tests may encode the desired rule too directly and therefore fail to detect unanticipated bypasses. **External validity:** handcrafted state categories may not generalize to realistic conversations or malicious documents. **Construct validity:** a pass/fail authority test is not a direct measure of cognition, autonomy, learning, or alignment. **Reproducibility:** private source and unshared test reports currently prevent independent audit. **Security:** private-LAN operation and identity checks alone are not equivalent to security assurance.

We also do not assert that the described mechanisms are unique to Clair or unprecedented in academic or industrial systems. Prior work on agent memory, provenance, event sourcing, and policy enforcement must be reviewed systematically before any priority or novelty claim.

## 7. Discussion

The contribution proposed here is an integration discipline: experience is useful only in relation to recorded origin, subsequent assessments, and explicit authority constraints. Local-first operation may help users control data and runtime deployment, but makes durable governance and audit particularly important. A successful implementation would provide a testable boundary between what an agent remembers happening and what it is justified in believing.

This is an architectural case study and proposed evaluation framework, not proof that the architecture achieves the desired properties in unconstrained environments.

## 8. Conclusion

Project Clair's prototype development suggests a practical research direction: experience persistence and retrieval should not imply epistemic admission. The reported authority-boundary regressions are a preliminary signal that specific denial rules can be enforced in local tests. Claims of reliable long-term learning, broad correctness gains, or superior performance must await end-to-end experiments and independent replication.

## Availability and citation

**Code and supporting materials:** [Project Clair public repository](https://github.com/bhilton114/Clair_v.3). The current private V4 implementation and the full raw reports underlying this manuscript are not included.  
**Competing interests:** None declared by the author in this manuscript draft; author to confirm before formal release.  
**Funding:** Not specified.  
**Ethics and privacy:** No human-subject data is presented.

### Suggested citation after release on a stable public revision

Hilton, B. (2026). *Governed Experience Reuse in a Local-First Cognitive Agent: Architecture, Authority Boundaries, and Preliminary Regression Evidence* (Version 0.1, technical preprint). Project Clair. [Stable public release URL or DOI to be inserted after publication].

**Editorial note:** GitHub pull-request URLs are review artifacts, not ideal archival citations. For ORCID, use a released public version with a stable URL, ideally a Zenodo DOI if a repository snapshot is deposited there.

## References and related work to establish before formal scholarly submission

A formal literature review remains to be completed. Areas to cite and differentiate include event sourcing and immutable logs, data provenance, retrieval-augmented generation, agent memory architectures, and policy-based access control. This manuscript intentionally does not invent bibliographic references or imply priority over existing methods.
