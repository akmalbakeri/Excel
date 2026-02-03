## Restaurant order analysis using Microsoft Excel

This is a an analysis based on Maven dataset 

Based on this dataset, Maven recommend to answer these questions based on the dataset given. And we will answer them.

1. What were the least and most ordered items? What categories were they in?
2. What do the highest spend orders look like? Which items did they buy and how much did they spend?
3. Were there certain times that had more or less orders?
4. Which cuisines should we focus on developing more menu items for based on the data

# 📂 Project Workflow

## 📥 Data Extraction

1. **Source Acquisition**
   * Downloaded the raw **Restaurant Order Dataset** from [Maven Analytics](https://mavenanalytics.io/data-playground/restaurant-orders).

2. **File Inventory**
   * [`menu_items.csv`](./menu_items.csv): Contains the catalog of all dishes, including IDs, names, categories, and prices.
   * [`order_details.csv`](./order_details.csv): Contains transactional data including order IDs, timestamps, and item IDs.

## 🔄 Data Transformation

1. **Data Consolidation**
   * Identified `item_id` and `menu_item_id` as the common keys between the two datasets.
   * Imported `menu_items.csv` into the main workbook as a reference sheet.

2. **Relational Merging (XLOOKUP)**
   * Used `XLOOKUP` to pull `item_name`, `category`, and `price` into the master order sheet.
   * Code sample : `=XLOOKUP(F2,menu_items!$A$1:$A$33,menu_items!$B$1:$B$33,,0,1)`

3. **Feature Engineering**
   * Created an `hour_order` column by extracting the hour from the `order_time` field.
   * Code : `=TEXT(D2,"hh")`

4. **Output**
   * Saved the final processed data as [`restaurant_order.xlsx`](./restaurant_order.xlsx) 
  
## 📊 Data Analysis with Pivot Table

### 1.What were the least and most ordered items? What categories were they in?

**Pivot Table Configuration:**
* **Rows:** `item_name`, `category`
* **Values:** `Count of item_id`
* **Design Settings:**
    * **Subtotals:** Do Not Show Subtotals
    * **Report Layout:** Show in Tabular Form
    * **Sorting:** Sorted `item_name` by `Count of item_id` in **Descending** or **Ascending** order

**Key Findings:**
* 🏆 **Most Ordered:** Hamburger (Category: American)
* 📉 **Least Ordered:** Chips and Salsa (Category: Mexican)

---

### 2. What do the highest spend orders look like? Which items did they buy and how much did they spend?

**Pivot Table Configuration:**
* **Rows:** `order_id`, `item_name`
* **Values:** `Sum of price`
* **Sorting:** Sorted `Row_labels` by `Sum of price` **Descending**  order
* ** Expand top item.

**Top Order Profile: Order #440**
This order represents the highest spend in the dataset at **$192.15**. 

| Item Name | Price |
| :--- | :--- |
| **Order Total (#440)** | **$192.15** |
| Spaghetti & Meatballs | $35.90 |
| Fettuccine Alfredo | $29.00 |
| Korean Beef Bowl | $17.95 |
| Chicken Parmesan | $17.95 |
| Meat Lasagna | $17.95 |
| Eggplant Parmesan | $16.95 |
| Spaghetti | $14.50 |
| Steak Tacos | $13.95 |
| Hot Dog | $9.00 |
| French Fries | $7.00 |
| Chips & Salsa | $7.00 |
| Edamame | $5.00 |

---

### 3. Were there certain times that had more or less orders?

**Pivot Table Configuration:**
* **Rows:** `hour_order`
* **Values:** `Count of order_id`
* **Sorting:** Sorted `Row_labels` by `Count of order_id` (**Descending**)

**Key Findings:**
* 🕛 **Peak Business Hour:** **12:00 PM** (Lunch Rush)
* 🕙 **Slowest Business Hour:** **10:00 AM** (Post-breakfast lull)

---

### 4. Which cuisines should we focus on developing more menu items for based on the data?

 ** This is a dual-metric analysis. I compared **Revenue** (Total Spend) against **Volume** (Total Orders) to identify high-margin vs. high-popularity categories.

#### **Metric A: Most Revenue (Profitability)**
* **Pivot Table Configuration:**
    * **Rows:** `category`
    * **Values:** `Sum of price`
    * **Sorting:** Sorted `Row_labels` by `Sum of price` (**Descending**)
* **Finding:** 🇮🇹 **Italian** cuisine is the top revenue generator.

#### **Metric B: Most Ordered (Popularity)**
* **Pivot Table Configuration:**
    * **Rows:** `category`
    * **Values:** `Count of order_id`
    * **Sorting:** Sorted `Row_labels` by `Count of order_id` (**Descending**)
* **Finding:** 🥢 **Asian** cuisine is the most frequently ordered.

### Summary Recommendation
* **Italian** | Revenue | **1st Place** (Highest Value) |
* **Asian** | Volume | **1st Place** (Highest Frequency) |

**Strategy:** The restaurant should focus new menu development on **Italian** dishes to capture more high-ticket sales, while maintaining the **Asian** menu to drive consistent foot traffic.
