**📈Tailwind Traders Power BI Report✅**

[![Power BI](https://img.shields.io/badge/Power%20BI-FF2E00?style=flat&logo=powerbi&logoColor=white)](https://powerbi.microsoft.com/)
[![Excel](https://img.shields.io/badge/Excel-217346?style=flat&logo=microsoft-excel&logoColor=white)](https://www.microsoft.com/en-us/microsoft-365/excel)

---
Here's a README file for your GitHub project, "Tailwind Traders." It provides instructions, explanations, and an overview of the project, including details about the code, tools, and methods used.

---
**Project Overview📊💼**
---

The Power BI report for Tailwind Traders visualizes and analyzes sales and purchase data across countries and products. The report highlights stock levels, purchase quantities, median sales 💰, loyalty points, and trends over time ⏳, providing actionable insights for data-driven decision-making.

---


**Prerequisites**
---
* Power BI Desktop installed.
* Excel files: Tailwind Traders Purchases.xlsx, Tailwind Traders Sales.xlsx, Countries.xlsx.
* (Optional) An "Exchange Data" table or file with exchange rates linked by Exchange ID.

---

**Step 1: Importing and Loading Data 📥**

Power BI Desktop is used to import three Excel files:

1. Purchases.xlsx – Contains PurchaseID, Supplier, Purchase Date, Return Status, Warranty, and other purchase details.

2. Sales.xlsx – Contains OrderID, Product Name, Quantity Purchased, Stock, Profit, Gross Revenue, Loyalty Points, etc.

3. Countries.xlsx – Contains Country ID, Country Name, and Exchange ID 🌍.

An optional Exchange Data table 💱 is imported for currency conversion to USD. Tables are renamed for clarity: Purchases, Sales, Countries.

---

**Step 2: Transforming and Cleaning Data 🧹**

Data is cleaned and prepared using Power Query Editor:

General: Blank rows and duplicates are removed, and headers are promoted.

Purchases: Dates, numbers, and text fields are set to correct data types.

Sales: Numeric and monetary fields are converted, and Country ID is marked as a Country category.

Countries: IDs are converted to numbers, and Country is set as a text field with the Country category.

Currency Conversion: A Sales in USD 💲 table is created by merging Sales with Countries and Exchange Data, calculating Gross Revenue in USD.

---

**Step 3: Creating the Calendar Table 📆**

A Calendar Table is created to enable time intelligence calculations (YTD, QTD, etc.):
```Dax
CalendarTable =
ADDCOLUMNS(
    CALENDAR(DATE(2020,1,1), DATE(2023,12,31)),
    "Year", YEAR([Date]),
    "Month Number", MONTH([Date]),
    "Month", FORMAT([Date], "MMMM"),
    "Quarter", QUARTER([Date]),
    "Weekday", WEEKDAY([Date]),
    "Day", DAY([Date])
)

```
Columns include Year, Month, Month Number, Quarter, Weekday, and Day. The table is marked as a **Date Table** for proper time-based analysis.

---

**Step 4: Building Data Model and Relationships 🔗**

Relationships are established between:

Sales[OrderID] → Purchases[OrderID]

Sales[Country ID] → Countries[Country ID] 🌍

Purchases[Purchase Date] → CalendarTable[Date]

Cross-filter directions are set appropriately, and unnecessary fields are hidden for a cleaner model.

---

**Step 5: Creating DAX Measures 🧮**

**1. Median Sales 💰**
```dax
Median Sales = MEDIAN('Sales in USD'[Gross Revenue USD])

```
Calculates the typical sales value, ignoring outliers.

----

**2. Yearly Profit Margin 📈**
```dax
Yearly Profit Margin = DIVIDE(SUM('Sales in USD'[Profit USD]), SUM('Sales in USD'[Net Revenue USD]))

```
Calculates profit margin safely using **DIVIDE**.

---

**3.Quarterly Profit Margin 💹**
```dax
Quarterly Profit Margin = CALCULATE([Yearly Profit Margin], DATESQTD(CalendarTable[Date]))

```
Calculates profit margin for the current quarter.

---

**4. Year-to-Date Profit 📅**
```dax
YTD Profit = TOTALYTD([Yearly Profit Margin], CalendarTable[Date])

```
Calculates cumulative profit margin from Jan 1 to the current date.

Formatted measures as **Percentage or Currency 💵**.

---

**Step 6: Designing the Report Page 🎨**

The report page is designed with:

**Green-themed color scheme.**

**KPIs**: Stock, Quantity Purchased, Median Sales 💰.

**Visuals**: Loyalty Points by Country, Quantity Sold by Product, Median Sales Distribution, Median Sales Over Time 📈.

**Report Tabs**: Sales Overview & Profit Overview.

**Filters**: Year = 2023.

---

**Step 7: Validating and Publishing ✅**

Refreshed the data 🔄

Tested filters, slicers, and interactions 🧩

Saved as .pbix file 💾 and published to Power BI Service 🌐

---

**Conclusion 🎯**

The report consolidates purchases, sales, and country data into an interactive dashboard, allowing monitoring of sales trends 📈, product performance 🛒, and profit margins 💹, supporting informed business decisions efficiently.

---

**Contributions**

Explore the Power BI dashboard for interactive visualizations: [Tailwind Traders Sales](https://github.com/VickyPatel-MSPI/Tailwind-Traders-Sales/blob/main/Tailwind%20Traders%20Sales.pbix)

---
