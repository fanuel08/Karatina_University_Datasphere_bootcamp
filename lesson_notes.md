
# 📘 Karatina Data Science Bootcamp: The Official Handbook

**Theme:** Solving Local Kenyan Problems with Data.
**Role:** From Scripting to Deployment.

---

# 🟢 Week 1: The Logic Foundation
**Scenario:** A local **Sacco** needs a system to check if a member qualifies for a loan.
**The Rule:** A member can only borrow up to **3 times** their savings.

### 1. Core Concepts
* **Variables:** Storing data (`savings = 5000`).
* **Input:** Getting user data (`input()`).
* **Logic:** Making decisions (`if/else`).


### 2. The Project: "Sacco Loan Calculator"

```# Python code
def check_loan_eligibility():
    print("--- 🏦 SACCO LOAN SYSTEM ---")
    
    # Input
    savings = int(input("Enter Total Savings (Ksh): "))
    loan_request = int(input("Enter Loan Amount (Ksh): "))
    
    # Logic: 3x Rule
    limit = savings * 3
    
    if loan_request <= limit:
        print(f"✅ Approved! Disbursing Ksh {loan_request}")
    else:
        print(f"❌ Rejected. Max limit is Ksh {limit}")

# Run it
check_loan_eligibility()



##🟡 Week 2: Data Structures (Pandas)

Scenario: The University Registrar has a messy Excel sheet of student marks. The Goal: Calculate average performance and find the top students.

1. Core Concepts

    Pandas: The library for data tables.

    DataFrame: A table in Python.

    Filtering: Selecting specific rows.

2. The Project: "The KCSE Analyzer"

Dataset: Student_Name, Math, English, Kiswahili

  # Python code

import pandas as pd

# Load the data
df = pd.read_csv("student_marks.csv")

# Task 1: Create Average Column
df['Average_Score'] = (df['Math'] + df['English'] + df['Kiswahili']) / 3

# Task 2: Filter (Pass > 50)
passed_students = df[df['Average_Score'] > 50]

# Task 3: Top 10 Students
top_10 = df.sort_values(by='Average_Score', ascending=False).head(10)

print(top_10)



##🔴 Week 3: Data Cleaning (The Critical Skill)

Scenario: A Nairobi Shopkeeper records sales manually. The Mess: Prices have "Ksh" mixed with numbers (e.g., "1000ksh"), and some rows are empty (NaN).

1. Core Concepts

    NaN: Not a Number (Empty data).

    String Manipulation: Cleaning text.

    Casting: Converting text to numbers.

2. The Project: "The Messy Shopkeeper"

Dataset: Item, Price (Dirty), Quantity

   # Python code

import pandas as pd

df = pd.read_csv("dirty_sales.csv")

# Step 1: Remove "ksh" and "Zero" text
df['Price'] = df['Price'].str.replace('ksh', '', regex=False)
df['Price'] = df['Price'].str.replace('Zero', '0', regex=False)

# Step 2: Convert to numbers
df['Price'] = pd.to_numeric(df['Price'])

# Step 3: Fill missing values (NaN) with the average price
avg_price = df['Price'].mean()
df['Price'].fillna(avg_price, inplace=True)

# Step 4: Remove Duplicates
df.drop_duplicates(inplace=True)

# Export Clean Data
df.to_csv("clean_sales_data.csv", index=False)



##🔵 Week 4: Visualization & Storytelling

Scenario: The Ministry of Agriculture wants to see rainfall patterns vs. Maize prices. The Goal: Visualize the relationship to warn farmers.

1. Core Concepts

    Matplotlib/Seaborn: Libraries for graphing.

    Line Graph: Trends over time.

    Scatter Plot: Relationships between two variables.

2. The Project: "Crop vs. Climate Dashboard"

     # Python code

import matplotlib.pyplot as plt
import seaborn as sns

# Line Graph: Rainfall over time
plt.figure(figsize=(10, 5))
sns.lineplot(data=df, x='Month', y='Rainfall_mm')
plt.title("Rainfall Patterns 2024")
plt.show()

# Scatter Plot: Does Rain affect Price?
plt.figure(figsize=(10, 5))
sns.scatterplot(data=df, x='Rainfall_mm', y='Maize_Price')
plt.title("Correlation: Rainfall vs Maize Price")
plt.show()



##🟣 Week 5: Exploratory Data Analysis (EDA)

Scenario: An M-Pesa Agent wants to know which day has the highest transaction volume to hold cash. The Goal: Group data to find insights.

1. Core Concepts

    GroupBy: Splitting data into buckets (e.g., by Day).

    Aggregation: Summing or counting those buckets.

2. The Project: "M-Pesa Transaction Insights"

    # Python code

# Group by 'Day_of_Week' and sum the 'Amount'
daily_volume = df.groupby('Day_of_Week')['Amount'].sum()

# Sort to see the busiest day
print(daily_volume.sort_values(ascending=False))

# Insight: "Hold the most cash on Fridays!"



##🟠 Week 6: Intro to Machine Learning (Regression)

Scenario: A Real Estate Agent in Nyeri wants to estimate house rent based on size. The Goal: Train a model to predict rent.

1. Core Concepts

    Features (X): The input (Square_Feet, Rooms).

    Target (y): The output (Rent_Price).

    Linear Regression: Drawing the "best fit line."

2. The Project: "The Rent Predictor"

  # Python code

from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression

# Define X and y
X = df[['Square_Feet', 'Number_of_Rooms']]
y = df['Rent_Price']

# Train the Model
model = LinearRegression()
model.fit(X, y)

# Predict: 3 Rooms, 1500 sqft
prediction = model.predict([[1500, 3]])
print(f"Estimated Rent: Ksh {prediction[0]}")



##🚀 Week 7: Deployment (The "Wow" Factor)

Scenario: The code is useless to the agent. We need an app. The Goal: Build a Streamlit web interface.

The Project: "Live Price Estimator App"

Save this as app.py and run with streamlit run app.py

  # Python code

import streamlit as st
import joblib # Assuming we saved the model

st.title("🏠 Nyeri House Rent Estimator")

# Sliders for user input
rooms = st.slider("Number of Rooms", 1, 10)
sqft = st.slider("Square Footage", 300, 5000)

# Predict Button
if st.button("Estimate Price"):
    price = model.predict([[sqft, rooms]])
    st.success(f"Predicted Rent: Ksh {round(price[0], 2)}")



##🏆 Week 8: The Hackathon (Capstone)

Theme: "Open Choice."

The Challenge:

    Form Squads.

    Find a dataset (or use provided options).

    Clean -> Analyze -> Visualize -> Deploy.

    Present: 5-Minute Demo of a running Streamlit App.

Karatina Data Innovators | 2025
