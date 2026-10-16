Here is a reference guide and structured hints designed to help you unblock yourself if you get stuck at any phase of this project.

---

## Phase 1: Data Engineering & Relational Setup

### 💡 Hints & Concepts

* **Synthetic Data Generation:** If you need to build the dataset yourself, use Python (`pandas`, `numpy`, and `faker`). Generate a 12-month timeline per customer to observe monthly statement generation cycles.
* **Joining Fact and Dimension Tables:** Ensure primary-foreign key relationships are maintained across `customer_id` when joining transaction data with monthly billing statements.

### ❓ Self-Reflection Questions to Move Forward

1. *Do I have a full 12-month history for each customer, or are there missing billing cycles?*
2. *Is my transaction log generated before or after statement generation dates?*

---

