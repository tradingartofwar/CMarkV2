# Example Traces (Loop 1)

These example records exist to make the engine’s behavior legible before implementation.

## Format
- `spec/example_traces.jsonl` is JSON Lines (one JSON object per line).
- Each line corresponds to one evaluation of one market at one timestamp.

## What these examples demonstrate
1) Gate 1 refusal stops all downstream computation.
2) Gate 2 refusal is triggered by *any* perturbation collapse.
3) Passing Gate 2 only authorizes `TRADE_ALLOWED` (it does not encode direction, entries, or sizing).

## Non-negotiable
If implementation output cannot match these shapes, the implementation is wrong.
