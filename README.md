# MAVYN Retail Analysis & Business Intelligence

## Graduation Project Submission
**Data Cleaning, Modeling, and interactive Business Intelligence Dashboards**

---

## 👥 Team Members
* **Zyad Mohamed Alaaeldien**
* **Sahar Alaa Mohamed**
* **Mahmoud Osama Khattab**
* **Joyce Nardeen Nabil**
* **Fathy Raed Muhammad**

---

## 📊 Project Overview
This project focuses on analyzing **MAVYN's** global retail fashion chain data to extract strategic business insights. The analysis spans transactional data across **35 physical stores** in **7 countries** (United States, China, Germany, United Kingdom, France, Spain, Portugal) for the time period of **2020 – 2024**.

The source dataset comprises over **6.4 million transactions**, presenting key data engineering, normalization, and visualization challenges.

### Key Project Metrics
* **Total Net Revenue:** $211,956,524.31 (USD)
* **Total Transactions:** 4,540,404
* **Total Units Sold:** 7,060,071
* **Active Customer Base:** 783,217 customers
* **Product Catalog:** 17,940 products
* **Physical Outlets:** 35 stores

---

## 🏗️ Data Architecture (Star Schema)
The analytical model follows a standardized **Star Schema** design in both Power BI and Tableau. The central fact table is `transactions`, linked to five primary dimension tables via Active one-to-many relationships:

```mermaid
erDiagram
    transactions {
        Date Date
        String Invoice_ID FK
        Int Customer_ID FK
        Int Product_ID FK
        Int Store_ID FK
        Int Employee_ID FK
        Decimal Line_Total_USD
        Decimal Invoice_Total_USD
        Decimal Discount
        String Transaction_Type
        String Payment_Method
    }
    customers {
        Int Customer_ID PK
        String Customer_Name
        String Country
        String City
        String Job_Title
        String Job_Category
    }
    products {
        Int Product_ID PK
        String Product_Name
        String Category
        String SubCategory
        Decimal Production_Cost
        Decimal Price
    }
    stores {
        Int Store_ID PK
        String Store_Name
        String Country
        String City
    }
    employees {
        Int Employee_ID PK
        String Employee_Name
        Int Store_ID
    }
    invoices {
        String Invoice_ID PK
        Date Invoice_Date
    }

    transactions }|--|| customers : "Customer ID"
    transactions }|--|| products : "Product ID"
    transactions }|--|| stores : "Store ID"
    transactions }|--|| employees : "Employee ID"
    transactions }|--|| invoices : "Invoice ID"
```

---

## 🗃️ Repository Contents

This repository contains the core deliverables for the MAVYN graduation project:

| File Name | Description |
| :--- | :--- |
| 📊 **[Power BI Dashboard Drive link](Power%20BI%20Dashboard%20Drive%20link)** | **Power BI Desktop Dashboard** hosted on Google Drive (224 MB) — cleaned tables, star schema model, advanced DAX measures, and 11 interactive reporting pages. |
| 📁 **[Raw Data Drive link](Raw%20Data%20Drive%20link)** | Link to the raw CSV source files (transactions, customers, products, stores, discounts, employees) hosted on Google Drive due to their large size (700MB+). |
| 📝 **[MAVYN_Project_Documentation.docx](MAVYN_Project_Documentation.docx)** | **Comprehensive Project Documentation** (Project Planning, Stakeholder Analysis, Requirements, Data Quality Issues & ETL, DAX Formulas, Power BI Dashboards, Excel Analysis, and Final Insights). |
| 🎨 **[Tableau_Project_Documentation.docx](Tableau_Project_Documentation.docx)** | **Tableau Dashboard Documentation** outlining the financial, product, and geographical analysis dashboards built inside Tableau. |
| 💻 **[dax_formulas.txt](dax_formulas.txt)** | **Source Code File** containing all plain-text DAX Calculated Columns and DAX Measures created for analytical reporting (easy for code review directly on GitHub). |

---

## 🛠️ Advanced Analytics & DAX Formulas
All data manipulation and business metrics were calculated using optimized DAX code. Examples of core measures implemented in the model include:

### Average Order Value (AOV)
```dax
AOV = DIVIDE([Total Revenue], [Total transactions], 0)
```

### Customer Lifetime Value (CLV)
```dax
CLV = [AOV] * [Purchase Frequency] * [Gross Margin %] * [AVG CL(month)]
```

### New vs. Returning Customer Classification (Calculated Column)
```dax
Customer Type = 
VAR FirstPurchase =
    CALCULATE(
        MIN(transactions[Date]),
        ALLEXCEPT(transactions, transactions[Customer ID])
    )
RETURN
    IF(transactions[Date] = FirstPurchase, "New", "Returning")
```

> [!NOTE]
> The full source code for all **50+ DAX measures** and **Calculated Columns** is categorized and documented in the **[dax_formulas.txt](dax_formulas.txt)** file.

---

## 💻 Tech Stack
* **BI & Modeling:** Microsoft Power BI Desktop
* **Secondary Visualizations:** Tableau Public
* **Supplementary Analysis:** Microsoft Excel
* **ETL & Data Cleaning:** Power Query (M Language)
