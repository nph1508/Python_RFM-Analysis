# 🛒 Customer Segmentation using RFM Analysis for Marketing Strategy | Python

<img src="https://github.com/user-attachments/assets/52fc6a5a-1861-4842-bf42-4fa4ff5e6a13" width="100%" />

**Author:** Nguyễn Phương Huy

**Date:** June 2025

**Tools Used:** Python

---
## 📑 Table of Contents

[1. 📌 Background & Overview](#1--background--overview)  
[2. 📂 Dataset Description & Data Structure](#2--dataset-description--data-structure)  
[3. 🧹 Data Cleaning & Preprocessing](#3--data-cleaning--preprocessing)  
[4. 🔍 Exploratory Data Analysis (EDA)](#4--exploratory-data-analysis-eda)  
[5. 🧮 Apply RFM Model](#5--apply-rfm-model)  
[6. 📊 Visualization & Analysis](#6--visualization--analysis)  
[7. 💡 Insight & Recommendation](#7--insight--recommendation)  

--- 
## 1. 📌 Background & Overview
### 🎯 Objective 

**📖 What is this project about?**  

- The Marketing team wants to launch personalized campaigns for customer retention and acquisition during the holiday season. However, due to the large dataset, manual segmentation is no longer feasible.  
- To solve this, the **RFM model** is applied using **Python (Colab)** to classify customers into different segments based on their purchasing behavior.  
- This project involves **data preparation, RFM score calculation, segmentation, visualization, and providing actionable recommendations** for the Marketing and Sales teams to optimize their strategies.

**👤 Who is this project for?**  

✔️ Marketing & Sales Department  
✔️ Decision-makers & stakeholders 

**❓ Business Questions:**  

✔️ How can we segment customers effectively using the RFM model?  
✔️ Which customer groups should be prioritized for retention and promotional campaigns?  
✔️ What actionable insights can help improve marketing strategies and customer engagement?  
✔️ What strategies should be applied to different customer segments to maximize value?

### RFM Analysis Overview  

**🔎 Why use RFM?**  

RFM (Recency, Frequency, Monetary) is a customer analysis technique based on purchasing behavior. In RFM analysis, each customer is assigned a score based on these three factors. The data is then used to categorize customers into segments, helping businesses identify key audiences for targeted marketing and sales strategies.  

- **Recency**: Measures the time elapsed since a customer's last purchase.  
- **Frequency**: Evaluates how often a customer makes transactions.  
- **Monetary**: Calculates the total amount spent by the customer.  
By applying RFM, businesses can segment customers based on their value, allowing them to optimize marketing and customer engagement strategies.  

---
## 2. 📂 Dataset Description & Data Structure

### 📌 Data Source  
- **Source**: Provided dataset for E-commerce retail analysis  
- **Size**: 541,910 rows × 8 columns (Sheet 1: E-commerce retail), additional segmentation details in Sheet 2  
- **Format**: .xlsx (Excel file with two sheets)

## 📂 Data Structure & Relationships  

### 1️⃣ Tables Used  
The dataset consists of **two tables (sheets)**:  
- **Sheet 1: E-commerce Retail** – Contains transaction-level data, including order details, customer IDs, and purchase information.  
- **Sheet 2: Segmentation** – Stores customer segments along with their RFM scores.  

### 2️⃣ Table Schema & Data Snapshot  
#### 📌 Sheet 1: E-commerce Retail  
### 📋 Table Schema: E-commerce Retail  

<details>
  <summary>📂 Dataset Schema (Click to expand)</summary>

| Column Name  | Data Type         | Description  |  
|-------------|-----------------|--------------|  
| **InvoiceNo**  | `object`  | Unique invoice number for each transaction (6-digit). If it starts with 'C', it indicates a cancellation. |  
| **StockCode**  | `object`  | Unique product (item) code (5-digit). |  
| **Description**  | `object`  | Product (item) name. |  
| **Quantity**  | `int64`  | The number of units purchased per transaction. |  
| **InvoiceDate**  | `datetime64[ns]`  | Date and time when the transaction occurred. |  
| **UnitPrice**  | `float64`  | Price per unit of the product in sterling. |  
| **CustomerID**  | `float64`  | Unique 5-digit identifier for each customer. |  
| **Country**  | `object`  | Name of the country where the customer resides. |  

</details>

#### 📌 Sheet 2: Segmentation  
### 📊 Customer Segmentation & RFM Scores  

<details>
  <summary>📊 RFM Segmentation Mapping (Click to expand)</summary>

| **Segment**              | **RFM Score**  |  
|-------------------------|-----------------------------------------------------------|  
| **Champions**            | 555, 554, 544, 545, 454, 455, 445  |  
| **Loyal**                | 543, 444, 435, 355, 354, 345, 344, 335  |  
| **Potential Loyalist**   | 553, 551, 552, 541, 542, 533, 532, 531, 452, 451, 442, 441, 431, 453, 433, 432, 423, 353, 352, 351, 342, 341, 333, 323  |  
| **New Customers**        | 512, 511, 422, 421, 412, 411, 311  |  
| **Promising**            | 525, 524, 523, 522, 521, 515, 514, 513, 425, 424, 413, 414, 415, 315, 314, 313  |  
| **Need Attention**       | 535, 534, 443, 434, 343, 334, 325, 324  |  
| **About To Sleep**       | 331, 321, 312, 221, 213, 231, 241, 251  |  
| **At Risk**              | 255, 254, 245, 244, 253, 252, 243, 242, 235, 234, 225, 224, 153, 152, 145, 143, 142, 135, 134, 133, 125, 124  |  
| **Cannot Lose Them**     | 155, 154, 144, 214, 215, 115, 114, 113  |  
| **Hibernating Customers** | 332, 322, 233, 232, 223, 222, 132, 123, 122, 212, 211  |  
| **Lost Customers**       | 111, 112, 121, 131, 141, 151   |

</details>
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
