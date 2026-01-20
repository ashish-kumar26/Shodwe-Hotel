# Shodwe-Hotel

🏨 Hotel Revenue & Booking Analytics Project

(MS Excel | SQL | Power BI | Tableau)

📌 Project Overview

This project is based on the analysis of hotel booking and revenue data to understand how the business is performing, how customers behave, and how hotel capacity is being used.

The work is done using MS Excel, SQL (PostgreSQL/MySQL), Power BI, and Tableau, covering the complete flow from raw data to final dashboards.

The main purpose of this project is to:

Calculate correct and meaningful KPIs

Keep results consistent across all tools

Build clear and interactive dashboards

Follow industry-standard business logic

🗂️ Dataset Description

The dataset contains 5 tables, divided into dimension tables and fact tables.

🔹 Dimension Tables

dim_date → Date, month-year, week number, weekday/weekend

dim_hotels → Hotel details such as property name, category, and city

dim_rooms → Room class information

🔹 Fact Tables

fact_bookings → Booking-level data including revenue, booking status, and customer details

fact_aggregated_bookings → Aggregated data used for capacity and occupancy analysis

This data structure follows a star schema, which works well for SQL queries and BI tools.

🧠 Business Logic & KPI Definitions

All KPIs are calculated using clear and fixed definitions to avoid confusion.

Total Revenue → Revenue earned from completed stays (Checked Out)

Total Bookings → Count of completed reservations

Occupancy & Capacity → Calculated using aggregated booking data

Cancellation Metrics → Based on booking status

Trend Analysis → Performance tracked monthly and weekly

Extra care was taken to:

Avoid double counting

Clearly separate bookings and room utilization

Keep the same logic in Excel, SQL, Power BI, and Tableau

📊 KPIs Created
🔹 Core KPIs (11)

Total Revenue

Occupancy Rate

Cancellation Rate

Total Bookings

Utilized Capacity

Revenue Trend (Monthly)

Weekday vs Weekend Revenue & Bookings

Revenue by City & Hotel

Class-wise Revenue

Booking Status Breakdown

Weekly Trend – Key Metrics

🧮 SQL (PostgreSQL / MySQL)

SQL was used to work directly with the data and validate all calculations.

Key work includes:

Creating tables with correct data types

Fixing date format issues during data import

Writing clean SQL queries for KPI calculations

Applying correct business filters such as booking_status = 'Checked Out'

Handling transaction-level and aggregated data separately

SQL acted as the base reference for checking results in other tools.

📗 MS Excel Analysis

In MS Excel:

Pivot Tables were used to calculate KPIs

Correct aggregation logic was applied:

COUNT(booking_id) for Total Bookings

SUM(successful_bookings) for Utilized Capacity

Booking status filters were applied properly

KPI naming issues were identified and corrected

Results were matched with SQL outputs

Excel was mainly used for quick checks and understanding the data.

📈 Power BI Dashboard

In Power BI:

A clean data model was built using fact and dimension tables

DAX measures were created instead of calculated columns

Filter behavior was controlled using CALCULATE and REMOVEFILTERS

KPI cards were created for:

Total Revenue

Total Bookings

Occupancy

Cancellation Rate

KPIs were kept stable even when slicers were used

Power BI was used to create interactive and business-friendly dashboards.

📊 Tableau Dashboard

In Tableau:

Calculated fields were created for all KPIs

Booking status logic was applied inside calculations

Correct aggregation levels were maintained

KPI values were formatted using K and M

Trend and comparison charts were built

Tableau helped in presenting trends and patterns visually.

🔍 Key Insights & Learnings

Clear difference between Total Bookings and Utilized Capacity

Importance of defining KPIs correctly before analysis

Understanding how filters behave differently in BI tools

Why SQL validation is important for accuracy

Proper use of fact and dimension tables

Challenges in keeping metrics consistent across tools

🛠️ Tools & Technologies

SQL – PostgreSQL / MySQL

MS Excel – Pivot Tables and KPI validation

Power BI – Data modeling, DAX, dashboards

Tableau – Calculated fields and visual analysis

GitHub – Documentation and version control

📌 Conclusion

This project shows the complete data analysis journey, starting from raw data and ending with validated dashboards.
It follows real business logic and practical analytics methods, making it suitable for:

Data Analyst roles

Business Analyst roles

BI Developer interviews

Portfolio showcase
