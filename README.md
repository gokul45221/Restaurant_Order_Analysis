# Restaurant Order Analysis

## Table of contents
- [Project Overview](#project-overview)
- [Data Sources](#data-sources)
- [Recommendations](#recommendations)
  
### Project Overview
This project aims to analyze restaurant order data to gain insights into customer behavior, preferences, and trends. Using MySQL and data analysis techniques, we'll explore order patterns, identify areas for improvement, and provide recommendations for enhancing the restaurant's services.

### Data Sources
- Source: Restaurant Order Data (.CSV file)
- Description: Contains order information, including customer ID, order date, items ordered, and total cost.

### Tools
- MySQL: Relational database management system for data storage and querying.
- Data Analysis: Techniques used to extract insights from data.

### Data cleaning/Preparation
- Data import and formatting
- Handling missing values and outliers
- Data normalization and transformation

### Data Analysis
- Order frequency and distribution analysis
- Customer segmentation (demographics, order behavior)
- Menu item popularity and revenue analysis
- Seasonal and temporal trends identification
  
#### Which orders had the most number of items?
```SQL
SELECT order_id, COUNT(item_id) AS num_items 
	FROM order_details 
GROUP BY order_id
ORDER BY num_items DESC;
```

#### Ном many orders had more than 12 items?
```SQL
SELECT COUNT(*) 
	FROM
(SELECT order_id, COUNT(item_id) AS num_items
	FROM order_details
GROUP BY order_id
HAVING num_items > 12) AS num_orders;
```

#### What were the least and most ordered items? What categories were they in?
```SQL
SELECT 
    item_name,
    category,
    COUNT(order_details_id) AS num_purchases
FROM
    order_details od
        LEFT JOIN
    menu_items mi ON od.item_id = mi.menu_item_id
GROUP BY item_name , category
ORDER BY num_purchases; -- Least ordered items
```

```SQL
SELECT 
    item_name,
    category,
    COUNT(order_details_id) AS num_purchases
FROM
    order_details od
        LEFT JOIN
    menu_items mi ON od.item_id = mi.menu_item_id
GROUP BY item_name , category
ORDER BY num_purchases DESC; -- Most ordered items
```

#### What were the top 5 orders that spent the most money?
```SQL
SELECT 
    order_id, SUM(price) AS total_spend
FROM
    order_details od
        LEFT JOIN
    menu_items mi ON od.item_id = mi.menu_item_id
GROUP BY order_id
ORDER BY total_spend DESC
LIMIT 5;
```

#### View the details of the highest spend order. What insights can you gather from the results?
```SQL
SELECT 
    category, COUNT(item_id) AS num_items
FROM
    order_details od
        LEFT JOIN
    menu_items mi ON od.item_id = mi.menu_item_id
WHERE
    order_id = 440
GROUP BY category;
```

#### View the details of the top 5 highest spend orders. What insights can you gather from the results
```SQL
SELECT 
    order_id, category, COUNT(item_id) AS num_items
FROM
    order_details od
        LEFT JOIN
    menu_items mi ON od.item_id = mi.menu_item_id
WHERE
    order_id IN (440 , 2075, 1957, 330, 2675)
GROUP BY order_id , category;
```

### Results/Findings
- Key insights and patterns discovered in the data
- Visualizations (e.g., charts, graphs) supporting findings
- Statistical analysis results (e.g., correlation, regression)

### Limitations
- Data quality and availability limitations
- Assumptions made during analysis
- Potential biases or areas for further exploration

### Recommendations
- Actionable suggestions for the restaurant based on findings
- Potential menu adjustments, marketing strategies, or operational improvements

### References
- List of sources used for research, inspiration, or guidance
1. SQL for Businesses by werty
2. chandoo, EMC and tech tfq.
3. Kaggle
4. [Youtube](https://www.youtube.com/@MavenAnalytics)
5. [W3schools](https://www.w3schools.com/sql/default.asp)
