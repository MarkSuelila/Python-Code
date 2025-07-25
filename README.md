# Python-Code
# From Raw Excel to Insightful Visualization in Python
# Today, I explored a simple yet powerful data analysis workflow using Pandas and Matplotlib to extract meaningful insights from an Excel dataset.

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

# Load data from Excel
df = pd.read_excel(r"C:\Users\Admin\Desktop\Sample.xlsx")

# Print selected columns
print(df[['Year', 'Country', 'Revenue']])
# Create pivot table
pivot = df.pivot_table(values='Revenue', index='Country', columns='Year', aggfunc='sum', fill_value=0)

# Add Grand Total column (row-wise sum)
pivot['Grand Total'] = pivot.sum(axis=1)

# Format with commas
formatted_pivot = pivot.copy()
for col in formatted_pivot.columns:
    formatted_pivot[col] = formatted_pivot[col].map(lambda x: f"{x:,}")
# Print formatted pivot table
print(formatted_pivot)

#create Line Chart 
pivot.T.plot(figsize=(12,6), marker='o')
plt.title('Revenue Over Years by Country')
plt.xlabel('Year')
plt.ylabel('Revenue')
plt.grid(True)
plt.legend(title='Country')
plt.tight_layout()
plt.show()
