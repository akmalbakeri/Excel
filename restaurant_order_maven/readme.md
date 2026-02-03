## Restaurant order analysis using Microsoft Excel

This is a an analysis based on Maven dataset 

Based on this dataset, Maven recommend to answer these questions based on the dataset given. And we will answer them.

1. What were the least and most ordered items? What categories were they in?
2. What do the highest spend orders look like? Which items did they buy and how much did they spend?
3. Were there certain times that had more or less orders?
4. Which cuisines should we focus on developing more menu items for based on the data

📂 Project Workflow

Extraction: 
1.  Downloaded raw CSV data from [Restaurant Order dataset](https://mavenanalytics.io/data-playground/restaurant-orders)
2.  2 files received menu_item.csv and order_details.csv

Transformation:

   1.  Combined both csv
      - Both csv have common key menu_item_id for menu_item.csv and item_id for order_details.csv.
<img width="414" height="227" alt="image" src="https://github.com/user-attachments/assets/985db5a7-f148-4f98-9e9b-c100057563c1" />

       

    Applied XLOOKUP to map relational data across tables.

    Formatted dates and currency for consistency.

Analysis: Created a Pivot Table to summarize [Key Metric].


