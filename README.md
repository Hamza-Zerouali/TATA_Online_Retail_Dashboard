# TATA_Online_Retail_Dashboard

## 📌 Project Overview
This project analyzes the **Online Retail dataset (2010–2011)** containing over **541,000 transactions**. The goal was to clean the raw dataset, calculate revenue, and build dashboards in **Power BI** to answer specific business questions posed by executives (CEO & CMO).

---

## 🛠️ Tools & Skills
- **Power BI** → Data modeling, DAX measures, interactive dashboards  
- **DAX** → Created custom measures like Revenue  
- **Data Cleaning** → Filtering invalid data and handling missing values  
- **Business Analytics** → Turning raw data into actionable insights

---

## 🔧 Data Cleaning & Preparation
- Removed rows where:
  - `Quantity < 1` (invalid sales)
  - `UnitPrice < 0` (negative prices)
- Excluded **cancelled orders** (Invoice numbers starting with "C")  
- Removed rows with missing `CustomerID` when analyzing customers  
- Created a new measure: Revenue = Quantity × UnitPrice
- Verified date formats, customer IDs, and country labels  

---

## 📊 Key Business Questions & Insights

### **Q1 — Monthly Revenue Trend (2011)**
- Built a **line chart** showing monthly revenue for 2011.  
- **Findings:**  
- Sales peaked strongly in **November and December 2011** due to holiday seasonality.  
- Lowest sales occurred around **April–July**.  
- A clear **upward trend at the end of the year** shows seasonality opportunities.  
- **Value for CEO:** Helps in planning inventory and marketing around high-demand months.  

---

### **Q2 — Top 10 Countries by Revenue (excluding UK)**
- Compared **Revenue vs Quantity** for the top 10 non-UK countries.  
- **Findings:**  
- **Netherlands, Germany, and France** had the highest revenues.  
- Some countries (like Ireland) showed **high quantities but lower revenue**, suggesting price sensitivity.  
- **Value for CMO:** Identifies strongest international markets and helps refine pricing strategies.  

---

### **Q3 — Top 10 Customers by Revenue**
- Ranked customers descending by total revenue.  
- **Findings:**  
- A small number of **VIP customers** contributed a **large share of overall revenue**.  
- The top customer’s revenue was **significantly higher** than average.  
- **Value for CMO:** High-value customers should be retained through loyalty programs and targeted offers.  

---

### **Q4 — Demand by Country (excluding UK)**
- Created a **full-view country demand chart** showing all countries without scrolling/hovering.  
- **Findings:**  
- **Europe** dominates in terms of demand.  
- Notable opportunities exist in **Oceania** and **Scandinavia**.  
- **Value for CEO:** Helps evaluate **international expansion** opportunities.

---

## 💡 Summary of Insights
1. **Seasonality** drives sales → strongest in Q4 (holidays).  
2. **Top countries** outside the UK: Netherlands, Germany, France.  
3. **Top customers** generate a major portion of revenue → retention strategies are critical.  
4. **Global demand** suggests expansion potential beyond the UK, especially in Europe and Oceania.

---

## 🧑🏼‍💻 DAX Codes That i Used

### Peak Month Measure:
```
Peak Month = 
VAR MaxRevenue = 
    MAXX(
        SUMMARIZE(
            'Online Retail',
            'Online Retail'[InvoiceDate].[Month],
            "MonthRevenue", SUM('Online Retail'[Revenue])
        ),
        [MonthRevenue]
    )
VAR MaxMonth = 
    MAXX(
        FILTER(
            SUMMARIZE(
                'Online Retail',
                'Online Retail'[InvoiceDate].[Month],
                "MonthRevenue", SUM('Online Retail'[Revenue])
            ),
            [MonthRevenue] = MaxRevenue
        ),
        'Online Retail'[InvoiceDate].[Month]
    )
RETURN
    MaxMonth & ": " & FORMAT(MaxRevenue, "#,##0")
```

### Lowest Month Measure:
```
Lowest Month = 
VAR MinRevenue = 
    MINX(
        SUMMARIZE(
            'Online Retail',
            'Online Retail'[InvoiceDate].[Month],
            "MonthRevenue", SUM('Online Retail'[Revenue])
        ),
        [MonthRevenue]
    )
VAR MinMonth = 
    MAXX(
        FILTER(
            SUMMARIZE(
                'Online Retail',
                'Online Retail'[InvoiceDate].[Month],
                "MonthRevenue", SUM('Online Retail'[Revenue])
            ),
            [MonthRevenue] = MinRevenue
        ),
        'Online Retail'[InvoiceDate].[Month]
    )
RETURN
    MinMonth & ": " & FORMAT(MinRevenue, "#,##0")
```

### Average Month Measure:
```
Average Month Revenue = 
VAR AvgRevenue = 
    AVERAGEX(
        SUMMARIZE(
            'Online Retail',
            'Online Retail'[InvoiceDate].[Month],
            "MonthRevenue", SUM('Online Retail'[Revenue])
        ),
        [MonthRevenue]
    )
RETURN
    "Average: " & FORMAT(AvgRevenue, "#,##0")
```
<img width="1091" height="187" alt="image" src="https://github.com/user-attachments/assets/b8c66d12-7c84-496e-8277-289806a93d39" />

---

## Overview:
### Screenshots
<img width="1302" height="733" alt="image" src="https://github.com/user-attachments/assets/37f47dcd-2ec1-4faf-9754-18c54ab8ab87" />
<img width="1304" height="729" alt="image" src="https://github.com/user-attachments/assets/bb69ceb1-318c-4cae-ae75-f43260c7cc9f" />
<img width="1305" height="730" alt="image" src="https://github.com/user-attachments/assets/4d9bfcc9-53ab-4015-8a1b-4497451c98b4" />
<img width="1302" height="729" alt="image" src="https://github.com/user-attachments/assets/c4acc607-c240-4354-84fa-14d5db9327e5" />

---




