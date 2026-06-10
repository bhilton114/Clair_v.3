# Project Clair V3.4

**Cognitive Learning and Interactive Reasoner**

Project Clair is an experimental AI reasoning architecture focused on resourcefulness, verification, memory discipline, and safe answer formation.

Clair is not designed as a simple chatbot wrapper. The goal is to build a modular cognitive reasoning system that can detect what a task needs, plan by capability, retrieve or inspect supporting information, evaluate evidence, gate answers, and avoid treating unsupported claims as trusted memory.

Current restoration status:

```text
Full Smoke Suite: 416 passed, 1 skipped
RESTORE-020A: Closed
```

---

## Project Overview

Clair is a personal research prototype exploring how an AI assistant can reason through tasks using structured cognitive loops rather than direct single-pass responses.

The current architecture focuses on:

* resourceful task handling
* capability-based planning
* evidence-supported answering
* fallback recovery
* document-first reasoning
* verification-aware memory
* answer safety gates
* structured memory recall
* modular reasoning components

The long-term goal is to develop Clair into a governed cognitive assistant capable of learning, verifying, recovering from missing information, and explaining uncertainty.

---

## Current Milestone

Clair V3.3 recently completed a major resourcefulness restoration pass.

Final smoke result:

```text
416 passed, 1 skipped, 60 warnings
```

The warnings are currently test-hygiene warnings from pytest where some smoke tests return diagnostic objects instead of `None`. They do not represent failing behavior.

---

## What Clair Can Currently Handle

The current system includes passing smoke coverage for:

### Public Fact Lookup

Clair can route public fact questions through a resourcefulness pipeline that detects the need for support, plans a capability path, coordinates lookup/fetch behavior, scores evidence, and gates the final answer.

Example task types:

* headquarters lookup
* population lookup
* software version lookup
* current role lookup
* claim verification

---

### Ownership and Relation Validation

Clair can distinguish between different relationship types instead of treating nearby entities as interchangeable.

Supported relation-style tasks include:

* owner
* founder
* CEO
* operator
* maintainer
* publisher
* acquirer

The system is designed to reject role confusion such as:

```text
CEO ≠ owner
founder ≠ current owner
operator ≠ maintainer
publisher ≠ developer
investor ≠ owner
```

---

### Document-First Reasoning

Clair can answer from provided document context before falling back to other sources.

Expected behavior:

```text
If the answer is in the document, answer from the document.
If the answer is not in the document, report what source/context was checked.
```

This is part of Clair’s context-discipline restoration work.

---

### Fallback and Recovery

Clair includes fallback behavior for missing or failed resources.

The system can:

* continue after weak evidence
* try alternate resource paths
* report unsupported answers instead of inventing them
* distinguish missing-resource failures from answer failures

---

### Verification-Aware Memory

Clair includes a memory policy layer that treats facts differently based on evidence and verification state.

Supported memory states include:

* verified
* provisional
* conflicted
* rejected / blocked

The goal is to prevent unsupported or contradicted claims from becoming trusted memory.

---

## High-Level Architecture

Clair V3.3 is organized around a resourcefulness reasoning spine:

```text
NeedDetector
→ CapabilityPlanner
→ ResourcefulnessCoordinator
→ Tool / Source Attempt Path
→ EvidenceScorer
→ AnswerGate
→ ReasoningEngine
→ Memory / Reflection
```

Each stage has a specific responsibility:

| Component                  | Purpose                                             |
| -------------------------- | --------------------------------------------------- |
| NeedDetector               | Detects what the user request requires              |
| CapabilityPlanner          | Plans by capability rather than hardcoded tool      |
| ResourcefulnessCoordinator | Coordinates lookup, fallback, and recovery attempts |
| EvidenceScorer             | Scores source support and relevance                 |
| AnswerGate                 | Blocks weak, unsupported, or unsafe answers         |
| ReasoningEngine            | Produces structured answers from supported context  |
| Memory Policy              | Controls what can be stored or trusted              |
| Reflection                 | Records useful execution and learning traces        |

---

## Design Goals

Project Clair is built around several guiding principles:

