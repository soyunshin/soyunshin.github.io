---
title:  "[kaggle 01] London bike sharing dataset 작성중"
excerpt: "Historical data for bike sharing in London 'Powered by TfL Open Data'"

categories:
  - Data Analytics
tags:
  - [Data Analytics]

toc: true
toc_sticky: true
 
date: 2021-09-05
last_modified_at: 2021-09-05
---


# 1. 필요한 환경 설정
```python
import numpy as np 
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import missingno as msno #결측치 시각화
```


```python
df = pd.read_csv('london_merged.csv', parse_dates=['timestamp'])
df.head()
```

```python
print('데이터 구조 : ', df.shape)
print('데이터의 타입 : ', df.dtypes)
```


```python
print('데이터의 columns : ', df.columns)
```


```python
df.describe()
```


```python
df.isna().sum() 
```

다음은 결측값이 존재하는지 확인하는 그래프, 현재 결측값이 존재하지않기때문에 빈 그래프를 보여준다.

```python
msno.matrix(df)
plt.show()
```


```python
df['year'] = df['timestamp'].dt.year
df['month'] = df['timestamp'].dt.month
df['dayofweek'] = df['timestamp'].dt.dayofweek
df['hour'] = df['timestamp'].dt.hour
df.head()
```

```python
df['year'].value_counts().sort_index()
```
```
2015    8643
2016    8699
2017      72
Name: year, dtype: int64
```

```python
df['month'].value_counts().sort_index()
```
```
1     1487
2     1359
3     1468
4     1438
5     1488
6     1422
7     1481
8     1484
9     1394
10    1479
11    1430
12    1484
Name: month, dtype: int64
```


```python
df['dayofweek'].value_counts().sort_index()
```
```
0    2508
1    2505
2    2489
3    2492
4    2450
5    2465
6    2505
Name: dayofweek, dtype: int64
```


```python
df['hour'].value_counts().sort_index()
```
```
0     724
1     724
2     721
3     721
4     721
5     721
6     726
7     726
8     724
9     727
10    725
11    727
12    729
13    728
14    728
15    729
16    730
17    728
18    728
19    727
20    727
21    726
22    725
23    722
Name: hour, dtype: int64
```
<br>

# 2. seaborn으로 그래프그리기

연도별 자전거 이용객
```python
a, b = plt.subplots(1,1, figsize=(10,5))
sns.boxplot(df['year'], df['cnt'])
```
월별

```python
a, b = plt.subplots(1,1, figsize=(10,5))
sns.boxplot(df['month'], df['cnt'])
```
```python
a, b = plt.subplots(1,1, figsize=(10,5))
sns.boxplot(df['dayofweek'], df['cnt'])
```

```python
a, b = plt.subplots(1,1, figsize=(10,5))
sns.boxplot(df['hour'], df['cnt'])
```
출퇴근시간에 주로 자전거를 이용한다는 사실을 알 수 있다.

```python
#그래프 생성 함수
def plot_bar(data, feature) :
	fig = plt.figsize(figsize=(12,3))
	sns.barplot(x=feature, y='cnt', data=data, palette='Set3', orient='V')
```


```python
plot_bar(df, 'hour')
```

```python
plot_bar(df, 'dayofweek')
```


<br>

# 3. 데이터 전처리

이상치 제거

```python
def is_outliers(s) :
	lower_limit = s.mean() - (s.std()*3)
	upper_limit = s.mean() + (s.std()*3)
	return ~s.between(lower_limit, upper_limit)
```

```python
df_out =df[~df.groupby('hour')['cnt'].apply(is_outlier)]

print('이상치 제거 전 : ', df.shape)
print('이상치 제거 후 : ', df_out.shape)
```

```python
df_out.dtypes
```

```python
df_out['weather_code'] = df_out['weather_code'].astype('category')
df_out['season'] = df_out['season'].astype('category')
df_out['year'] = df_out['year'].astype('category')
df_out['month'] = df_out['month'].astype('category')
df_out['hour'] = df_out['hour'].astype('category')
```

```python
#더미변수 처리
df_out['season']

df_out = pd.get_dummies(df_out, columns=['weather_code', 'season', 'year', 'month', 'hour'])
```

```python
# 더미변수화
df_out.head()
```
```python
# 59개 컬럼이 생김
df_out.shape
```

```python
#종속변수
df_y = df_out['cnt']

#독립변수
df_x = df_out.drop(['timestamp', 'cnt'], axis=1)
#axis =1 이면 열
```

```python
df_x.head()
```
```python
df_y.head()
```


```python
from sklearn.model_selection import train_test_split
```

```python
x_train, x_test, y_train, y_test = train_test_split(df_x, df_y, random_state=66, test_size=0.3, shuffle=False) #시계열 데이터는 섞으면 안됨
```

```python
print('x_train 구조', x_train.shape)
print('y_train 구조', y_train.shape)

print('x_test 구조', x_test.shape)
print('y_test 구조', y_test.shape)
```

<br>

# 4. model prediction

간단한 딥러닝 모델로 런던자전거의 시간대별 수요 예측

```python
import keras
from keras.models import Sequential
from keras.layers import Dense
from keras.callbacks import EarlyStopping
```

```python
model = Sequential()
model.add(Dense(units=160, activation='relu', input_dim=57))
model.add(Dense(units=60, activation='relu'))
model.add(Dense(units=20, activation='relu'))
model.add(Dense(units=1, activation='linear'))
```

```python
model.summary()
```

```python
model.compile(loss='mae', optimizer='adam', metrics=['mae'])
early_stopping=EarlyStopping(monitor='loss', patience=5, mode='min')
history = model.fit(x_train, y_train, epochs=50, batch_size=1, validation_split=0.1, callbacks=[early_stopping])
```