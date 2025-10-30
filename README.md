# Task-7-Basic-Sales-Summary-Using-SQLite-Python
Fetch and visualize simple sales summary (total quantity &amp; revenue by product) from a small SQLite database.
Tools Needed

Python (built-in sqlite3)

pandas

matplotlib

(Optional: jupyter notebook for visualization)

📁 Step 1: Create a Sample SQLite Database

import sqlite3

# Create or connect to database
conn = sqlite3.connect("sales_data.db")
cursor = conn.cursor()

# Create table
cursor.execute("""
CREATE TABLE IF NOT EXISTS sales (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    product TEXT,
    quantity INTEGER,
    price REAL
)
""")

# Insert sample data
data = [
    ('Laptop', 5, 60000),
    ('Mobile', 10, 20000),
    ('Tablet', 7, 15000),
    ('Headphones', 15, 3000),
    ('Smartwatch', 8, 8000)
]

cursor.executemany("INSERT INTO sales (product, quantity, price) VALUES (?, ?, ?)", data)
conn.commit()
conn.close()

print("✅ Database and table created with sample data!")

📊 Step 2: Query and Visualize Data
import sqlite3
import pandas as pd
import matplotlib.pyplot as plt

# Connect to database
conn = sqlite3.connect("sales_data.db")

# SQL query for summary
query = """
SELECT product,
       SUM(quantity) AS total_qty,
       SUM(quantity * price) AS revenue
FROM sales
GROUP BY product
"""

# Load into pandas DataFrame
df = pd.read_sql_query(query, conn)

# Close connection
conn.close()

# Print summary
print("📦 Sales Summary:")
print(df)

# Plot bar chart for revenue
df.plot(kind='bar', x='product', y='revenue', legend=False, color='skyblue')
plt.title("Revenue by Product")
plt.xlabel("Product")
plt.ylabel("Total Revenue")
plt.tight_layout()
plt.savefig("sales_chart.png")  # Save chart (optional)
plt.show()

🧾 Output Example (Printed)

📦 Sales Summary:
      product  total_qty   revenue
0     Headphones         15    45000
1        Laptop          5   300000
2        Mobile         10   200000
3      Smartwatch        8    64000
4        Tablet          7   105000


📈 Output Chart

A simple bar chart comparing revenue by product will be displayed (and saved as sales_chart.png).

✅ Outcome

By completing this task, you will:

Learn to connect Python with an SQLite database

Run SQL queries directly from Python

Use pandas to load query results

Create a simple bar chart using matplot


