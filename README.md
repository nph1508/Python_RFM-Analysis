# Python for Customer Segmentation: RFM Analysis for Marketing Strategy

Author: Nguyễn Phương Huy

Date: 2000-15-08

Tools Used: SQL

---
## 📑 Table of Contents

1. [📌 Background & Overview](#-background--overview)  
2. [📂 Dataset Description & Data Structure](#-dataset-description--data-structure)  
3. [🔎 Final Conclusion & Recommendations](#-final-conclusion--recommendations)
---
## 📌 Background & Overview
### 🎯 Objective

📖 This project uses Python to analyze transactional data from SuperStore and applies the RFM model (Recency–Frequency–Monetary) to:

✔️ Segment customers based on purchase behavior  
✔️ Identify high-value and loyal customers  
✔️ Detect inactive or at-risk customers for re-engagement  
✔️ Support the marketing team in planning targeted, data-driven campaigns

🔍 Business Problem:
The Marketing team cannot manually segment customers due to data volume. They need an automated segmentation system to run personalized campaigns during the holiday season.

### 👤 Who is this project for?

✔️ Data analysts looking to apply customer segmentation in retail datasets  
✔️ Marketing teams aiming to personalize outreach and increase ROI  
✔️ Business stakeholders and decision-makers who want to improve customer retention and CLV (Customer Lifetime Value)

---
## 📊 What is RFM Model?

**RFM** stands for **Recency**, **Frequency**, and **Monetary** — a classic customer segmentation technique used in marketing analytics.

- **Recency (R):** How recently a customer made a purchase  
- **Frequency (F):** How often a customer makes a purchase  
- **Monetary (M):** How much money a customer has spent

By scoring each customer based on these three metrics, we can group them into segments such as:

✔️ Champions  
✔️ Loyal Customers  
✔️ Potential Loyalists  
✔️ At Risk  
✔️ Lost Customers  
✔️ Hibernating

🎯 This model helps businesses identify which customers to reward, retain, or re-engage.

---

## 📂 Dataset Description & Data Structure

### 📌 Data Source
 **File name:** `ecommerce_retail.xlsx`  
 **Size:** ~500,000+ rows  
 **Format:** Excel (.xlsx) 
### 📊 Data Structure & Relationships
**Main columns:**
  - `InvoiceNo`: Unique transaction ID  
  - `StockCode`, `Description`: Product details  
  - `Quantity`: Number of units purchased  
  - `InvoiceDate`: Date of transaction  
  - `UnitPrice`: Price per item  
  - `CustomerID`: Unique customer ID  
  - `Country`: Country of the customer

---

## ⚒️Main Process

---

## 🔎 Final Conclusion & Recommendations
👉 Based on the RFM analysis, we recommend the **Marketing & Sales team** to:

### 📌 Key Actions

✔️ **Retain Champions:**  
   Offer VIP programs, personalized rewards, and early access to new products.

✔️ **Promote Loyal → Champions:**  
   Encourage upsells with milestone-based rewards and targeted nudges.

✔️ **Re-activate At Risk / Hibernating:**  
   Win-back campaigns with discounts, expiring vouchers, or “We miss you” messages.

✔️ **Exclude Lost Customers** from paid targeting to reduce budget waste.

✔️ **Focus on Recency (R)** for Marketing → Re-engagement  
✔️ **Focus on Monetary (M)** for Sales → Upselling high-value groups

---
