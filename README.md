# Clair V3.3

Clair is a solo-built correction-first cognitive agent prototype using three core loops:

- Reasoning: solves tasks and forms candidate answers
- Calibration: checks truth, confidence, and evidence before output or storage
- Maintenance: audits memory, reduces drift, and preserves system health

The goal is to build an inspectable agent architecture that can improve under benchmark pressure without poisoning its own memory.

## Current Status

Experimental prototype. Not production-ready.

## Current GAIA-Style Baseline

- Behavior: 50/50
- Answer quality: 14/50
- Average score: 0.28
- Generic responses: 0
- Unrelated memory errors: 0
- Needs tool/document support: 33

## Why Clair Is Different

Most agent systems focus on acting and remembering.
Clair focuses on correction before memory.

The system is designed around:
- strict module boundaries
- verification-based storage
- correction dominance
- memory governance
- failure-class testing
- benchmark-driven improvement

## Architecture

[Insert diagram here]

## Main System Layers

- Intake
- Perception
- Reasoning
- Calibration
- Planning
- Action Selection
- Execution
- Evaluation
- Reflection
- Memory
- Maintenance

## Roadmap

- Add real PDF extraction
- Add real XLSX extraction
- Improve document support solver
- Reduce tool/document failures
- Push GAIA-style answer quality from 28% toward 55%+
