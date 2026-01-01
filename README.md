# Project 1: ATM Downtime Report Automation 🏧
### Migration of Legacy Excel Logic to Python (Rule-Based Engine V1.0)

## 🎯 Project Summary
This project documents a Data Engineering case study: migrating a complex **Business Logic Engine** from Microsoft Excel to **Python**.

In my current role at Bank Permata (IT Ops), I handle daily ATM downtime reports. The process involves receiving 100+ raw, unstructured text reports from field teams. Previously, I used a complex 3-step Excel engine (nested `IF/SEARCH/AND/OR` formulas) to process this data.

**The Goal:**
I translated the Excel engine 1:1 into a Python script (Pandas/NumPy) to prove that Python is faster, more scalable, and easier to maintain than Excel.

### 🚀 Key Achievement (Impact)
* **Efficiency Boost:** Reduced reporting time by **50%** (from **60 minutes** manually to **30 minutes** with this script).
* **Reliability:** Eliminated human error in manual data entry using VLOOKUP logic.

---

## 🛠️ Tools & Data
* **Language:** Python 3.10+
* **Libraries:** Pandas, NumPy
* **Environment:** Jupyter Notebook / Google Colab
* **Dataset:** `data_atm_downtime_FINAL.csv`
    * *Note: This is a dummy dataset containing 100 rows of "dirty" data designed to replicate real-world field reports (e.g., typos, misplaced commas, inconsistent formatting).*

---

## ⚙️ The V1.0 Architecture (Rule-Based)
This Python script mimics the original Excel workflow using a **3-Pipeline Approach**:

1.  **Pipeline 1 (Text Classification):**
    * Reads raw text from `Cause` (Column M).
    * Classifies it into `N_Real_Problem` using keyword matching (Python version of Excel's `SEARCH`).
2.  **Pipeline 2 (Category Mapping):**
    * Maps `N_Real_Problem` to `P_Category` (Column P).
    * *Logic:* Equivalent to Excel's `VLOOKUP`.
3.  **Pipeline 3 (Business Logic):**
    * Determines the final `Q_Responsibility` based on Category AND System Owner data.
    * *Logic:* Equivalent to Excel's `IF` + `AND`.

---

## ⚠️ Critical Findings & Fatal Flaws (QA Analysis)
While the migration was successful, this project exposed two **fundamental flaws** in the V1.0 Rule-Based approach. As a QA enthusiast, I identified these edge cases:

**1. Logical Flaw: Dependency on Priority Order**
The engine executes rules strictly from top to bottom, leading to "false positives."
* *Input:* "Open ticket to Network Team"
* *V1.0 Result:* Classified as **"Network Issue"** (matched keyword "Network").
* *Expected Result:* **"On-Progress"** (should prioritize "Open ticket" action).

**2. Technical Flaw: Non-Robust against "Dirty Data"**
The engine fails when input data isn't 100% clean.
* *Scenario:* A misplaced comma (e.g., "Electricity, shop closed") shifts the dataframe alignment.
* *Result:* The engine crashes or misidentifies the issue entirely (e.g., reading "Shop Closed" as "Restart Machine").
* *Conclusion:* A rule-based system is too brittle for production without heavy data cleaning.

---

## 🔮 Future Roadmap: Bridge to Project 2
This project proved that **Rule-Based Engine V1.0 is not good enough** for scaling. It is brittle and lacks context awareness.

This justifies the need for **Project 2: The Intelligent Engine (V2.0)**.
I plan to build a V2.0 using **Machine Learning (NLP)** to create a classifier that is:
* **Context-Aware:** Understands that "Open ticket" implies an action, regardless of word order.
* **Robust:** Can handle dirty data without crashing.

---

## 📬 Contact
Thank you for reviewing my code! I am currently transitioning into Quality Assurance & Data roles.

* **LinkedIn:** [Antonius Rildo](https://www.linkedin.com/in/antonius-rildo-232b9411a/)
