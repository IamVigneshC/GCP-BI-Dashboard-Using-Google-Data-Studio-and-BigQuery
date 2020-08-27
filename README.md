# Build a BI Dashboard Using Google Data Studio and BigQuery

For as long as business intelligence (BI) has been around, visualization tools have played an important role in helping analysts and decision-makers quickly get insights from data. 

As a manager of tree services for a large city, you make important decisions based on usage logs data, stored in large (multiple TBs) date-partitioned tables in a BigQuery dataset called "Trees".To get business value out of that data as quickly as possible, you will build a dashboard for analysts that will provide visualizations of trends and patterns in your data.


## Solution overview

Typically, a dashboard shows an aggregated view of usage — it doesn't need details all the way to the level of an order ID, for instance. So, to reduce query costs, you'll first aggregate your needed logs into another dataset called "Reports" then create a table of aggregated data. You'll query the table from the Data Studio dashboard. This way, when your dashboard is refreshed, the reporting dataset queries process less data. Since usage logs from the past never change, you'll only refresh new usage data into the Reports dataset.

