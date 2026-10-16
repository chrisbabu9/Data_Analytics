# **Business Case Brief: Credit Card Portfolio Risk & Revolver Migration Analysis**

**To:** Senior Data Analyst, Risk & Portfolio Analytics (Albert Charles Palathingal)

**From:** Head of Risk Analytics

**Date:** October 17, 2026

**Subject:** Q4 Portfolio Review: Behavioral Risk Segmentation & Revolver Migration

---

### **1. Executive Summary & Business Context**

Over the last two quarters, our retail credit card portfolio has seen an unexpected compression in net interest margins coupled with an uptick in early-stage delinquencies. While our total billing volume is growing, executive leadership is concerned about the shifting ratio of **transactors** (customers who pay their full statement balance within the grace period) versus **chronic revolvers** (customers who consistently pay only the Minimum Amount Due).

We need an analytical deep-dive into customer payment habits, credit utilization velocity, and behavioral transition states. The objective is to identify leading indicators that signal when a healthy transactor or low-risk borrower is about to transition into high-risk revolver behavior or potential default.

---

### **2. Available Data Landscape**

Your data engineering counterparts have provisioned a staging environment containing three core relational tables. Due to regulatory compliance and data governance policies, raw Personally Identifiable Information (PII) has been scrubbed or hashed.

* **`dim_customers` (Customer Master)**
* `customer_id` (PK, String)
* `signup_date` (Date)
* `credit_limit` (Decimal)
* `income_bracket` (Categorical: Low, Medium, High, Unverified)
* `risk_tier_initial` (Categorical assigned at onboarding)


* **`fact_statements` (Monthly Billing Ledger)**
* `statement_id` (PK, String)
* `customer_id` (FK, String)
* `statement_date` (Date - generated monthly)
* `total_billed_amount` (Decimal)
* `min_amount_due` (Decimal - calculated via 5% principal + 100% fees/EMIs rule)
* `amount_paid` (Decimal)
* `payment_date` (Timestamp)
* `overlimit_flag` (Boolean)


* **`fact_transactions` (Transactional Log)**
* `txn_id` (PK, String)
* `customer_id` (FK, String)
* `txn_timestamp` (Timestamp)
* `merchant_category` (Categorical: Retail, Travel, Dining, Cash Advance, Utility)
* `txn_amount` (Decimal)
* `settlement_status` (Categorical: Settled, Pending, Disputed)



---

### **3. Key Business Objectives & Questions to Address**

When you present your findings to the Risk Committee next month, your analysis must address the following core problems:

1. **Behavioral Segmentation & Profiling:**
* How can we accurately classify our active customer base into distinct behavioral tiers (e.g., Transactors, Chronic Revolvers, Delinquent Risks) based on their historical payment timeliness and credit utilization ratios over a 12-month rolling window?


2. **Migration Patterns:**
* What is the typical lifecycle or transition path of a customer? Specifically, how many billing cycles does it take on average for a customer to transition from a full payer to paying only the Minimum Amount Due for 3 consecutive months?


3. **Leading Indicators of Default Risk:**
* Are there specific triggers—such as sudden spikes in credit utilization velocity, shifts toward cash advances, or paying the minimum due past the optimal payment window—that correlate most strongly with an account defaulting within the next 90 days?


4. **Portfolio Exposure Impact:**
* What is the total outstanding exposure currently locked up in accounts showing chronic revolver patterns, and how does this impact our projected portfolio loss provisions?



---

### **4. Constraints & Technical Requirements**

* **Data Scale & Performance:** The raw transaction log contains over 45 million rows. Your data extraction and transformation pipeline must be optimized to handle large datasets efficiently without timing out our staging warehouse.
* **Handling Missing & Messy Data:** Expect instances of late payment settlements, delayed transaction postings, and unverified income fields. Your analysis must explicitly document how you handle edge cases (e.g., accounts with zero utilization, dormant cards, or partial payments that fall slightly below the calculated Minimum Amount Due).
* **Reproducibility:** All analytical transformations, feature engineering pipelines, and clustering or predictive logic must be fully reproducible via clean, modular code and documented schema definitions.
* **Output Format:** Leadership expects an executive summary memo paired with an interactive prototype or dashboard layout that allows risk managers to filter accounts by utilization brackets and behavioral risk tiers dynamically.