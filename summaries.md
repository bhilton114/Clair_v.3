# Project Clair General Summary

Project Clair is a personal AI reasoning system built around modular cognition, governed memory, tool/resource use, and evidence-aware answering.

The project began as an attempt to build a private cognitive assistant that could reason, remember, reflect, and eventually support a human user through learning, planning, conversation, and decision-making. Clair is not being designed as a simple chatbot. The goal is to build a reusable reasoning architecture that can detect what a task requires, decide what capability is needed, gather or check information when necessary, evaluate evidence, and avoid unsupported guessing.

## Core Goal

Clair’s long-term goal is to become a governed cognitive reasoner with:

- memory
- reflection
- capability planning
- evidence scoring
- source-supported answers
- safe failure behavior
- reusable reasoning paths
- future support for broader learning and tool use

The project is currently focused on restoring Clair’s core reasoning architecture so that each improvement teaches the system a reusable capability instead of patching individual questions or benchmark tasks.

## Current Architecture Direction

The current restoration architecture is centered around this flow:

NeedDetector → CapabilityPlanner → ResourcefulnessCoordinator → Tool/Source Fetch → EvidenceScorer → AnswerGate → ReasoningEngine → Memory/Reflection

This means Clair should first detect what a user is asking for, identify what capability is required, locate the needed source or tool, evaluate the evidence, and only then produce an answer.

## Current Restoration Phase

Clair V3 is in a restoration phase.

The focus is moving Clair away from benchmark-shaped logic and back toward a general-purpose cognitive reasoning system. The restoration work is centered on making Clair resourceful, evidence-aware, and reusable across many task types.

Recent restoration work confirmed that Clair can now complete source-supported headquarters lookup through the full restored pipeline.

Example confirmed behavior:

> OpenAI is headquartered at 1455 3rd Street, San Francisco, California, U.S.

That answer was produced through the restored path:

NeedDetector → CapabilityPlanner → ResourcefulnessCoordinator → source fetch → EvidenceScorer → AnswerGate

## Confirmed Regression Areas

Current regression coverage includes:

- headquarters lookup
- France population lookup
- Python version lookup
- Apple CEO lookup
- claim verification
- direct math
- owner safe-failure behavior

These tests help confirm that Clair is improving without breaking earlier restored behavior, because apparently software likes to collapse the second you look away from it.

## Current Design Rule

Every update must create reusable capability behavior.

Clair should not be improved through:

- hardcoded answers
- benchmark-only patches
- one-off question fixes
- unsupported memory guessing
- role confusion between owner, founder, CEO, investor, partner, or parent company

The goal is not just to make Clair answer one question correctly. The goal is to teach Clair how to handle a class of questions correctly.

## Next Restoration Target

The next target is:

RESTORE-012: Owner Attribute Validation

The goal is to make questions like:

> Who owns X now?

work through the same source-supported attribute path while rejecting common confusion cases such as:

- founder
- CEO
- investor
- parent company
- partner
- publisher
- operator
- distributor

If Clair cannot verify ownership from source-supported evidence, it should refuse the unsupported answer instead of guessing.

## Project Direction

Clair is being developed as a long-term cognitive architecture project. The current priority is not just adding features, but restoring and strengthening the core reasoning loop so the system can grow without turning into a pile of disconnected patches wearing a trench coat.

The main direction is:

- restore reusable reasoning
- improve source-supported lookup
- protect memory truth
- strengthen evidence gates
- prevent unsupported answers
- keep benchmark logic out of the core
- prepare Clair for broader tool use, learning, and future expansion
