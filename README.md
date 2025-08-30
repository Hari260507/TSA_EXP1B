# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 30/8/2025
# Name: M. Harekrishnaa
# Dep: CSE

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on international airline passenger data
### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
### PROGRAM:
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose

# Load tomato dataset
data = pd.read_csv("/content/Tomato.csv")

# Convert Date to datetime
data['Date'] = pd.to_datetime(data['Date'])

# Group by Date and take mean of Average price
data = data.groupby('Date')['Average'].mean().reset_index()
data.set_index('Date', inplace=True)

# Regular difference
data['avg_diff'] = data['Average'] - data['Average'].shift(1)

# Seasonal decomposition on Average
result = seasonal_decompose(data['Average'], model='additive', period=52)
data['avg_sea_diff'] = result.resid

# Log transformation
data['avg_log'] = np.log(data['Average'])

# Log differencing
data['avg_log_diff'] = data['avg_log'] - data['avg_log'].shift(1)

# Seasonal decomposition on log-differenced data
result = seasonal_decompose(data['avg_log_diff'].dropna(), model='additive', period=52)
data['avg_log_seasonal_diff'] = result.resid

# Plot results
plt.figure(figsize=(16, 16))

plt.subplot(6, 1, 1)
plt.plot(data['Average'], label='Original')
plt.legend(loc='best')
plt.title('Original Data - Tomato Average Price')
plt.xlabel('Year')
plt.ylabel('Average Price')

plt.subplot(6, 1, 2)
plt.plot(data['avg_diff'], label='Regular Difference')
plt.legend(loc='best')
plt.title('Regular Differencing')
plt.xlabel('Year')
plt.ylabel('Differenced Price')

plt.subplot(6, 1, 3)
plt.plot(data['avg_sea_diff'], label='Seasonal Adjustment')
plt.legend(loc='best')
plt.title('Seasonal Adjustment')
plt.xlabel('Year')
plt.ylabel('Seasonally Adjusted Price')

plt.subplot(6, 1, 4)
plt.plot(data['avg_log'], label='Log Transformation')
plt.legend(loc='best')
plt.title('Log Transformation')
plt.xlabel('Year')
plt.ylabel('Log(Average Price)')

plt.subplot(6, 1, 5)
plt.plot(data['avg_log_diff'], label='Log Transformation and Regular Differencing')
plt.legend(loc='best')
plt.title('Log Transformation and Regular Differencing')
plt.xlabel('Year')
plt.ylabel('RDiff(Log(Average Price)))')

plt.subplot(6, 1, 6)
plt.plot(data['avg_log_seasonal_diff'], label='Log Transformation + Regular Differencing + Seasonal Differencing')
plt.legend(loc='best')
plt.title('Log Transformation + Regular Differencing + Seasonal Differencing')
plt.xlabel('Year')
plt.ylabel('SDiff(RDiff(Log(Average Price)))')

plt.tight_layout()
plt.show()

```

### OUTPUT:



REGULAR DIFFERENCING:

<img width="1739" height="288" alt="image" src="https://github.com/user-attachments/assets/26c6d79f-3376-4449-9b16-6ac01f3cc77a" />

SEASONAL ADJUSTMENT:

<img width="1741" height="287" alt="image" src="https://github.com/user-attachments/assets/107468b2-f238-47c6-b240-f900f446a83d" />

LOG TRANSFORMATION:

<img width="1740" height="295" alt="image" src="https://github.com/user-attachments/assets/43d1a8c0-841c-4901-b6d3-05c6b119593e" />


### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
