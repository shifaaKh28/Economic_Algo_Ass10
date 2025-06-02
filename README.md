
## Overview

This project solves assignment questions related to the Equal Shares method from Participatory Budgeting.

Specifically, we addressed:
- **Section A** — Demonstrating non-monotonicity (increasing the committee size from k to k+1 causes previously selected candidates to drop out).
- **Section B** — Demonstrating non-monotonicity **without relying on tie-breaking** (there’s always a unique cheapest candidate at each selection step).

---

## What We Did

We implemented a **custom Python script** that simulates the Equal Shares method step by step, printing:
- Initial budgets
- Which candidates are checked each round
- How much each supporter needs to pay
- Which candidates are selected
- How voter budgets update
- Final committee selections

We then compared results between \( k \) and \( k + 1 \) to check if monotonicity holds.

---

## Used Library

We used the [abcvoting Python library](https://github.com/martinlackner/abcvoting)  
specifically to define the `Profile` object and represent the voter approval ballots.

However, we **did not** rely on the library’s internal Equal Shares computations.  
Instead, we implemented our own manual simulation to fully control and track all steps,  
and to avoid hidden tie-breaking mechanisms.

---

## Examples and Results

### **Section A**: Example for Non-Monotonicity

- Voter approvals:
    - Voter 0 → {0, 1}  
    - Voter 1 → {0, 1}  
    - Voter 2 → {2, 3}  
    - Voter 3 → {2, 3}

- Results:
    - For \( k = 2 \):
        - Committee selected: {0, 2}
    - For \( k = 3 \):
        - No candidates can be afforded → committee is ∅

✅ **Non-monotonicity detected**: candidates {0, 2} were selected for \( k = 2 \) but disappeared when increasing to \( k = 3 \).

---

### **Section B**: Non-Monotonicity Without Tie-Breaking

- Voter approvals:
    - Voter 0 → {0}  
    - Voter 1 → {1}  
    - Voter 2 → {1, 2}  
    - Voter 3 → {3}

- Results:
    - For \( k = 2 \):
        - Committee selected: {1}
    - For \( k = 3 \):
        - No candidates can be afforded → committee is ∅

✅ **Non-monotonicity detected without tie-breaking**: candidate {1} was uniquely the cheapest and selected for \( k = 2 \),  
but disappeared when increasing to \( k = 3 \).

---

## How to Run

1️⃣ Install the required library:
```bash
pip install abcvoting
