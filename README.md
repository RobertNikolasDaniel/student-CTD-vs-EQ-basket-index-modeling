# CTD Basket Equal Carry Index

## Purpose

The CTD (Cheapest-to-Deliver) bond is one of the most important concepts in Treasury futures. It determines the economics of delivery and heavily influences futures pricing.

However, the CTD is only one bond within a much larger delivery basket.

This project explores a simple question:

**Does the CTD generate more financed carry-adjusted total return than the average bond in the delivery basket?**

To answer this, the workbook constructs two carry-adjusted total return indices:

1. **CTD Carry Index** – Tracks the financed carry-adjusted return of the current CTD.
2. **Equal-Weighted Basket Carry Index** – Tracks the financed carry-adjusted return of the entire delivery basket using equal weights.

The difference between these two indices represents a form of **within-basket relative value**, allowing us to study how CTD financing economics compare to the broader delivery universe.

---

## Methodology

### CTD Index

The CTD index tracks only the current Cheapest-to-Deliver bond.

The bond earns carry according to:

[
Spread = Yield - Repo
]

and compounds continuously through time.

### Equal-Weighted Basket Index

Every deliverable bond receives equal weight:

[
Weight_i = \frac{1}{N}
]

where:

* (N) = number of deliverable bonds

The basket measures the average carry-adjusted performance of the entire delivery basket rather than focusing on a single bond.

---

## Inputs

### Global Inputs

| Input | Description        |
| ----- | ------------------ |
| Days  | Investment horizon |

### Per Bond Inputs

| Input       | Description         |
| ----------- | ------------------- |
| Dirty Price | Current dirty price |
| Yield       | Bond yield          |
| Repo        | Financing rate      |

---

## Core Formulas

### Carry Spread

For each bond:

[
Spread_i
========

## Yield_i

Repo_i
]

---

### Projected Total Return Value

Continuous compounding is used to represent reinvestment of earned carry:

[
ProjTRValue_i
=============

Dirty_i
\times
e^{Spread_i \times \frac{Days}{360}}
]

---

### Basket Value

Equal-weight average:

[
Basket_t
========

\frac{
\sum ProjTRValue_i
}{
N
}
]

---

### Starting Basket Value

[
Basket_0
========

\frac{
\sum Dirty_i
}{
N
}
]

---

### Basket Index

The basket index is normalized to the initial CTD dirty price:

[
BasketIndex_t
=============

Dirty_{CTD,0}
\times
\frac{
Basket_t
}{
Basket_0
}
]

---

### CTD Index

For the CTD:

[
CTDIndex_t
==========

Dirty_{CTD,0}
\times
e^{Spread_{CTD}\times\frac{Days}{360}}
]

---

### Relative Value Basis

The relative value spread between the CTD and the basket is defined as:

[
Basis
=====

## CTDIndex_t

BasketIndex_t
]

Interpretation:

* Positive Basis → CTD outperforming basket
* Negative Basis → Basket outperforming CTD

---

## Outputs

### CTD Outputs

* Carry Spread
* Projected Total Return Value
* CTD Index

### Basket Outputs

* Average Carry Spread
* Projected Basket Value
* Basket Index

### Relative Value Outputs

* CTD vs Basket Basis
* CTD Outperformance / Underperformance

---

## Transparency

This model intentionally avoids:

* Conversion factors
* Futures pricing
* Invoice pricing
* Net basis calculations
* Delivery optionality models
* Weighting optimizations

Every assumption is visible and every calculation can be replicated directly from the inputs.

The goal is not to build a trading model.

The goal is to build an intuitive framework for understanding how financing economics differ across the Treasury futures delivery basket.

---

## Lessons Learned

Several observations emerged from building this model:

### The CTD Is Not The Basket

The CTD is often treated as representative of the entire delivery basket.

In reality, each deliverable bond has its own:

* Yield
* Repo rate
* Carry profile

The basket is not homogeneous.

---

### Financing Matters

Small differences in repo rates can create meaningful differences in carry through time.

Two bonds with nearly identical yields may generate very different financed returns.

---

### There May Be A Within-Basket Relative Value Trade

By comparing the CTD against the equal-weight basket, we can observe whether the CTD consistently earns superior carry-adjusted returns.

This suggests that Treasury futures may contain relative value opportunities not only between cash and futures, but also within the delivery basket itself.

---

## Future Improvements

Potential extensions include:

* Real Treasury delivery baskets
* Special repo dynamics
* CTD probability weighting
* Conversion-factor weighting
* Net basis integration
* Historical time-series testing
* Market CTD vs Ideal CTD comparisons

---

## Disclaimer

This project is an educational model intended to explore Treasury futures delivery basket financing dynamics.

It is not investment advice and should not be interpreted as a trading recommendation.
