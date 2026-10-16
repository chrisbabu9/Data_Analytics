## Phase 3: Behavioral Segmentation & Advanced Analytics

### 💡 Hints & Concepts

* **Clustering Features:** Aggregate monthly data per customer into a summary feature matrix:
* Average utilization % across 12 months.
* Count of months paying only Minimum Amount Due.
* Max utilization spike ($\Delta \text{Utilization}$).
* Cash advance transaction ratio ($\frac{\text{Cash Spend}}{\text{Total Spend}}$).


* **Scaling & Normalization:** Standardize numerical features (e.g., `StandardScaler` in `scikit-learn`) before applying clustering algorithms like K-Means, as unscaled monetary values can distort distance measurements.
* **Transition Matrices / Markov Chains:** To model transition states (e.g., Transactor $\rightarrow$ Revolver $\rightarrow$ Delinquent), count state changes from Month $T$ to Month $T+1$ and build a $3 \times 3$ probability matrix.

### ❓ Self-Reflection Questions to Move Forward

1. *Are my clusters distinct and explainable in plain business language?*
2. *Is high credit utilization correlated with an increased frequency of paying only the minimum due?*

---

