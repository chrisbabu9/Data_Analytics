## Phase 2: Feature Engineering & SQL Logic

### 💡 Hints & Concepts

* **Credit Utilization Rate:** $\text{Utilization \%} = \frac{\text{Total Billed Amount}}{\text{Credit Limit}} \times 100$
* **Payment-to-Statement Ratio:** $\text{Payment Ratio} = \frac{\text{Amount Paid}}{\text{Total Billed Amount}}$
* **Identifying Behavioral Tiers:**
* **Transactor:** Payment Ratio $\approx 1.0$ (100% paid).
* **Revolver:** Payment Ratio is close to the Minimum Amount Due ($\approx 0.05$ to $0.10$).
* **Delinquent/Partial:** Payment Ratio $<$ Minimum Amount Due, or `payment_date` $>$ Due Date.


* **Tracking Consecutive Behavior (SQL Window Functions):**
* Use `LAG()` or `LEAD()` over a window ordered by `statement_date` partitioned by `customer_id` to detect multi-month patterns (e.g., paying only MAD for 3 consecutive months).


* **Utilization Velocity:** Calculate the change in utilization over time: $\Delta \text{Utilization} = \text{Utilization}_{\text{Month } t} - \text{Utilization}_{\text{Month } t-1}$.

### ❓ Self-Reflection Questions to Move Forward

1. *Am I correctly isolating transactions that fall strictly between Statement Date $N-1$ and Statement Date $N$?*
2. *How am I handling division by zero for customers with a ₹0 balance or zero limit?*

---

