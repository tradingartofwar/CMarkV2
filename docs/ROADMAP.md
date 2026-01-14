# CMarkV2 Roadmap (Living)

## Project intent
Constraint-first trading engine whose primary function is refusal:
- refuse interpretation in unstable markets
- refuse fragile interpretations
- authorize action only when structure is forced (Gate 3 later)

## What is locked
- Gate 1: regime gating (3 regimes, threshold 0.65, refuse stops all downstream)
- Gate 2: non-fragility (binary PASS/REFUSE; N=20, ΔN=±5, ε=±10%; trace fields defined)

## Current state
- Repo created and synced to GitHub
- Gates 1 & 2 committed
- Trace schema committed
- Example traces committed

## Now
Build the minimal replay harness that:
- loads a price series
- runs Gate 1
- conditionally runs Gate 2
- emits JSONL trace records matching spec/trace_schema.md

## Next step (single move)
Implement Python replay harness in `src/cmarkv2/` and `src/run_replay.py`.

## Not allowed yet
- Gate 3 definition (until replays demonstrate refusal density & stability)
- strategy logic, direction, entries, sizing
- parameter tuning based on outcomes
