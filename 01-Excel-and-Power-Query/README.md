# Excel and Power Query Projects

Five data-analysis projects (four individual, one group) built with **Excel, Power Query, the Excel Data Model, and PivotTables/PivotCharts**. Each one starts from raw or messy data, cleans and reshapes it with Power Query, and summarizes it in pivots and charts.

| # | Project | File | Main skills |
|---|---|---|---|
| 1 | [HR Analytics](#1-hr-analytics) | `HRDA-MayarMagdy.xlsx` | Power Query, calculated columns, 18 pivots, 14 charts |
| 2 | [Sales Analysis by Country, Product, and Color](#2-sales-analysis-by-country-product-and-color) | `Project1-DA-MayarMagdy.xlsx` | Multi-table Data Model, calculated sales column, pivots |
| 3 | [Invoice Data Cleaning](#3-invoice-data-cleaning) | `Project2-Invoice-DA-MayarMagdy.xlsx` | Splitting text, append queries, pivots |
| 4 | [Combining Sales Order Files](#4-combining-sales-order-files) | `Project3-DA-MayarMagdy.xlsx` | Folder query, custom function, unpivot |
| 5 | [Grocery Delivery Business Analysis (Group Project)](#5-grocery-delivery-business-analysis-group-project) | `GroupProject-DA.xlsx` | Folder of CSVs, merged queries, 6-sheet analysis |

**Tools:** Microsoft Excel, Power Query (M language), Power Pivot / Data Model, PivotTables, PivotCharts

---

## 1. HR Analytics

**File:** `HRDA-MayarMagdy.xlsx`

### Business questions
The workbook answers 16 HR questions across six sheets: workforce size and status, departments, gender, age, job titles, race and ethnicity, work location, hiring trends, terminations, and turnover.

### Data
An employee-level HR table of **22,214 records** (department, job title, gender, race, birth date, hire date, termination date, location).

### What I did in Power Query
- Imported the CSV and set the correct data types, including dates.
- Split the termination date column and handled blank values.
- Created **Actual Employee Status**: Active, Terminated, or *Future Term Date (Excluded)* for termination dates still in the future.
- Calculated **Age** (against a fixed reference date) and grouped it into **Age Group** bands: <25, 25-35, 36-45, 46-60.
- Calculated **Tenure Years**, **Hire Year**, **Termination Year**, and an **is terminated** flag used for turnover.
- Loaded the result to the Data Model and built the pivots and charts from it.

### Key findings
- **Workforce status:** 18,285 active (82.3%), 2,905 terminated (13.1%), and 1,024 with a future termination date, which I excluded from turnover.
- **Departments:** Engineering is the largest at 6,686 employees (30.1%), followed by Accounting at 3,333 (15.0%).
- **Gender:** Male 11,288 (50.8%), Female 10,321 (46.5%), Non-Conforming 605 (2.7%).
- **Age:** The 46-60 group is the largest at 40.0%, then 25-35 at 29.8%. Only 2.5% of employees are under 25.
- **Race:** White is the largest group at 6,328 employees (28.5%), followed by Two or More Races, Black or African American, and Asian, which are close to each other (about 3,600 each).
- **Hiring:** Between 2001 and 2020, the company hired roughly 1,000 to 1,150 people each year, with about three in four hires at headquarters rather than remote.
- **Terminations:** Terminations rose from 7 in 2001 to a peak of 205 in 2021.
- **Turnover:** The overall rate is about 13%. By department it ranges from 11.1% (Marketing) to 19.2% (Auditing) and 16.7% (Legal). Auditing and Legal are small departments, so a few leavers move the percentage a lot. By race it ranges from 12.2% to 14.6%.

---

## 2. Sales Analysis by Country, Product, and Color

**File:** `Project1-DA-MayarMagdy.xlsx`

### Task
Combine customer, product, and order data to find out what sells, where, and in which colors.

### Data
Three related tables: **Customers** (country, city, and contact details), **Products** (item, size, color), and **Orders** (quantity, unit price, order and delivery dates, status).

### What I did
- Loaded the three tables with Power Query and set the correct data types.
- Added **Total Sales = Quantity × Unit Price** to the Orders query.
- Linked the tables in the **Data Model** so that pivots can mix fields from all three.
- Built pivots of sales by **product**, **product and color**, and **country and product**, with a **Country slicer**, plus a bar chart.

### Key findings
- **Total sales:** 14,472,197 (in the dataset's currency).
- **Top countries:** Saudi Arabia leads with about 5.0M (34.5%), then Syria (3.48M), the UAE (2.57M), Iraq (1.97M), and Egypt (1.45M).
- **Top products:** Tie (2.26M), Jeans (2.20M), and Bag (1.84M) together make up about 43% of sales.
- **Weakest product:** Glasses, at about 155K.
- **Color:** The color pivots show which colors drive each product's sales (for example, red and rose lead among Belts and Coats), which can guide stock decisions.

---

## 3. Invoice Data Cleaning

**File:** `Project2-Invoice-DA-MayarMagdy.xlsx`

### Task
Invoice details arrived as long text strings in a single column. They had to be turned into a clean table that can be analyzed.

### What I did in Power Query
- Split the text column step by step with delimiters (space, tab, `;`, and `-`) and expanded the list into rows.
- Separated each string into **Invoice number**, **Amount**, and **Month**.
- Set data types and renamed the columns.
- Built a second query for the *Months-Increments* variant of the data and combined the results with an **Append** query.
- Summarized amounts by customer, invoice, and month with pivots and two charts.

### Result
A clean table with `Customer ID | Invoice | Amount | Month` for **10 customers** and **94 invoices**, totalling **714,891**.
- The largest customer is `CUST-259700` with about 147K, roughly twice the next customer.
- January is the strongest month (about 78K), followed by October and December. August and September are the weakest.

---

## 4. Combining Sales Order Files

**File:** `Project3-DA-MayarMagdy.xlsx`

### Task
Sales order data was spread across many separate Excel files, each laid out as a cross-tab (dates across columns). The goal was to combine them into one analysis-ready table automatically.

### What I did in Power Query
- Connected to a **folder** of Excel files and combined every workbook and sheet.
- Wrote a reusable **custom function** that, for each sheet, promotes headers, removes empty rows and totals, **unpivots** the date columns into rows, converts the dates, and extracts the year.
- Invoked the function across all files and expanded the result into a single table.
- Built pivots that count the records per territory and metric to check the consolidation.

### Result
One consolidated table covering **8 sales territories** (Australia, Canada, Central, France, Germany, Northwest, Southwest, United Kingdom) and **7 measures** (# Order Details, # Orders, Freight, Qty, Subtotal, Tax Amount, TotalDue), with 171 date records per measure. Adding a new file to the folder and refreshing is enough to update everything.

---

## 5. Grocery Delivery Business Analysis (Group Project)

**File:** `GroupProject-DA.xlsx` | **Team project**

**My contribution:**
- **Understanding the data:** I studied the structure and meaning of each dataset (customers, orders, products, marketing, feedback, delivery, and inventory) to understand how the business works.
- **Designing the relationships:** I worked out how the tables relate to each other and which relationships should be created in the Data Model so orders can be analyzed by customer, product, and category.
- **Analyzing results and business impact:** I interpreted the pivot results and explained what they mean for the business, such as sales performance, delivery delays, customer segments, and marketing returns.
- **Identifying missing information:** I identified which additional data would be needed to get a complete picture of the business.

### Task
Analyze a grocery delivery business end to end: customers, sales, marketing, inventory, customer feedback, and delivery performance.

### Data
Several CSV files loaded from one folder: **Customer** (25,000 customers), **Order**, **Product**, **Marketing**, and **Feedback** (50,000 records), covering **2023 to 2025**.

### What we did in Power Query
- Loaded every file from a folder and set the correct data types, including splitting date-time columns.
- Built separate queries for Customer, Order, Product, Marketing, Feedback, Category, and Rating.
- Merged queries (**Order-Customer**, **Order-Product**, **Products details**) so orders can be analyzed by customer segment, category, and brand.
- Loaded everything into the Data Model and built pivots and charts on **six sheets**: Customer, Sales, Marketing, Inventory, Feedback, and Delivery.

### Key findings
- **Sales:** Total sales are about 232.3M across 449,854 units, and are flat across years (77.5M in 2023, 77.5M in 2024, 77.2M in 2025).
- **Categories:** Instant & Frozen Food (31.3M), Baby Care (30.3M), and Cold Drinks & Juices (29.8M) lead. Dairy & Breakfast (13.5M) and Personal Care (14.2M) are the smallest.
- **Customers:** Customers split almost evenly into four segments (Inactive, New, Premium, Regular), about a quarter each, so roughly 25% of customers are classed as Inactive, which is a retention opportunity.
- **Marketing:** Spend of about 741K generated about 2.97M in revenue, around 4 times the spend, and App, Email, SMS, and Social Media channels perform very similarly.
- **Delivery:** 70.2% of orders arrive on time, 19.8% are slightly delayed, and 10.0% are significantly delayed.
- **Feedback:** The average rating is 4.05 out of 5. 70.2% of feedback is positive and 10.0% is negative, spread evenly across App Experience, Customer Service, Delivery, and Product Quality.
- **Inventory:** In every category, damaged stock is roughly half of stock received, which is high enough to be worth checking in a real business.

---

## Skills Demonstrated
- Cleaning and reshaping data with Power Query (split, unpivot, append, custom functions, folder queries)
- Creating calculated and conditional columns (status, age group, tenure, total sales)
- Building a Data Model with relationships between tables
- PivotTables, PivotCharts, and slicers
- Turning data into business findings
- Working in a team on a shared analysis project

## How to Open
1. Download any `.xlsx` file from this folder.
2. Open it in Microsoft Excel (desktop version, for Power Query and the Data Model).
3. To see the cleaning steps, go to **Data > Queries & Connections**, right-click a query, and choose **Edit**.

*Note: some queries load source files from my local computer, so **Refresh** will only work with the original files. The cleaned results and pivots are saved inside each workbook.*

---
*Created by Mayar Magdy | [GitHub](https://github.com/Mayar-Magdy-DA)*
