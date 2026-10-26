# Project Clair

**Cognitive Learning and Interactive Reasoner (Clair)**  
**Research prototype | Local-first AI architecture | Active development**

Project Clair is an independently developed research prototype exploring how an AI assistant can maintain governed memory, distinguish evidence from inference, plan tool use, and improve through bounded experience without delegating its authority to a language model.

The guiding principle is **facts governed, wording flexible**: language models can help generate candidate answers, but separate components govern admissible evidence, memory state, tool selection, and final output.

> **Version notice (October 2026):** The public `Clair_v.3` repository documents an earlier research snapshot. Work on a separately packaged **Clair V4** system has been reported in local test logs. This README summarizes that later direction and selected developer-reported checkpoints; it does **not** mean the V4 source, APK, or runtime is published in this repository.

## What the system is designed to do

- **Local-first execution:** prioritize operation on the user's hardware, including experiments with access over a private local network.
- **Governed memory:** separate working, episodic, and long-term information, with admission rules for what may be recalled or promoted as trusted.
- **Epistemic discipline:** represent uncertainty and distinguish verified, provisional, conflicted, rejected, and unknown claims.
- **Resourceful reasoning:** detect missing capabilities or evidence, attempt bounded retrieval and fallback, and decline to manufacture unsupported results.
- **Planning and simulation:** evaluate candidate actions under explicit limits and verification requirements.
- **Experience-based improvement:** preserve eligible experience traces and investigate controlled consumption of prior outcomes while retaining authority boundaries.
- **LLM-as-tool architecture:** use an optional language model for candidate generation, not as the final authority for identity, memory, or truth.

These are architectural goals and implemented development surfaces, **not** claims that general-purpose autonomous reasoning or safe continual learning has been scientifically demonstrated.

## Architectural overview

```text
User / local-network client
            |
    Input and perception
            |
     Routing / planning
            |
    Evidence + retrieval  <--- optional tools / candidate LLM
            |
  Reasoning and simulation
            |
  Verification / authority gates
            |
         Response
            |
 Reflection / governed experience
            |
  Memory admission + recall policy
```

Representative modules and mechanisms documented in development work include:

| Layer | Examples of responsibilities |
| --- | --- |
| Perception & routing | InputPacket, PerceptionPipeline, ThalamusRouter |
| Memory | WorkingMemory, long-term SQLite store, episodic memory, promotion rules |
| Truth / authority | TruthGovernance, RetrievalPolicy, AnswerGate, DecisionValidator |
| Reasoning | ReasoningEngine, evidence selection, bounded fallback |
| Planning | Simulator, hazard context, action selection |
| Calibration | uncertainty and conflict handling |
| Reflection / experience | experience persistence, retrieval and admissibility boundaries |
| Interfaces | Python server, browser-based tester and experimental Android client |

Module names and details are subject to change. This is a conceptual map, not a complete source inventory or a security audit.

## Selected development checkpoints

The following figures come from developer-run logs and should be treated as **reported local test results**, not independent third-party validation:

| Checkpoint | Reported result | Scope / caveat |
| --- | --- | --- |
| Earlier public V3 restoration | **416 passed, 1 skipped** | Historical smoke suite documented in the original public README |
| V3 packaging-era core smoke | **2,410 passed, 1 skipped** | Developer-reported local checkpoint |
| A7-era expanded smoke | **2,721 passed, 1 skipped** | Developer-reported local checkpoint |
| REIL adapter-era smoke | **2,854 passed, 4 skipped** | Developer-reported local checkpoint |
| October 7, 2026 combined checkpoint | **62 passed** | Targeted regression set, **not** the entire core suite |
| October 9, 2026 experience authority boundary | **20/20 checks passed** | Specific denied-state and fallback regression scenarios |
| October 9, 2026 local-network tester | **HTTP 200 / identity verified** | Developer-reported mobile browser health/tester session |

Test counts from different scopes should **not** be added together or compared as identical benchmarks. Passing automated tests demonstrates behavior on those scenarios, not broader real-world reliability.

## Experimental local-network access

In October 2026, Clair was exercised through a local server and an Android browser-based tester on the same network. An experimental APK interface was also tested. These are development demonstrations, not a public APK release, independent security review, or claim of production readiness.

## Current research questions

1. Can long-lived assistants enforce durable evidence and memory provenance across restarts?
2. How should contradicted, rejected, or superseded evidence be excluded from later reasoning and experience reuse?
3. Can a governed system learn from prior attempts without promoting unverified outputs into fact?
4. Which capabilities generalize beyond scripted or benchmark-shaped test cases?
5. How can local-first systems remain inspectable, usable, and secure when exposed to clients over a private network?

## Roadmap

- Publish a reproducible V4 architecture and test methodology where IP and privacy considerations permit.
- Validate the experience **consumer** path end to end, including provenance, selection, and denied-state cases.
- Re-run capability benchmarks with strict separation between general reasoning and benchmark-specific hardcoding.
- Improve conversation, document ingestion, installation instructions, and tester usability.
- Seek independent technical review and publish carefully scoped research claims.

## Limitations and disclosure

Clair is an **experimental research system**. It is not validated as generally autonomous, continuously self-improving, commercially production-ready, or compliant with any specific regulatory framework. Local test assertions are not external certification. Some development code and artifacts remain unpublished.

Please do not use this repository's historical contents as proof of unpublished V4 implementation details. Research demonstrations should include the code revision, environment, methodology, and evidence required to reproduce their claims.

## Historical V3 snapshot

The earlier public README documented work on resourcefulness, relation validation (e.g., founder versus owner), document-first reasoning, fallback recovery, and verification-aware memory. Its historical checkpoint was `416 passed, 1 skipped` after RESTORE-020A. This repository remains a public reference point for that earlier phase.

## Authorship

**Blake Hilton**  
Independent developer and researcher, Project Clair.

*Last public-overview update: October 12, 2026.*
