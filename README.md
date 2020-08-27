# Build a BI Dashboard Using Google Data Studio and BigQuery

For as long as business intelligence (BI) has been around, visualization tools have played an important role in helping analysts and decision-makers quickly get insights from data. 

As a manager of tree services for a large city, you make important decisions based on usage logs data, stored in large (multiple TBs) date-partitioned tables in a BigQuery dataset called "Trees".To get business value out of that data as quickly as possible, you will build a dashboard for analysts that will provide visualizations of trends and patterns in your data.


## Solution overview

Typically, a dashboard shows an aggregated view of usage — it doesn't need details all the way to the level of an order ID, for instance. So, to reduce query costs, you'll first aggregate your needed logs into another dataset called "Reports" then create a table of aggregated data. You'll query the table from the Data Studio dashboard. This way, when your dashboard is refreshed, the reporting dataset queries process less data. Since usage logs from the past never change, you'll only refresh new usage data into the Reports dataset.

![Image of BI](https://github.com/IamVigneshC/GCP-BI-Dashboard-Using-Google-Data-Studio-and-BigQuery/blob/master/Resources/BI.jpg)


## Uploading queryable data

Explore and add public data set: Street Trees

## Create a reports dataset in BigQuery

Create a new dataset called Reports in your project. A separate dataset has a couple of benefits: it reduces the amount of data queried by the dashboard, and it removes unnecessary access to your source datasets by users who are only interested in aggregated data.

## Query the dashboard data

Run a one-time query to pull the data for the last year, summarizing:
•	The number of trees planted each month

•	Which species of trees were planted

•	Who the caretaker of the trees is

•	Address of the planted trees

•	The tree site information.

` SELECT `
 `TIMESTAMP_TRUNC(plant_date, MONTH) as plant_month, `
 
  COUNT(tree_id) AS total_trees,
  
  species,
  
  care_taker,
  
  address,
  
  site_info
  
FROM `

 ` bigquery-public-data.san_francisco_trees.street_trees ` 
 
` WHERE

  address IS NOT NULL
  
  AND plant_date >= TIMESTAMP_SUB(CURRENT_TIMESTAMP(), INTERVAL 365 DAY)
  
  AND plant_date < TIMESTAMP_TRUNC(CURRENT_TIMESTAMP(), DAY)
  
GROUP BY

  plant_month,
  
  species,
  
  care_taker,
  
  address,
  
  site_info  `
  
 
Click the More button, and select Query settings. Set a destination table for query results box, and create a name for the table, like Trees:
  
When the Query Settings has a table name in an existing dataset specified, along with the Write if empty destination option selected, a table will be created if it doesn't already exist, using the name you added.
Accept the other default settings and click Save.
Click Run to run the query.
You will be on the Results tab, where you can see the data.


