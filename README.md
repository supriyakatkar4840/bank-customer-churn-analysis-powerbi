# Bank Customer Churn Analysis (Power BI + Python)

End-to-end churn analysis of 10,000 retail-bank customers: data cleaning, 10 business questions, KPI dashboard and recommendations.

![Dashboard preview](images/dashboard_preview.png)

## Key findings
* Overall churn: **20.38%** (2,038 / 10,000)
* **Germany** 32.4% vs France 16.2% / Spain 16.7%
* **Female** 25.1% vs Male 16.5%
* **Age 46-55** 50.6% and 56-65 48.3% vs ~8% under 35
* **2 products** = 7.6% churn; **3-4 products** = 83-100%
* **Inactive** members 26.9% vs active 14.3%
* **High balance (>100K)** 25.2% vs 15.9%
* Tenure has almost no effect (17-23%)

Full write-up: [REPORT.md](REPORT.md)

## Repository structure
```
bank-churn-powerbi/
|-- data/            Customer-Churn-Records.csv
|-- python/          churn_analysis.py   (answers Q1-Q9, makes charts)
|-- powerbi/         DAX_measures.md, POWERBI_BUILD_GUIDE.md, Bank_Churn_Dashboard.pbix
|-- images/          charts + dashboard screenshots
|-- outputs/         summary tables (CSV)
|-- REPORT.md
|-- requirements.txt
```

## How to run
```bash
git clone https://github.com/<your-username>/bank-churn-powerbi.git
cd bank-churn-powerbi
pip install -r requirements.txt
python python/churn_analysis.py
```
For the dashboard open `powerbi/Bank_Churn_Dashboard.pbix` in Power BI Desktop (or follow `powerbi/POWERBI_BUILD_GUIDE.md`).

## Skills demonstrated
Power BI, DAX, Power Query, data cleaning, KPI design, storytelling with data, Python (pandas, matplotlib).

## Author
Supriya Katkar - [LinkedIn](https://linkedin.com/in/your-profile)
