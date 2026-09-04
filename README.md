# Telecom Customer Churn — End-to-End Analysis & Prediction

End-to-end churn analytics project: SQL/Python EDA → ML churn prediction → Power BI dashboards, built on a 6,400+ row telecom customer dataset. Goal: not just visualize churn, but build something a retention team could actually act on — who's at risk, why, and how much revenue is on the line.

##  Dashboards

### Summary Dashboard
<img width="1163" height="652" alt="image" src="https://github.com/user-attachments/assets/8bb5cc0c-1d1d-4b84-a441-0318f0fcd985" />

Churn breakdown by demographics, geography, services, contract, and payment method.

### Prediction Dashboard
<img width="1156" height="648" alt="image" src="https://github.com/user-attachments/assets/aca5c94b-f38c-4de2-b54e-6db22291363b" />

Model-driven churn-risk scoring — high-chance churners flagged, ranked by revenue and tenure, with profile breakdowns (age, contract, state, marital status).

Both dashboards use a custom Airtel-brand (red/white/grey) Power BI theme — see `dashboard/airtel_theme.json`.

##  Key Findings
- Month-to-month contracts drive **47%** of churn vs just **3%** for two-year plans
- Competitor switching is the **#1 churn category** (218 cases)
- Jammu & Kashmir has the highest state-level churn rate (**57%**)
- **₹1.6M+** in revenue sits with customers flagged as high churn-risk
- Of currently active ("Stayed") customers, the model flags **240** with a predicted churn probability above 60%
- Churned customers pay a **higher average monthly charge** than retained customers — churn isn't purely a low-value-customer problem

##  Churn Prediction Model
- Models compared: Logistic Regression, Random Forest, XGBoost
- **XGBoost**: 77% recall / 66% precision on the Churned class, ROC-AUC ~0.89
- Leakage-safe: `Churn_Category`/`Churn_Reason` excluded as features (only known post-churn)
- `Joined` (new) customers excluded from training, scored separately as an early-warning list

##  Business Recommendations
Framed against real retention strategies in the Indian telecom market (Airtel, Jio):

| Finding | Real-world parallel | Recommendation |
|---|---|---|
| Month-to-month = 47% of churn | Jio's Prime relaunch price-locks users for 12 months | Offer a 12-month rate lock to month-to-month customers instead of a generic discount |
| "Competitor" is the #1 churn reason | Airtel countered switching with data rollover & better service | Trigger a matched-offer retention call before renewal for high-risk customers with a "Competitor" churn history |
| Customers with 0 add-ons churn more | Airtel grew ARPU via bundling, not price cuts | Bundle add-ons (security/streaming) free for 3 months to high-value at risk customers instead of discounting |
| J&K, Assam, Jharkhand top churn-by-state | Retention is a resource-allocation problem, not one national policy | Regional triage — states above a churn threshold get proactive outreach + service-quality audits |
| Churned customers pay more on average | — | High-paying customers churning signals a value/perception gap, not a price problem — prioritize service quality checks for this segment before offering discounts |

##  Tools & Tech
- **SQL** — data quality checks, churn-rate segmentation queries
- **Python** — pandas, seaborn/matplotlib, scikit-learn, XGBoost
- **Power BI** — dashboard design, DAX measures, custom Airtel theme

##  Repo Structure
```
├── notebooks/
│   ├── churn_analysis_fixed.ipynb      # EDA: cleaning, univariate/bivariate, chi-square, revenue impact
│   └── churn_prediction.ipynb          # ML pipeline: modeling, evaluation, risk scoring
├── data/
│   ├── current_customers_churn_risk.csv
│   └── joined_customers_churn_risk.csv
├── dashboard/
│   ├── summary_dashboard.png
│   ├── prediction_dashboard.png
│   └── airtel_theme.json               # Power BI theme file
└── README.md
```


