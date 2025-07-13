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

## 3. 🧹 Data Cleaning & Preprocessing
[In 1]:  
```python
# Print the first five rows of the dataset
ecommerce_retail.head()
```

[Out 1]: 

<img width="1053" height="199" alt="Ảnh màn hình 2025-07-13 lúc 11 09 48" src="https://github.com/user-attachments/assets/2b165c99-b3ac-4cf0-9417-93da3b3c1511" />

[In 2]:  
```python
# Check the general information of df
ecommerce_retail.info()
```
[Out 2]:

<img width="526" height="325" alt="Ảnh màn hình 2025-07-13 lúc 11 11 52" src="https://github.com/user-attachments/assets/cde2e286-7da1-40d4-8845-95ddaad86a1f" />

[In 3]:
```python
# Check Data Summary
ecommerce_retail.describe()
```
[Out 3]:

<img width="616" height="303" alt="Ảnh màn hình 2025-07-13 lúc 11 12 12" src="https://github.com/user-attachments/assets/0ed8348d-5f22-40d8-bd91-70fd0d5ff980" />

### 🧹 Data Cleaning Summary

- ❌ Removed transactions with **missing `CustomerID`**  
- ❌ Removed rows with **`Quantity` ≤ 0 or `UnitPrice` ≤ 0** (likely returns or cancellations)  
- ✅ Removed duplicate records  
- 🧮 Created new column `TotalPrice = Quantity × UnitPrice`  
- 🔄 Reset index after cleaning  
- 🔢 Converted `CustomerID` to string to avoid decimal formatting

### 🧐 Reasons for Data Exclusion

- **Missing `CustomerID`**:  
  - Likely caused by guest checkouts, offline orders, or anonymous purchases  
  - Cannot be used to track customer behavior  
  - Accounted for ~25% of the data → dropped entirely

- **Negative `Quantity` or `UnitPrice`**:  
  - Indicates returns, refunds, or test transactions  
  - Not relevant for customer segmentation and spend behavior

---

## 4. 🔍 Exploratory Data Analysis (EDA)
### 🛠 Data Cleaning
```python
ecommerce_retail = ecommerce_retail.dropna(subset=['CustomerID'])
ecommerce_retail['CustomerID'] = ecommerce_retail['CustomerID'].astype(int).astype(str)
ecommerce_retail = ecommerce_retail[(ecommerce_retail['Quantity'] > 0) & (ecommerce_retail['UnitPrice'] > 0)]
ecommerce_retail = ecommerce_retail.drop_duplicates()
ecommerce_retail['TotalPrice'] = ecommerce_retail['Quantity'] * ecommerce_retail['UnitPrice']
ecommerce_retail.reset_index(drop=True, inplace=True)
```
### ✅ Data Quality After Cleaning
- ✔ No missing values in relevant fields  
- ✔ No duplicates  
- ✔ All transaction values are valid and positive  
- ✔ Ready for RFM metric generation (Recency, Frequency, Monetary)

---

## 5. 🧮 Apply RFM Model

#### 🛠 Step 1. Calculate RFM Score

[In 8]:

```python
rfm = ecommerce_retail.groupby('CustomerID').agg({
    'InvoiceDate': lambda x: (snapshot_date - x.max()).days,   # Recency
    'InvoiceNo': 'nunique',                                    # Frequency
    'TotalPrice': 'sum'                                        # Monetary
}).reset_index()

rfm.columns = ['CustomerID', 'Recency', 'Frequency', 'Monetary']
```
#### 🛠 Step 2. Check outlier

In 9]:

```python
plt.figure(figsize=(12,4))
for i, col in enumerate(['Recency', 'Frequency', 'Monetary']):
    plt.subplot(1,3,i+1)
    sns.boxplot(y=rfm[col])
    plt.title(col)
plt.tight_layout()
plt.show()
```
[Out 9]:

<img width="1189" height="390" alt="image" src="https://github.com/user-attachments/assets/b619ea3e-962c-489e-b05b-b50ef9be514a" />


**📌 Solution**
We set a 95% threshold for **Recency**, **Frequency**, and **Monetary** to remove extreme values (outliers) from the dataset. This ensures that the analysis focuses on the majority of the data, improving its reliability for further insights.

#### 🛠 Step 3. Assign RFM scores using Qcut

