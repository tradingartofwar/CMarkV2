# Market Engine vNext — Gate 1: Regime Classification

## Status

**Gate One is locked.**

This document defines the first irreversible decision in CMarkV2.
Once a market passes or fails Gate One, all downstream logic is constrained accordingly.

No optimization, forecasting, or interpretation may occur before this gate.

---

## Purpose

Gate One exists to answer **one question only**:

> **Is the market in a stable regime where interpretation is allowed?**

If the answer is **NO**, all downstream gates are bypassed.

Gate One does not measure opportunity.
Gate One does not predict direction.
Gate One only determines **interpretability**.

---

## Allowed Regimes (vNext Loop 1)

Gate One classifies the market into **exactly three regimes**.

No additional regimes are permitted in Loop 1.

---

### 1. STABLE_TREND

**Definition**

- Directional movement persists over the evaluation window
- Volatility is bounded
- Structural changes are slow relative to price movement

**Interpretation Allowed:** YES

---

### 2. STABLE_RANGE

**Definition**

- Price oscillates within identifiable bounds
- Mean reversion dominates
- Volatility is moderate and contained

**Interpretation Allowed:** YES

---

### 3. UNSTABLE

**Definition**

- Volatility expansion dominates
- Structure changes faster than interpretation can stabilize
- Regime confidence is low or fractured

**Interpretation Allowed:** NO

---

## Output Contract

Gate One must output:

- `regime_label` ∈ {STABLE_TREND, STABLE_RANGE, UNSTABLE}
- `regime_confidence` ∈ [0, 1]

No additional outputs are permitted.

---

## Hard Constraints

Gate One explicitly forbids:

- prediction
- trade direction
- optimization
- indicator stacking
- narrative interpretation

Any system component that violates these constraints is invalid.

---

## Invariant

> **No interpretation without regime stability.**

This invariant governs all downstream gates.
