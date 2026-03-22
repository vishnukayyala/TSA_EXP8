# Ex.No: 08     MOVINTG AVERAGE MODEL AND EXPONENTIAL SMOOTHING
### Date: 


### AIM:
To implement Moving Average Model and Exponential smoothing Using Python.
### ALGORITHM:
1. Import necessary libraries
2. Read the electricity time series data from a CSV file,Display the shape and the first 20 rows of
the dataset
3. Set the figure size for plots
4. Suppress warnings
5. Plot the first 50 values of the 'Value' column
6. Perform rolling average transformation with a window size of 5
7. Display the first 10 values of the rolling mean
8. Perform rolling average transformation with a window size of 10
9. Create a new figure for plotting,Plot the original data and fitted value
10. Show the plot
11. Also perform exponential smoothing and plot the graph
### PROGRAM:

## Moving Average And Plot Transform Dataset:

```

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import os
import warnings
warnings.filterwarnings('ignore')

# --- Independent Path Finder ---
file_path = None
for path in ['/content/aapl_master_enriched.csv', 'aapl_master_enriched.csv', '/aapl_master_enriched.csv']:
    if os.path.exists(path):
        file_path = path
        break

if file_path:
    # Read the data
    df = pd.read_csv(file_path)
    
    # Display shape and first 20 rows
    print("Dataset Shape:", df.shape)
    print("\n--- FIRST 20 ROWS ---")
    print(df[['date', 'close']].head(20))

    # Set figure size
    plt.rcParams['figure.figsize'] = (12, 6)

    # Use first 100 values for clearer visualization
    subset = df.head(100).copy()

    # 1. Plot the first 50 values
    plt.figure()
    plt.plot(subset['close'].iloc[:50], marker='o', linestyle='-', color='black')
    plt.title('Apple Stock: First 50 Data Points')
    plt.ylabel('Price ($)')
    plt.show()

    # 2. Moving Average (Rolling Window of 5)
    subset['MA_5'] = subset['close'].rolling(window=5).mean()
    print("\nFirst 10 values of Rolling Mean (Window=5):")
    print(subset['MA_5'].head(10))

    # 3. Moving Average (Rolling Window of 10)
    subset['MA_10'] = subset['close'].rolling(window=10).mean()

    # 4. Create Plot for Comparison
    plt.figure()
    plt.plot(subset['close'], label='Original Close Price', color='gray', alpha=0.5)
    plt.plot(subset['MA_5'], label='Rolling Mean (Window=5)', color='red', linewidth=2)
    plt.plot(subset['MA_10'], label='Rolling Mean (Window=10)', color='blue', linewidth=2)
    
    plt.title('Apple Stock: Moving Average Model (Window 5 vs 10)')
    plt.xlabel('Days')
    plt.ylabel('Price ($)')
    plt.legend()
    plt.grid(True, alpha=0.3)
    plt.show()

```

## Exponential Smoothing:

```

import pandas as pd
import matplotlib.pyplot as plt
from statsmodels.tsa.holtwinters import SimpleExpSmoothing
import os
import warnings
warnings.filterwarnings('ignore')

# --- Independent Path Finder ---
file_path = None
for path in ['/content/aapl_master_enriched.csv', 'aapl_master_enriched.csv', '/aapl_master_enriched.csv']:
    if os.path.exists(path):
        file_path = path
        break

if file_path:
    df = pd.read_csv(file_path)
    # Using a subset for visibility
    data = df['close'].head(150)

    # Perform Simple Exponential Smoothing
    # model.fit(smoothing_level=0.2) gives more weight to past data, 0.8 to recent data
    model = SimpleExpSmoothing(data).fit(smoothing_level=0.3, optimized=False)
    smoothed_data = model.fittedvalues

    # Plot the results
    plt.figure(figsize=(12, 6))
    plt.plot(data, label='Original Apple Stock Price', color='black', alpha=0.4)
    plt.plot(smoothed_data, label='Exponential Smoothing (alpha=0.3)', color='orange', linewidth=2)
    
    plt.title('Apple Stock Price: Exponential Smoothing Representation')
    plt.xlabel('Days')
    plt.ylabel('Price ($)')
    plt.legend()
    plt.grid(True, alpha=0.3)
    plt.show()

    print("Exponential Smoothing completed successfully.")


```

### OUTPUT:

<img width="663" height="591" alt="image" src="https://github.com/user-attachments/assets/dd53ae4d-55a1-4a6c-97c9-ac84a64c5737" />
<img width="637" height="479" alt="image" src="https://github.com/user-attachments/assets/40728f8a-0ab4-4b21-97d8-75edad4f07c1" />

### RESULT:
Thus we have successfully implemented the Moving Average Model and Exponential smoothing using python.