[In 10]:

```python
# Recency score: Lower values indicate more recent purchases, so assign higher scores to lower recency values  
rfm['R_Score'] = pd.qcut(rfm['Recency'], 5, labels=[5,4,3,2,1]).astype(int)
# Frequency score: Higher values indicate more frequent purchases, so assign higher scores to higher frequency values  
rfm['F_Score'] = pd.qcut(rfm['Frequency'].rank(method='first'), 5, labels=[1,2,3,4,5]).astype(int)
# Monetary score: Higher values indicate higher spending, so assign higher scores to higher monetary values  
rfm['M_Score'] = pd.qcut(rfm['Monetary'], 5, labels=[1,2,3,4,5]).astype(int)
# Combine RFM scores into a single string to create the RFM segment  
rfm['RFM_Score'] = rfm['R_Score'].astype(str) + rfm['F_Score'].astype(str) + rfm['M_Score'].astype(str)
```
#### 🛠 Step 4. Calculate RFM Score

Process the segmentation table & merge with RFM_df

[In 11]:

```python
segment_dict = {}
for _, row in segmentation.iterrows():
    scores = row['RFM Score'].replace(" ", "").split(',')
    for score in scores:
        segment_dict[score] = row['Segment']
rfm['Segment'] = rfm['RFM_Score'].map(segment_dict)
rfm
```
[Out 11]:

<img width="833" height="417" alt="Ảnh màn hình 2025-07-13 lúc 11 38 12" src="https://github.com/user-attachments/assets/80a5d348-26f6-4f52-8e14-adbcbd5a9ace" />

## 6. 📊 Visualization & Analysis
### **1. Contribution by Segmentation**

<img width="950" height="655" alt="image" src="https://github.com/user-attachments/assets/08bc1095-4093-414f-bb36-c4d5b41967fd" />

### **2. Segmentation by Spending** 

<img width="950" height="655" alt="image" src="https://github.com/user-attachments/assets/4ea70fce-12d1-4dde-a122-3419530e9b88" />


### **3. Segmentation by Frequency** 

<img width="1189" height="790" alt="image" src="https://github.com/user-attachments/assets/01b16eae-215f-43ee-968e-828ee0d4439f" />


### **4. Segmentation by Recency** 

<img width="1189" height="790" alt="image" src="https://github.com/user-attachments/assets/fc1d92d8-b146-4406-88da-7ada2d600418" />

---

## 7. 💡 Insight & Recommendation

From the four analysis charts on contribution, monetary, recency, and frequency for each segment, we can analyze the behavior of the 11 segments as follows:

| Segment                 | Recency (R)             | Frequency (F)          | Monetary (M)           | **Characteristics** |
|-------------------------|--------------------------|--------------------------|--------------------------|----------------------|
| **Champions (18%)**      | **Very Low** (~35 days)   | **Very High** (~6.8x)     | **Very High** (~43% of revenue) | Best customers. Buy often and recently. Huge contribution to revenue. Should be prioritized for VIP treatment. |
| **Loyal (10%)**          | Low (~62 days)            | High (~4.6x)              | High (~17%)               | Repeat customers with consistent spending. Should be maintained with loyalty programs. |
| **Potential Loyalist (11%)** | Very Low (~49.9 days)      | Moderate (~2.4x)           | Medium (~5%)               | New customers showing potential. Encourage to convert to loyal with targeted offers. |
| **Promising (4%)**       | Very Low (~50.4 days)     | Low (~1.2x)               | Low (~3%)                 | New/early-stage buyers. Educate and offer follow-up promotions. |
| **New Customers (6%)**   | Very Low (~50.4 days)     | Very Low (~1.0x)          | Very Low (~1%)            | Just made their first purchase. Focus on onboarding & retention. |
| **Need Attention (6%)**  | Low (~59.1 days)          | Medium (~2.7x)            | Moderate (~6%)            | Previously active, now slowing down. Send reminders or time-limited offers. |
| **At Risk (11%)**        | High (~174 days)          | Moderate (~3.4x)          | High (~14%)               | Good spending history but have not returned in a while. Use reactivation campaigns. |
| **Hibernating (15%)**    | High (~178.4 days)        | Low (~1.4x)               | Medium (~5%)              | Once active, now dormant. Try to reignite interest with updates or re-engagement. |
| **Can't Lose Them (3%)** | Very High (~257.7 days)   | Low (~1.8x)               | Medium (~3%)              | Previously valuable but haven’t purchased recently. Personal outreach recommended. |
| **Lost Customers (11%)** | **Very High** (~301.7 days) | **Very Low** (~1.1x)      | **Very Low** (~2%)        | Inactive for a long time. Low priority for retention; focus on acquiring new users. |
| **About To Sleep (7%)**  | High (~116.9 days)        | Low (~1.3x)               | Low (~2%)                 | Slowing down. Try reactivation with urgency-based messages. |