### 1. Resourcefulness Over Guessing

Clair should detect when it lacks information and attempt to find support instead of guessing.

### 2. Verification Before Trust

Clair should not treat claims as trusted memory unless they pass the appropriate verification or governance checks.

### 3. Capability-Based Design

Clair should plan around capabilities, not just individual tools. This makes the system easier to extend and less brittle.

### 4. Safe Failure

When Clair cannot support an answer, it should fail cleanly and explain the limitation.

### 5. Modular Growth

Each component should solve a reusable class of problems rather than hardcoding benchmark answers.

---

## Current Test Coverage

The current smoke suite covers the restored reasoning and resourcefulness surface.

Confirmed stable paths include:

* document answer extraction
* document context discipline
* fallback ladder recovery
* fallback exhaustion reporting
* resourcefulness end-to-end regression
* owner attribute validation
* owner AnswerGate integration
* relation attribute distinction
* relation capability planning
* relation query shaping
* public fact spine
* source quality and canonical preference
* orchestrator packet flow
* reasoning path smoke
* wordplay reasoning
* structured memory recall
* verification-aware memory learning
* verification memory bridge
* verification memory policy bridge

Run the smoke suite:

```powershell
python -m pytest Tests/Smoke
```

Expected current result:

```text
416 passed, 1 skipped
```

---

## Example Test Commands

Run the orchestrator flow smoke test:

```powershell
python -m pytest Tests/Smoke/test_v3_orchestrator_flow.py
```

Run the resourcefulness end-to-end regression:

```powershell
python -m pytest Tests/Smoke/test_full_resourcefulness_end_to_end_regression.py
```

Run the verification memory bridge tests:

```powershell
python -m pytest Tests/Smoke/test_verification_memory_bridge_storage_path.py
```

Run the full smoke suite:

```powershell
python -m pytest Tests/Smoke
```

---

## Project Status

Clair V3.3 is currently a research prototype.

Current state:

```text
Status: Active development
Milestone: RESTORE-020A closed
Smoke stability: Passing
Primary focus: Resourcefulness, verification, memory governance, and runtime validation
```

The project is not yet packaged as a commercial product. The next work phase is focused on runtime validation, demo cleanup, documentation, and clearer public presentation.

---

## Recent Milestone: RESTORE-020A

RESTORE-020A closed the full smoke compatibility cleanup after the resourcefulness restoration work.

The main issue resolved during this cleanup was an older smoke-test assumption that confused interaction-history records with semantic memory records. The test contract was updated to distinguish between those record types.

Final result:

```text
416 passed, 1 skipped, 60 warnings
```

This confirms that the restored architecture and the older smoke surface now agree again.

---

## Current Limitations

Clair is still early-stage and should be treated as an experimental system.

Known limitations:

* not yet packaged for simple installation
* runtime UI validation is still ongoing
* broad open-web research is still limited by available tool integrations
* some tests still return diagnostic objects, creating pytest warnings
* not yet optimized for production deployment
* documentation is still being expanded

---

## Roadmap

Near-term goals:

* clean remaining pytest return-value warnings
* validate live runtime behavior against smoke-tested paths
* improve demo flow
* improve setup documentation
* package a clearer technical overview
* continue reducing benchmark-shaped logic
* strengthen memory governance and source verification
* expand public fact and document reasoning coverage

Longer-term goals:

* improve autonomous recovery behavior
* expand capability registry
* improve source quality ranking
* strengthen reflection and learning loops
* create a cleaner public demo
* continue moving toward a governed cognitive assistant architecture

---

## Philosophy

Project Clair is built on the idea that an AI assistant should not simply answer. It should reason about what the task requires, determine what information is missing, seek support when needed, evaluate that support, and explain when it cannot answer safely.

The project is not only about producing answers. It is about building a system that can recover, verify, remember responsibly, and improve through structured reasoning.

---

## Repository Note

This repository represents an active prototype and research build. Some files may change quickly as the architecture is restored, tested, and cleaned.

The current public focus is on showing the architecture, test stability, and design direction without exposing private or sensitive project material.

---

## Author

Built by Blake Hilton as part of Project Clair.
