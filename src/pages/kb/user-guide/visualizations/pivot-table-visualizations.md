---
category: visualizations
parent_category: user-guide
title: How to make a pivot table
toc: true
slug: pivot-table-visualizations
# IMG BASE URL /assets/images/docs/gitbook/
---

# Intro

Redash's pivot table visualization can aggregate records from a query result into a new tabular display. It's similar to `PIVOT` or `GROUP BY` statements in SQL. But the visualization is configured with drag-and-drop fields instead of SQL code.

# Step 1: Write a query

It should return at least three columns. The source query for a pivot table is usually non-aggregated or "melted". In the below example, I pull indicative data from a school grading system. This is mock data.

![Example Query for Pivot Table](/assets/images/docs/gitbook/pivot-table-query.png)

The SQL query is "dumb". It doesn't group or sort the data. Because we'll use the pivot table to do this without SQL.

Save the query.

# Step 2: Add a **Pivot Table** visualization

Click **New Visualization** and choose **Pivot Table** as the visualization type. The visualization preview on the right will update to show a pivot table.

All the field aliases from your query result become available at the top of the pivot control surface. You can drag these to the _row_ side or the _column_ side. You can also nest them.

Here are some examples using the grade data above:

![](/assets/images/docs/gitbook/pivot-table-configuration-examples.png)

The Pivot Table visualization can display more than one metric side-by-side under each column group. To do this, your query results must be in **long (melted) format**, with one column for the metric name and one for the metric value.

**Example Query Output Format:**

| Student   | grade | School      | Gender |
|-----------|-------|-------------|--------|
| Adams     | 66.54 | Adams       | Female |
| Adams     | 57.42 | Adams       | Male   |
| Jefferson | 58.66 | Jefferson   | Female |
| Jefferson | 66.21 | Jefferson   | Male   |
| Lincoln   | 64.69 | Lincoln     | Female |
| Lincoln   | 60.48 | Lincoln     | Male   |
| McKinley  | 61.39 | McKinley    | Female |
| McKinley  | 64.85 | McKinley    | Male   |
| Washington| 64.79 | Washington  | Female |
| Washington| 62.77 | Washington  | Male   |

You can prepare your data like this in your query (or upstream in your data source).

**To configure the Pivot Table:**
1. Drag your **row grouping field** (e.g., `School`) into the **Rows** area.  
2. Drag **Gender** into the **Columns** area.  
3. Drag **grade** into the **Values** area, and choose the aggregation you want (e.g., *Average*, *Count*, etc.).  
4. *(Optional)* Add another field to **Rows** or **Columns** to create nested groupings, such as adding `Student` under `School` in the Rows area.  

The result will show each school with separate columns for each gender, plus totals.
{% callout warning %}

Pivot table performance can degrade if your query result is too big. The exact size threshold will depend on the computer and browser from which you access Redash. But in general, performance is best below 50,000 _fields_. That could mean 10,000 records with 5 fields each. Or 1,000 records with 50 fields each.

{% endcallout %}
