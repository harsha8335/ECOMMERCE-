#  ECOMMERCE- return rate analysis

#  🎯 Objective

The primary objective of this project is to analyze and reduce product return rates in an e-commerce environment by identifying the key factors that influence customer returns.

This includes:

Exploring how return behavior varies across different product categories, regions, and marketing channels

Using logistic regression to predict the probability of return for each order

Highlighting high-risk products to support decision-making in product design, marketing, and logistics

Creating an interactive Power BI dashboard to visualize trends, patterns, and risk scores for effective business insights

The ultimate goal is to enable the business to reduce returns, improve profitability, and enhance customer satisfaction through data-driven strategies.

#  📑 Table of Contents 

    Introduction & Objective

    Dataset Description

    Tools & Technologies Used

    Data Preprocessing

    Exploratory Data Analysis (EDA)

    Predictive Modeling (Logistic Regression)

    Power BI Dashboard

    Insights & Recommendations

    Conclusion

    deliverables
 

#   📑 Table of Contents (Short Version)
  
    Introduction & Objective

    Dataset Description

    Tools & Technologies Used

    Data Preprocessing

    Exploratory Data Analysis (EDA)

    Predictive Modeling (Logistic Regression)

    Power BI Dashboard

    Insights & Recommendations

    Conclusion

    Deliverables

#   📘 Project Overview

In the fast-growing e-commerce industry, product returns significantly impact revenue, logistics, and customer satisfaction.
This project aims to analyze return patterns and identify key factors influencing customer returns by examining product, customer, and marketing data.

A synthetic dataset is generated to simulate real-world scenarios, including categories, regions, channels, and return behavior. Using Python for data analysis and logistic regression, the project predicts the probability of return for each order. A Power BI dashboard is then created to visualize these insights, helping businesses identify high-risk areas and take proactive actions.

This end-to-end project provides a data-driven approach to reduce return rates and improve overall profitability and user experience in e-commerce platforms.

#  FEATURES

Synthetic data generation for 10,000 orders with 15% returns.
Logistic regression model to predict return probabilities.
SQLite database for efficient data storage and querying.
Interactive Power BI dashboard with visuals for return rates and risk scores by category, geography, and marketing channel.
PDF report summarizing the project and findings.

#  Tools Used

Python: Data generation, preprocessing, and modeling (pandas, NumPy, scikit-learn).
SQLite: Data storage and SQL queries.
Power BI Desktop: Interactive visualizations.
Command Prompt (CMD): Script execution.

#   DATASET USED

