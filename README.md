# ☕ Café X Sales Data Analysis  
*A Data Cleaning and Product Performance Analysis Project*  
**Prepared by:** Gio Noga  
**Date:** October 2025  

---

## 1. Objective

The goal of this project is to analyze Café X’s sales data to identify:

- The top-performing menu item in terms of quantity sold and revenue  
- Best-selling and top revenue–generating menu items  
- Customer purchase patterns  
- Sales trends over time  

**Deliverables**

- Café Menu Performance Dashboard  
- Insights that support better business decision-making  

---

## 2. Dataset Overview

**Source:** [Cafe Sales - Dirty Data for Cleaning Training](https://www.kaggle.com/datasets/ahmedmohamed2003/cafe-sales-dirty-data-for-cleaning-training)  
**Size:** 10,000 rows  

### Columns

| Column Name        | Description                                                  | Example       |
|--------------------|--------------------------------------------------------------|---------------|
| Transaction ID     | Unique identifier                                            | TXN_1234567   |
| Item               | Purchased item; may contain missing/invalid values           | Coffee        |
| Quantity           | Quantity purchased                                           | 1, 3, UNKNOWN |
| Price Per Unit     | Item's unit price                                            | 2.00, 4.00    |
| Total Spent        | Quantity × Price Per Unit                                    | 8.00, 12.00   |
| Payment Method     | May contain missing/invalid entries                          | Cash, Card    |
| Location           | Transaction location                                         | In-store      |
| Transaction Date   | May contain incorrect formatting                             | 2023-01-01    |

### Reference Price Table

| Item      | Price ($) |
|-----------|-----------|
| Coffee    | 2.00      |
| Tea       | 1.50      |
| Sandwich  | 4.00      |
| Salad     | 5.00      |
| Cake      | 3.00      |
| Cookie    | 1.00      |
| Smoothie  | 4.00      |
| Juice     | 3.00      |

---

## 3. Methodology

### 3.1 Data Validation

Before performing any cleaning operations, the dataset was reviewed to assess its overall quality and identify issues that required correction. Key findings include:

Code:
```python

```
Output:
```
```

- Multiple columns contain missing or invalid values.
- Missing-value indicators are not standardized (e.g., *Unknown*, *ERROR*, blank cells).  
- Several fields do not contribute to the project’s objectives and add unnecessary noise.  
- Certain numeric fields show inconsistencies that violate expected mathematical relationships.  

These validation findings guided the subsequent data-cleaning procedures.

---

### 3.2 Data Cleaning

#### 3.2.1 Removing Unnecessary or Unusable Columns

Since the goal of this project is to analyze the performance of the café’s menu items, the columns **Payment Method** and **Location** were removed because:

- Each column contains more than **50% missing values**, making them unreliable for analysis.  
- These fields do not contribute meaningful insights toward item-level performance.  

#### 3.2.2 Handling Missing or Inaccurate Values

Two main strategies were applied to reconstruct missing or inconsistent values:

##### **• Using Deterministic Relationships to Reconstruct Missing Values**

The columns **Quantity**, **Price per Unit**, and **Total Spent** share a deterministic (functional) mathematical relationship:

$$
Quantity \times Price\ per\ Unit = Total\ Spent
$$

Because these fields depend directly on one another, any missing value can be accurately reconstructed as long as the remaining two values are present. This method ensures precise, non-random imputation.

##### **• Reference-Based Imputation**

When the **Item** value was available, missing prices were filled using the reference price table derived from consistent entries.

Additionally:

- If *Item* was missing but the **price was unique**, the correct item could be inferred.  
- If the price matched multiple items, the item was **not** imputed to avoid incorrect assumptions.  

#### 3.2.3 Standardizing Missing Indicators

To ensure consistent handling of missing data:

- Numeric and date fields containing *ERROR*, *UNKNOWN*, or blanks were replaced with **Null**.  
- String fields that could not be reliably imputed (e.g., ambiguous item names) were standardized to **"Unknown"**.

---

### 3.3 Data Analysis

- **Item Sales Volume** — Total units sold per item  
- **Total Revenue Contribution** — Revenue generated per item  
- **Menu Item Performance Rating** — Combined normalized volume and revenue  
- **Monthly Transaction Frequency** — Number of transactions per month  
- **Customer Volume per Day of Week** — Identification of peak days  

---

### 3.4 Visualizations

A Power BI dashboard was created to visualize analysis results:

- **KPI Cards** → Top menu item, total items sold, total revenue  
- **Lollipop Charts** → Top items by quantity and revenue  
- **Bar Chart** → Revenue share  
- **Line Chart** → Monthly transaction trend  
- **Heat Map** → Daily customer volume pattern  

---

## 4. Results

### 4.1 Item Sales Volume

- Total items sold: **30,180**  
- Most purchased: **Coffee**, **Salad**, **Tea**  
- Least purchased: Cake, Sandwich, Smoothie  

**Trends:**  
- Coffee remained consistently in the top three.  
- Salad showed a decline in Q4.  
- Tea increased in popularity in the second half.

---

### 4.2 Item Revenue Contribution

Total annual revenue: **$89,096**

Top revenue generators:

1. **Salad** – ~21%  
2. **Sandwich** – ~15%  
3. **Smoothie** – ~15%  

Low revenue despite high volume: Coffee, Tea, Cookie  

---

### 4.3 Menu Item Performance Index

| Item     | Sales Score | Revenue Score | Final Rating | Rank |
|----------|-------------|---------------|--------------|------|
| Salad    | 0.978       | 1.000         | **0.989**    | **1** |
| Sandwich | 0.878       | 0.718         | 0.798        | 2 |
| Smoothie | 0.854       | 0.699         | 0.777        | 3 |
| Juice    | 0.898       | 0.551         | 0.724        | 4 |
| Cake     | 0.888       | 0.545         | 0.717        | 5 |
| Coffee   | 1.000       | 0.409         | 0.704        | 6 |
| Tea      | 0.935       | 0.287         | 0.611        | 7 |
| Cookie   | 0.922       | 0.188         | 0.555        | 8 |

**Key Takeaway:**  
Salad is the café’s best-performing item overall, offering a strong balance of sales volume and revenue.

---

### 4.4 Monthly Transaction Frequency

- Average: **~800 transactions/month**  
- Lowest: February  
- Highest: October  
- Trend: Stable year-round customer activity  

---

### 4.5 Daily Customer Volume

- In-store and takeaway counts are nearly equal  
- Payment method data is incomplete (~40% missing), limiting insight  

---

## 5. Conclusion and Recommendations

### Key Findings

- Coffee, Tea, Cookie → high volume but low revenue  
- Salad, Sandwich, Smoothie → strongest revenue contributors  
- Monthly sales remain stable with small seasonal variations  

--

### Recommendations

- Promote high-revenue items (Salad, Sandwich, Smoothie)  
- Slightly adjust Coffee pricing to boost revenue  
- Bundle or reposition underperforming items (Cookie, Tea)  
- Maintain mid-tier items (Cake, Juice)  

---





