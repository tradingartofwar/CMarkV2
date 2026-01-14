# CMarkV2 — Trace Schema (Minimum Viable)

## Status

**LOCKED for Loop 1.**

This schema defines the minimum fields required to make every refusal legible and replayable.
If the engine cannot produce this record, it is not valid.

---

## Purpose

A trace record answers:

1) **What did the engine decide?**  
2) **Which gate refused, and why?**  
3) **What local stress caused collapse (if Gate 2 ran)?**

The trace is for **inspection and replay**, not optimization.

---

## Trace Record Shape

One evaluation produces **one record** (one JSON object).

### Required Top-Level Fields

- `timestamp` (string, ISO 8601)
- `market_id` (string)

---

## Gate 1 Fields (Required)

- `gate1_regime_label` : `STABLE_TREND | STABLE_RANGE | TRANSITION_UNSTABLE`
- `gate1_regime_confidence` : float in `[0, 1]`
- `gate1_decision` : `ALLOW | REFUSE`

**Rule:** If `gate1_decision == REFUSE`, Gate 2 fields may be omitted or set to `null`.

---

## Gate 2 Fields (Present Only If Gate 1 ALLOW)

### Decision Fields

- `gate2_decision` : `PASS | REFUSE`
- `fragility_score` : float in `[0, 1]`

**Invariant:** `fragility_score` never overrides `gate2_decision`.

### Perturbation Results

- `timescale_results` (object)
  - `N_minus` : `PASS | FAIL`
  - `N_base`  : `PASS | FAIL`
  - `N_plus`  : `PASS | FAIL`

- `volatility_results` (object)
  - `eps_minus` : `PASS | FAIL`
  - `eps_plus`  : `PASS | FAIL`

---

## Refusal Diagnostics (Required If Final Decision is NO_TRADE)

- `refusal_reasons` : list of strings

Examples:
- `"gate1: regime=TRANSITION_UNSTABLE"`
- `"gate1: confidence_below_threshold"`
- `"gate2: fails_timescale_N_plus"`
- `"gate2: fails_volatility_eps_plus"`

---

## Final Output (Required)

- `final_decision` : `TRADE_ALLOWED | NO_TRADE`

**Mapping rule:**
- If Gate 1 REFUSE → `final_decision = NO_TRADE`
- Else if Gate 2 REFUSE → `final_decision = NO_TRADE`
- Else (Gate 2 PASS) → `final_decision = TRADE_ALLOWED`

---

## Notes

- This schema does not include P&L, direction, sizing, or entries.
- Additional fields may be added later only with a version bump and explicit justification.
- Trace must remain readable without code context.

---

## Loop 1 Parameter References (Non-Executable)

Gate 2 parameters are defined in the Gate 2 spec:

- `N = 20 bars`
- `ΔN = ±5 bars` → `N_minus=15`, `N_base=20`, `N_plus=25`
- `ε = ±10%` → `eps_minus=-10%`, `eps_plus=+10%`

These are **spec references**, not runtime configuration.
