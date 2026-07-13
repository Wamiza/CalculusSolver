# SLaNg Dataset Report

## 1. Dataset Scale
- **Total Records:** 115,000 unique calculus strings.
- **Data Splits:** 90% Train (103,500), 5% Val (5,750), 5% Test (5,750).

## 2. Rule Coverage
- **Expanded Polynomials:** The synthesizer generates operations representing the calculus power rule, sum rule, constant rule, and partial derivatives.
  - 35,000 single-term power rule problems
  - 25,000 multi-term polynomials (sum rule)
  - 10,000 constant terms
  - 10,000 negative exponent problems
  - 20,000 multi-variable partial derivatives (using `x`, `y`, `z`)
- **Trig/Exp/Log Support (Phase 2):** Added support for non-polynomial functions using vocabulary v1.2's OP tokens.
  - 5,000 trigonometric `sin` differentiation problems (derivative outputs `cos`)
  - 5,000 exponential `exp` differentiation problems
  - 5,000 logarithmic `ln` differentiation problems
- **Envelope Format:** Real SLaNg representation (no legacy `"type"` or `"terms"` wrappers on input math expressions).
- **Constraints:**
  - Coefficient ($\text{coeff}$) range: $[-10, 12]$
  - Power/Exponent ($\text{power}$) range: $[-3, 5]$
  - Variables: `x`, `y`, `z`

## 3. Limitations & Gaps
- **Cos/Tan Derivatives:** `cos` and `tan` differentiation are excluded because their correct analytical derivatives ($-\sin(x)$ and $\sec^2(x)$) cannot be represented without introducing a sign/coefficient field on operation nodes or a `sec` token, neither of which exists in the `slang_serializer.py` schema today.