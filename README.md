TVS Motors Order Tracking Dashboard

A 5-page Power BI dashboard that tracks the full order lifecycle for a simulated two-wheeler manufacturer — from order placement through an 8-stage manufacturing pipeline to final delivery — across 250,000+ orders.

Business Context

TVS Motors operates a centralized order processing system where dealers across Tamil Nadu place orders on behalf of customers for various bike models. Each order moves through an 8-stage manufacturing pipeline — Quotation → Confirmation → Engine Setup → Body Setup → Final Assembly → QC → Delivery Start → Delivered — typically taking 30–45 days end to end.

The goal of this dashboard is to give operations, sales, and supply chain teams a single view into delivery performance, dealer SLA compliance, and customer behavior.

Dashboard Pages

1. Dealer Performance
Total orders per dealer, average delivery time, on-time delivery %, delayed order counts, and a weighted SLA compliance score to rank top/bottom performing dealers.

2. Order Fulfillment Tracker
Real-time view of orders sitting in each of the 8 pipeline stages, completed vs. in-progress orders, average time spent per stage, and SLA breach counts.

3. Model-Wise Sales Performance
Revenue estimation (On-Road Price × Quantity), order volume by bike model and category, Petrol vs. Electric split, and average delivery time by model.

4. Customer Insights
Repeat customer counts, gender and age-band segmentation, city-wise distribution, and a loyalty index based on purchase frequency and recency.

5. Monthly Trend & SLA Report
Monthly order volume, on-time % trend, average delivery days, cumulative YTD orders, and monthly delayed order counts.

Data Model

Star schema built across 9 tables:


Bike_Master, Dealer_Master, Customer_Master — dimension tables
Orders, TVS_Orders_Part_1 – TVS_Orders_Part_5 — fact tables (250K+ rows, split across parts)


The Hard Part: Parsing Packed Stage History

The raw data stored each order's entire stage history as a single packed text string, e.g.:

Quotation:2023-08-08 16:51:00, Confirmed:2023-08-09 17:37:00, ...

There was no clean "current stage" field to filter or aggregate on. This required custom Power Query (M) logic to split, parse, and extract timestamps for each stage, then derive the order's current stage and per-stage duration — before any of the actual report building could start. A good reminder that most BI effort goes into shaping messy source data, not into the visuals.

Key Techniques Used


Power Query (M) for parsing stage-history strings into structured fields
Custom Date table via CALENDAR()
DAX variables and SWITCH() logic for dynamic KPI calculations
Dynamic metric switching using SELECTEDVALUE()
Field Parameters for interactive metric selection
Bookmarks & tooltips for drill-down interactions
(Optional) Role-level security scoped by dealer


Sample Insight


₹25Bn+ in estimated revenue across 250K+ orders
Electric models made up ~40% of order category share, with Scooter and Commuter close behind
Petrol still dominates fuel type share (~93%) over Electric (~7%)


Tools

Power BI Desktop · Power Query (M) · DAX · Star Schema Modeling
