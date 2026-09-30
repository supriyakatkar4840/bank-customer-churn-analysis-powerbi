# Bank Customer Churn Analysis - Full Report

**Dataset:** 10,000 retail-bank customers, 18 columns (no missing values, no duplicate `CustomerId`).
**Tools:** Power BI (dashboard, DAX) and Python/pandas (validation of every number).
**Formula:** Churn Rate (%) = (Churned Customers / Total Customers) x 100

## 1. Executive summary
* **20.38%** of customers churned (2,038 of 10,000) - roughly 1 in 5.
* Churn is **concentrated**, not uniform: Germany, female customers, ages 46-65, customers with 3-4 products, inactive members and high-balance customers all churn well above average.
* Tenure, credit-card ownership, card type and satisfaction score barely move churn.
* `Complain` almost perfectly matches churn (99.5% of complainers churned) - treat it as a warning signal / possible data leakage, not a cause to model blindly.

## 2. Answers to the 10 questions

### Q1. Overall churn rate and trend over time
Overall churn = **20.38%** (2,038 churned / 7,962 retained).
*Trend:* the dataset has **no date field**, so a true time trend cannot be built. `Tenure` (0-10 years) is the closest proxy - see Q5. State this as a limitation in the report.

![Q1](images/q1_overall_churn.png)

### Q2. Churn by geography
| Geography | Customers | Churned | Churn rate |
|---|---:|---:|---:|
| France | 5,014 | 811 | 16.17% |
| **Germany** | 2,509 | 814 | **32.44%** |
| Spain | 2,477 | 413 | 16.67% |

Germany holds 25% of customers but **40% of all churners**; its churn is double France/Spain. Germany also has the highest average balance (~119.7K vs ~62K elsewhere).

![Q2](images/q2_geography.png)

### Q3. Gender
| Gender | Customers | Churned | Churn rate |
|---|---:|---:|---:|
| Female | 4,543 | 1,139 | **25.07%** |
| Male | 5,457 | 899 | 16.47% |

Females churn ~1.5x more than males. The gap holds in every country (e.g. Germany: F 37.6% vs M 27.8%).

![Q3](images/q3_gender.png)

### Q4. Age groups
| Age group | Customers | Churn rate |
|---|---:|---:|
| 18-25 | 611 | 7.53% |
| 26-35 | 3,542 | 8.50% |
| 36-45 | 3,736 | 19.65% |
| **46-55** | 1,311 | **50.57%** |
| 56-65 | 536 | 48.32% |
| 65+ | 264 | 13.26% |

Churn jumps sharply after 45: about half of customers aged 46-65 leave. Churned customers average 44.8 years vs 37.4 for retained.

![Q4](images/q4_age_group.png)

### Q5. Tenure
Churn is **flat across tenure** - between 17.2% (7 years) and 23.0% (new customers, 0 years). Slightly higher in the first two years (22-23%), but tenure is **not a strong driver**.

![Q5](images/q5_tenure.png)

### Q6. High-balance customers (> 100K)
* **25.23%** of high-balance customers churned (1,211 of 4,799) vs **15.90%** for balance <= 100K.
* High-balance customers are 48% of the base but **59% of all churners** - the most costly churn, since they hold the money.
* Zero-balance customers (36% of base) churn least (13.82%).

![Q6](images/q6_balance_band.png)

### Q7. Number of products
| Products | Customers | Churn rate |
|---|---:|---:|
| 1 | 5,084 | 27.71% |
| **2** | 4,590 | **7.60%** (healthiest) |
| 3 | 266 | 82.71% |
| 4 | 60 | 100.00% |

Two products is the sweet spot. Customers with 3-4 products churn almost certainly (small groups, but a clear red flag - possible over-selling/bundling problems). Single-product customers are also at risk: cross-sell to a second product.

![Q7](images/q7_products.png)

### Q8. Active vs inactive members
| Status | Customers | Churn rate |
|---|---:|---:|
| Inactive (0) | 4,849 | **26.87%** |
| Active (1) | 5,151 | 14.27% |

Yes - inactive members are **1.9x more likely** to churn. Only 51.5% of customers are active, so re-engagement is a big lever.

![Q8](images/q8_active.png)

### Q9. KPI dashboard
Yes - see `powerbi/POWERBI_BUILD_GUIDE.md` and `powerbi/DAX_measures.md`.
| KPI | Value |
|---|---:|
| Total customers | 10,000 |
| Churned customers | 2,038 |
| Churn rate | 20.38% |
| Average salary | 100,090 |
| Average balance | 76,486 |
| Active users | 5,151 (51.5%) |

![Dashboard](images/dashboard_preview.png)
*(static preview; replace with your Power BI screenshot)*

### Q10. Complete report
This document. Key extra finding:

**Complaints:** 2,044 customers complained; 2,034 of them (99.51%) churned, versus 0.05% (4 of 7,956) of non-complainers. Satisfaction score (1-5) shows no relationship with churn (~20% at every level) - suggesting the score is not capturing real dissatisfaction, and complaints handling is the real signal.

## 3. Highest-risk segment
Combine the drivers: **German, female, aged 46-65, inactive, with high balance**. Germany + inactive alone is 41% churn vs 24% for active Germans.

## 4. Recommendations
1. **Germany deep-dive and retention campaign** - review pricing, service and competition there.
2. **Age 45+ proposition** - retirement/wealth products, dedicated relationship managers.
3. **Protect high-balance accounts** - early-warning list, personal outreach, loyalty rates.
4. **Reactivate inactive members** - nudges, offers, app engagement (halving the gap would cut churn noticeably).
5. **Aim for 2 products per customer**; review why 3-4 product holders leave (bundling, fees, mis-selling).
6. **Fix complaint handling** - fast resolution SLA; every complaint is a near-certain churn event.
7. Target women with tailored engagement; investigate why they churn more.

## 5. Limitations & next steps
* No date column -> no true time trend.
* Findings are correlations; churn drivers overlap (e.g. Germany also has higher balances).
* `Complain` may leak the outcome (complaint likely logged at/after exit) - exclude it from predictive models.
* Next: logistic regression / random forest churn model, customer-level risk score in Power BI.
