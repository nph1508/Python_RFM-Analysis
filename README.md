# Customer Segmentation using RFM Analysis for Marketing Strategy | Python

<img src="https://github.com/user-attachments/assets/52fc6a5a-1861-4842-bf42-4fa4ff5e6a13" width="100%" />

**Author:** Nguyễn Phương Huy

**Date:** June 2025

**Tools Used:** Python

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
### 1️⃣ Data Cleaning & Preprocessing

**📌 Code Purpose:**  
- Remove duplicate rows (`duplicated()`)  
- Drop entries with missing `CustomerID`  
- Filter out canceled orders with `Quantity < 0`

**🧪 Sample Code:**
```python
ecommerce_retail.dropna(subset=["CustomerID"], inplace=True)
ecommerce_retail = ecommerce_retail[ecommerce_retail["Quantity"] > 0]
print("Duplicates:", ecommerce_retail.duplicated().sum())
```
🧠 Observations:
- Around 25% of records had missing CustomerID and were removed
- Negative Quantity values represent canceled orders and were excluded
- Final dataset after cleaning contains ~392,000 records

### 2️⃣ Python Analysis – RFM Segmentation
**📌 Code Purpose:**
- Compute RFM values per customer:
  - Recency: Days since the last purchase
  - Frequency: Total number of orders
  - Monetary: Total amount spent
- Score each metric from 1–5 using quantiles
- Combine into RFM_Score and map to segments

**🧪 Sample Code:**
```python
snapshot_date = datetime.datetime(2011, 12, 31)
rfm = ecommerce_retail.groupby('CustomerID').agg({
    'InvoiceDate': lambda x: (snapshot_date - x.max()).days,
    'InvoiceNo': 'nunique', 
    'TotalPrice': 'sum'
}).reset_index()

rfm.columns = ['CustomerID', 'Recency', 'Frequency', 'Monetary']
```

**📦 Boxplot – Outlier Detection:**
```python
plt.figure(figsize=(12,4))
for i, col in enumerate(['Recency', 'Frequency', 'Monetary']):
    plt.subplot(1,3,i+1)
    sns.boxplot(y=rfm[col])
    plt.title(col)
plt.tight_layout()
plt.show()
```
** ✅ Results:** 
![image](https://github.com/user-attachments/assets/eb6be89f-6e3d-49fa-af35-3a6b3dea8b68)
🧠 Observations:
- **Recency**: This metric reflects actual customer behavior, so outliers should be kept — no filtering is recommended.
- **Frequency**: Remove outliers to reduce the influence of resellers who purchase unusually often.
- **Monetary**: Remove outliers to avoid distortion when calculating monetary scores.

**🌳 Treemap of Customer Segments**
<details>
  <summary>📋 Click to view code</summary>
  
  ```python
total_customers = rfm['CustomerID'].nunique()
total_revenue = rfm['Monetary'].sum()

rfm_segment_summary = rfm.groupby('Segment').agg({
    'CustomerID': 'nunique',
    'Monetary': 'sum'
}).reset_index()

rfm_segment_summary['Customer_%'] = round(rfm_segment_summary['CustomerID'] / total_customers * 100, 1)
rfm_segment_summary['Revenue_%'] = round(rfm_segment_summary['Monetary'] / total_revenue * 100, 1)

rfm_segment_summary['Label'] = (
    rfm_segment_summary['Segment'] + '\n' +
    'Cus: '+ rfm_segment_summary['Customer_%'].astype(str) + '% ' + '\n' +
    'Rev: '+ rfm_segment_summary['Revenue_%'].astype(str) + '%'
)

segment_colors = {
    'Champions': '#60C5BA',
    'Loyal': '#4F9DED',
    'Potential Loyalist': '#75C09E',
    'New Customers': '#F6C24C',
    'Promising': '#F59E42',
    'Need Attention': '#D9534F',
    'About To Sleep': '#E8A9A6',
    'Hibernating customers': '#71D2C5',
    'At Risk': '#E8B28C',
    "Can't Lose Them": '#F5E05E',
    'Lost customers': '#B0B0B0'
}
colors = [segment_colors[s] for s in rfm_segment_summary['Segment']]

plt.figure(figsize=(14, 8))
squarify.plot(
    sizes=rfm_segment_summary['Customer_%'],
    label=rfm_segment_summary['Label'],
    color=colors,
    text_kwargs={'fontsize': 14, 'fontproperties': 'DejaVu Serif', 'weight': 'normal', 'color': 'black'}
)

plt.title(
    'Customer Segment Distribution: %Customer / %Revenue',
    fontsize=16,
    fontproperties='DejaVu Serif',
    weight='bold'
)

plt.title('Customer Segment Distribution: %Customer / %Revenue', fontsize=16)
plt.axis('off')
plt.show()
  ```
</details>
  
** ✅ Results:** 
![image](https://github.com/user-attachments/assets/14d1a6a4-2f72-4a74-b04a-43782f8bd203)
🧠 Observations:
- Majority of customers fall into **Hibernating, Lost**, or **At Risk** groups
- **Champions** and **Loyal Customers** are fewer in number but contribute most of the revenue
- Segment distribution is highly imbalanced, supporting targeted re-engagement strategies

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