Based on the above analysis, we can see that some segments share similar characteristics. Therefore, we can group them into segment clusters for easier analysis and to propose suitable strategies as follows:

### **Group 1: High-Risk Customers (27%)**
📌 **Includes:** Can't Lose Them (3%), At Risk (11%), About to Sleep (7%), Need Attention (6%)

💡 **Reason for grouping:**

These customers previously showed moderate to high engagement but are now at risk of churning.  
- **Recency** is high, ranging from ~60 to 250+ days  
- **Purchase frequency** has dropped (1.3 – 3.4 orders on average)  
- Some (e.g. *At Risk*) still contribute noticeably to revenue (~14%), but decline is evident  
Without intervention, they are likely to disengage completely. Targeted reactivation campaigns are crucial.

### **Group 2: Loyal & High-Value Customers (39%)**
📌 **Includes:** Champions (18%), Loyal (10%), Potential Loyalist (11%)

💡 **Reason for grouping:**

These are the most valuable segments in terms of activity and revenue.  
- **Recency** is low (~35–60 days) → recently active  
- **Frequency** is high (2.4 – 6.8 orders)  
- **Revenue contribution** is the highest (Champions = 43%, Loyal = 17%)  
They have strong long-term potential. Retain and nurture through loyalty programs, exclusive offers, and personalized communication.

### **Group 3: New & Developing Customers (10%)**
📌 **Includes:** New Customers (6%), Promising (4%)

💡 **Reason for grouping:**

Customers who are new or starting to show early interest.  
- **Recency** is low (~50 days), indicating recent engagement  
- **Frequency** and **monetary** values are still low (~1.0–1.2 orders, ~1–3% revenue)  
This group should be onboarded carefully and encouraged to make repeat purchases through education, follow-up emails, and first-time discounts.

### **Group 4: Inactive & Lost Customers (24%)**
📌 **Includes:** Hibernating (15%), Lost Customers (11%)

💡 **Reason for grouping:**

These customers are **disengaged for a long time** and show minimal purchasing behavior.  
- **Recency** is very high (~180–300+ days)  
- **Frequency** is low (~1.1–1.4), and **monetary value** is also minimal (~2–5%)  
They are least likely to return organically. Consider whether to invest in win-back campaigns or focus on acquiring new users instead.

### 📌 Strategic Marketing Recommendations

- **Focus on retention**: Prioritize Champions and Loyal customers by offering VIP perks and loyalty programs.
- **Reactivation campaigns**: Target At Risk and About to Sleep groups with time-sensitive discounts or personalized offers.
- **Onboarding flows**: Engage New and Promising customers with educational content, follow-up emails, and incentives for second purchase.
- **Evaluate investment**: Consider cost-effectiveness before investing in win-back campaigns for Lost or Hibernating customers.

### 🎯 Key Metric to Prioritize: **Recency**

Among the RFM metrics, **Recency** is the most actionable and should be prioritized by both Marketing and Sales teams.

- **Why Recency matters**:
  - It's the strongest indicator of current engagement.
  - Customers who purchased recently are more likely to respond to marketing efforts.
  - Easier to re-engage customers who bought in the last 30–60 days than those inactive for 6+ months.

- **Actionable insights**:
  - Use Recency to trigger automated remarketing flows (e.g., 14 days after last purchase).
  - Monitor spikes in Recency among VIPs as early signs of churn.
  - Segment campaigns based on recent activity: <30 days (active), 30–90 (warm), >90 (cold).

💡 While Frequency and Monetary are important for long-term strategy and segmentation, **Recency** offers the best leverage for short-term revenue growth and customer retention.

---