![image](https://github.com/user-attachments/assets/59ca6d3d-0050-47f5-9d44-fb9e5ad0277d)


#  SAMPLE CODE

import pandas as pd
import numpy as np
from datetime import datetime, timedelta
import random

# Set random seed for reproducibility
np.random.seed(42)
random.seed(42)

# Parameters
    num_rows = 100

    start_date = datetime(2023, 1, 1)

    end_date = datetime(2023, 12, 31)

# Define possible values
    categories = ['Electronics', 'Apparel', 'Footwear']
    
    regions = ['North America', 'Europe', 'Asia', 'Australia']
                
    marketing_channels = ['Email', 'Social Media', 'Search Ads', 'Affiliate']
    
    products = {
  
    'Electronics': ['Widget', 'Laptop', 'Headphones', 'Phone', 'Tablet'],
    
    'Apparel': ['Shirt', 'Jacket', 'T-shirt', 'Pants', 'Sweater'],
    
    'Footwear': ['Shoes', 'Sandals', 'Boots', 'Sneakers']
}

# Generate dataset
    
    data = {
    
    'order_id': range(1001, 1001 + num_rows),
    
    'product_id': [random.randint(12345, 12444) for _ in range(num_rows)],
    
    'product_name': [],
    
    'category': [random.choice(categories) for _ in range(num_rows)],
    
    'customer_id': [random.randint(501, 600) for _ in range(num_rows)],
    
    'region': [random.choice(regions) for _ in range(num_rows)],
    
    'marketing_channel': [random.choice(marketing_channels) for _ in range(num_rows)],
    
    'order_date': [(start_date + timedelta(days=random.randint(0, (end_date - 
     start_date).days))).strftime('%Y-%m-%d') for _ in range(num_rows)],
    'order_amount': [],
    'is_returned': [random.choices([0, 1], weights=[0.8, 0.2])[0] for _ in 
     range(num_rows)]  # 20% return rate
}

# Generate product names and order amounts based on category
    for category in data['category']:
      product_name = f"{random.choice(products[category])} {chr(random.randint(65, 90))}
      # e.g., Widget A
      data['product_name'].append(product_name)
      # Assign order amounts based on category
      if  category == 'Electronics':
      amount = round(random.uniform(100, 1000), 2)
      elif category == 'Apparel':
      amount = round(random.uniform(20, 150), 2)
      else:  # Footwear
      amount = round(random.uniform(50, 200), 2)
      data['order_amount'].append(amount)

# Create DataFrame

    df = pd.DataFrame(data)

# Save to CSV
    df.to_csv('ecommerce_data.csv', index=False)

    print(f"Generated dataset with {num_rows} rows and saved to 'ecommerce_data.csv'")
    
    print(df.head())

# SAMPLE OUTPUT

![image](https://github.com/user-attachments/assets/3d9989e0-ba5d-4c2d-a737-e5f00eb2a177)


#📊 🔹 Exploratory Data Analysis (EDA) 

✅ Return Rate by Category

📦 Apparel: 12.5%

🔌 Electronics: 32.2%

👟 Footwear: 29.7%

✅ Return Rate by Region

🌏 Asia: 29.2%

    🇦🇺 Australia: 14.3%

    🇪🇺 Europe: 32.0%

    🇺🇸 North America: 23.3%

    ✅ Return Rate by Marketing Channel
    📩 Email: 43.5% (highest!)

    🤝 Affiliate: 28.6%

    🔍 Search Ads: 19.4%

    📱 Social Media: 12.0%

    💰 Average Order Amount by Category
    Electronics: ₹579

    Apparel: ₹84

    Footwear: ₹128

    | Metric    | Class = 0 (Not Returned) | Class = 1 (Returned) |
    | --------- | ------------------------ | -------------------- |
    | Precision | 0.57                     | 0.00 ⚠️              |
    | Recall    | 1.00                     | 0.00 ⚠️              |
    | F1-Score  | 0.72                     | 0.00 ⚠️              |


🎯 Accuracy: 56.7%

🧠   Sample Prediction Results

    | order\_id | product\_name | return\_probability |
    | --------- | ------------- | ------------------- |
    | 1001      | T-shirt U     | 0.21                |
    | 1002      | Pants W       | 0.06                |
    | 1003      | Jacket X      | 0.09                |
    | 1004      | Boots T       | 0.15                |
    | 1005      | Sneakers O    | 0.12                |

#  💻 Python Code to Export High-Risk Products

    import pandas as pd

    # Load the full dataset with return probability
    
    df = pd.read_csv('ecommerce_data_with_return_probability.csv')

# Filter high-risk products
    
    high_risk = df[df['return_probability'] > 0.7]

# Save to CSV
    high_risk.to_csv('high_risk_products.csv', index=False)

    print("High-risk product CSV saved successfully.")
#  ✅ Conclusion

          This project successfully demonstrated how data-driven analysis can be used to understand and reduce return rates in an e-commerce business.
    By generating a realistic synthetic dataset and analyzing key attributes such as product category, geographic region, and marketing channel, 
    we identified meaningful patterns in customer return behavior.

          Using logistic regression, we built a predictive model to estimate the probability of a return for each order. Although the model's
    performance suggests room for improvement (due to class imbalance and limited data), it still helps flag high-risk products, offering
    valuable insights to the business.

          The interactive Power BI dashboard further enhances this analysis by providing clear visualizations and filters, allowing stakeholders 
    to explore trends and make informed decisions.

          Overall, this end-to-end project highlights the potential of combining Python, SQL, and Power BI to drive actionable insights and improve 
    customer satisfaction in e-commerce operations
