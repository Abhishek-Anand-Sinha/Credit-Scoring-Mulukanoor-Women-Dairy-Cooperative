# The "Milky Way" Alternative Credit Scorecard

### Project Snapshot
**Context:** Rural women in Telangana often face financial exclusion despite having stable cash flows from dairy farming. Commercial banks reject them due to a lack of credit history (CIBIL Score) and formal collateral.
**Goal:** Build a credit risk model for unbanked rural women who lack CIBIL scores but have stable dairy income.
**Outcome:** Developed a Python algorithm that successfully segmented **1,000 women** into 3 risk tiers based on cash flow, asset behavior, literacy level & character.
**Key Finding:** Women investing in *Stree Dhan* (Gold) and *Education* show 30% higher creditworthiness than traditional metrics capture.

---

### 📂 File Structure
* `MWCD_Original_Data.csv`: The raw field data (N=35).
* `mwcd_synthetic_data_generator_py.py`: The Python script for generating 1000 response using Bootstrap Method.
* `MWCD_Synthetic_Data_1000.csv`: The bootstrapped dataset used for modeling.
* `Credit_Score_Algorithm.py`: The Python script containing the scoring logic.
* `MWCD_Scored_Data_Final.csv`: The final output with calculated Credit Scores.
* `Credit_Score_Distribution_Barchart.png`: The Credit Score Distribution Barchart with lending cut-off (55).

---

### 🛠️ The Tech Stack
* **Language:** Python 3.10
* **Libraries:** Pandas (Data Engineering), Seaborn (Visualization), NumPy (Simulation)
* **Data Methodology:** Bootstrapping (N=35 → N=1,000) with continuous noise injection.

---

### 📊 How It Works (The Algorithm)
The model calculates a `MWCD_Credit_Score` (0-100) using a weighted 4-factor logic:

| Factor | Weight | Logic |
| :--- | :--- | :--- |
| **Capacity** | **35%** | **Monthly Cash Flow.** Higher recurring income = higher repayment capacity. |
| **Collateral** | **25%** | **Livestock + Land.** Tangible assets that can be liquidated in default. |
| **Character** | **25%** | **Spending Behavior.** Investing in *Assets/Education* is "Low Risk"; spending on *Food/Subsistence* is "High Risk". |
| **Stability** | **15%** | **Education Level.** Proxy for financial literacy and ability to manage interest. |

---

### ⚙️ From Fieldwork to Fintech: The Data Pipeline

This project simulates a real-world data engineering workflow, moving from raw field data to a scalable product.

#### **Step 1: The Pilot Study (Data Collection)**
* **Context:** Conducted an immersive 8-day field study at *Mulukanoor Women's Cooperative Dairy* (Dec 2025).
* **Sample:** Collected N=35 detailed profiles (Income, Assets, Spending) using stratified random sampling.
* **Result:** Identified key correlations (e.g., High Income → Asset Purchase).

#### **Step 2: Data Standardization (The Codebook)**
* **Problem:** Raw survey data was unstructured text (e.g., "Husband decides money").
* **Solution:** Created a numerical `Codebook` to map categorical variables to integers (`Husband=1`, `Self=0`) for machine processing.

#### **Step 3: The Simulation (Synthetic Data Generation)**
* **Problem:** N=35 is too small for robust modeling.
* **Solution:** Utilized **Bootstrapping with Noise Injection**.
    * Resampled the original dataset to N=1,000 rows.
    * Added statistical noise (+/- 10%) to continuous variables (Income) to ensure realism and prevent overfitting.
    * *Code:* `df.sample(n=1000, replace=True)`

#### **Step 4: The Scoring Engine (Python)**
* Applied the weighted algorithm to the synthetic dataset.
* Segmented users into actionable Risk Tiers:
    * **Tier 1 (Prime):** Score > 75 (Eligible for 10% Interest).
    * **Tier 2 (Standard):** Score 55-75 (Eligible for 14% Interest).
    * **Tier 3 (Sub-Prime):** Score < 55 (Requires Collateral).
 
#### **The Mathematical Logic**
I mathematically differentiated borrowers based on their "Primary Spending" variable:
* **Investor Profile:** Spending on *Asset Purchase / Education* = **100 Points** (Behavior Score)
* **Survival Profile:** Spending on *Food / Loan Repayment* = **30 Points** (Behavior Score)

#### **Impact Analysis (The 17.5 Point Delta)**
Holding all other variables constant (e.g., Income Score = 60), the algorithm produces a significant divergence:

1.  **Woman A (Survival):** $(60 \times 0.35) + (30 \times 0.25) + \dots = \text{Lower Score}$
2.  **Woman B (Investor):** $(60 \times 0.35) + (100 \times 0.25) + \dots = \text{Higher Score}$

**The Result:** The "Investor" behavior contributes a **net lift of +17.5 points** to the final credit score.
> *Impact:* This mathematical adjustment is sufficient to move a borrower from **Tier 2 (Standard - 14% Interest)** to **Tier 1 (Prime - 10% Interest)**, effectively rewarding financial discipline that traditional CIBIL scores miss.

---
*Created by Abhishek Anand Sinha | TISS Hyderabad | Public Policy & Governance*
