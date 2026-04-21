# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 21-04-2026

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
data = pd.read_csv("/content/DailyDelhiClimateTest.csv")
data.head()
if data.index.name == 'date':
    data.reset_index(inplace=True)
data['date'] = pd.to_datetime(data['date'], format='%d-%m-%Y')
data.set_index('date', inplace=True)
data['humidity_diff'] = data['humidity']-data['humidity'].shift(1)
result = seasonal_decompose(data['humidity'], model='additive', period=12)
data['humidity_sea_diff'] = result.resid
data['humidity_log'] = np.log(data['humidity'])
data['humidity_log_diff'] = data['humidity_log']-data['humidity_log'].shift(1)
result = seasonal_decompose(data['humidity_log_diff'].dropna(), model='additive', period=12)
data['humidity_log_sea_diff'] = result.resid

plt.figure(figsize=(16,16))
plt.subplot(6,1,1)
plt.plot(data['humidity'],label = 'original')
plt.legend(loc = 'best')
plt.title('Original Data')
plt.xlabel('Date')
plt.ylabel('Humidity')

plt.subplot(6,1,2)
plt.plot(data['humidity_diff'],label = 'Regular Difference')
plt.legend(loc = 'best')
plt.title('Differenced Data')
plt.xlabel('Date')
plt.ylabel('Humidity')

plt.subplot(6,1,3)
plt.plot(data['humidity_sea_diff'],label = 'Seasonal Difference')
plt.legend(loc = 'best')
plt.title('Seasonal Differenced Data')
plt.xlabel('Date')
plt.ylabel('Humidity')

plt.subplot(6,1,4)
plt.plot(data['humidity_log'],label = 'Log Data')
plt.legend(loc = 'best')
plt.title('Log Data')
plt.xlabel('Date')
plt.ylabel('Humidity')

plt.subplot(6,1,5)
plt.plot(data['humidity_log_diff'],label = 'Log Difference')
plt.legend(loc = 'best')
plt.title('Log Differenced Data')
plt.xlabel('Date')
plt.ylabel('Humidity')

plt.subplot(6,1,6)
plt.plot(data['humidity_log_sea_diff'],label = 'Log Seasonal Difference')
plt.legend(loc = 'best')
plt.title('Log Seasonal Differenced Data')
plt.xlabel('Date')
plt.ylabel('Humidity')

```


### OUTPUT:
ORIGINAL DATA:
<img width="1614" height="323" alt="Screenshot 2026-04-21 094633" src="https://github.com/user-attachments/assets/084322e2-4010-4e36-8b77-bba89dedbb19" />


REGULAR DIFFERENCING:
<img width="864" height="206" alt="Screenshot 2026-04-21 094646" src="https://github.com/user-attachments/assets/bb135128-c138-4a6e-9bd3-051b7d1e554b" />



SEASONAL ADJUSTMENT:
<img width="578" height="138" alt="image" src="https://github.com/user-attachments/assets/9cee937f-f919-4b35-a086-554c0cbc73f3" />


LOG TRANSFORMATION:
<img width="554" height="138" alt="image" src="https://github.com/user-attachments/assets/72f0d9df-743b-4ee3-9509-62a12b6b7025" />


LOG DIFFERENCED DATA:
<img width="578" height="138" alt="image" src="https://github.com/user-attachments/assets/19864bfc-9755-4e83-aab5-f5dace187325" />

LOG SEASONAL DIFFERENCED DATA:
<img width="591" height="138" alt="image" src="https://github.com/user-attachments/assets/8b4f53d5-5dec-4212-bbc1-3a51e5095ad1" />




### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
