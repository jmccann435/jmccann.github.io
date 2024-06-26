---
layout: post
title: Customer Insights and Sales
image: "https://images.unsplash.com/photo-1607349913338-fca6f7fc42d0?q=80&w=1548&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D"
tags: [SQL, Python, Tableau]
---

# My first project
## is all about
### how much
#### I LOVE
##### Python & Coffee!

---

# Business Case

The owners of a small grocery chain have asked for an analysis of their Sales, Customers, and a recent marketing campaign based on data stored in a database. They would like a basic statistical analysis on this data and a dashboard summarizing the key insights and trends in these 3 domains.

# Solution

In this solution I will show how I connected directly to the companies postgreSQL database using Python and performed exploratory data analysis, handled outliers, generated precurosor visualisations, and the final dashboard in Tableau presenting key statistics and trends back to the business.

---

## Running Our SQL Statement in Python

In order to begin this analysis, we first load our data from the PostgreSQL database into Pandas DataFrames using Python. This sets us up to be able to quickly perform EDA and run our statisical analysis on the tables provided to us by the business.

...
from sqlalchemy import create_engine
import pandas as pd

db_params = {
    'dbname': 'data_science_infinity',
    'user': 'student',
    'password': '*******',
    'host': 'data-science-infinity.cpwa6tfdvnx2.eu-west-2.rds.amazonaws.com',
    'port': '5432'
}

connection_string = f"postgresql://{db_params['user']}:{db_params['password']}@{db_params['host']}:{db_params['port']}/{db_params['dbname']}"

# Create the SQLAlchemy engine
engine = create_engine(connection_string)

# Example query
try:
    
    customer_details = pd.read_sql('SELECT * FROM customer_details', engine)
    transactions = pd.read_sql('SELECT * FROM grocery_db.transactions', engine)
    campaign_data = pd.read_sql('SELECT * FROM grocery_db.campaign_data', engine)
    product_areas = pd.read_sql('SELECT * FROM grocery_db.product_areas', engine)
    loyalty_scores = pd.read_sql('SELECT * FROM grocery_db.loyalty_scores', engine)
    
except Exception as error:
    print(f"Error executing the query: {error}")
...
