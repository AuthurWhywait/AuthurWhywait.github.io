---
layout: post
title: "几种回归算法以及一些衡量指标的源码"
description: "几种回归算法以及一些衡量指标的源码"
categories: [Python]
tags: [Code, SVR, MLR, GPR, RF, MSE, RMSE, MAE, MAPE, R2]
redirect_from:
  - /2022/07/02/
---

- Content
{:toc}

## 基础设置

```python
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
from sklearn.model_selection import train_test_split 
from sklearn.svm import SVR
from sklearn.metrics import mean_squared_error, r2_score, mean_absolute_percentage_error, mean_absolute_error
import time
```

## 衡量指标

各指标的计算并打印。

```python
n = 10000 # 每个方法的循环次数
tr = 0.2 # test rate
R2scores = np.zeros((n, 4))

def scores(y_test, y_hat):
  # mean square error
  MSE = mean_squared_error(y_test, y_hat)
  # root mean square error
  RMSE = np.sqrt(MSE)
  # mean absolute error
  MAE = mean_absolute_error(y_test, y_hat)
  # mean absolute percetage error
  MAPE = mean_absolute_percentage_error(y_test, y_hat)
  # r2 score: the proportion of the variance in the dependent variable that is predictable from the independent variable(s).
  R2 = r2_score(y_test, y_hat)
  return MSE, RMSE, MAE, MAPE, R2

def print_scores(method, scores_record):
  scores = scores_record.mean(axis=0)
  print(method, '的各指标')
  print('\tMSE:', scores[0].round(3))
  print('\tRMSE:', scores[1].round(3))
  print('\tMAE:', scores[2].round(3))
  print('\tMAPE:', scores[3].round(3))
  print('\tR2:', scores[4].round(3))
  # print('\tR2:', scores[4], "\tR2 std:", np.std(scores_record[:,3], ddof=1))
```

## Supported Vector Regression (SVR)

```python
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
from sklearn.model_selection import train_test_split 
from sklearn.svm import SVR
from sklearn.metrics import mean_squared_error, r2_score, mean_absolute_percentage_error

def svr_predict(train_data, train_label, test_data):
  svr = SVR(kernel='rbf', C=100, gamma=0.001, epsilon=0.1)
  svr.fit(train_data, train_label)
  predict = svr.predict(test_data)
  return predict

start = time.time()

scores_record1 = np.zeros((n, 5))
for i in range(0, n):
  x_train, x_test, y_train, y_test = train_test_split(x, y, test_size = tr)
  y_hat = svr_predict(x_train, y_train, x_test)
  ss = scores(y_test, y_hat)
  # print(y_test, '\n', y_hat)
  scores_record1[i,:] = ss[0], ss[1], ss[2], ss[3], ss[4]

end = time.time()
R2scores[:,0] = scores_record1[:,4]
print_scores('SVR', scores_record1)
print("\tRunning time:", end - start)
```

## Multiple Linear Regression (MLR)

```python
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
from sklearn import metrics
import numpy as np

from operator import mul
def mul_lr_predict(x_train, y_train, x_test):
  linreg = LinearRegression()
  model = linreg.fit(x_train, y_train)
  y_hat = linreg.predict(x_test)
  return y_hat

start = time.time()

scores_record2 = np.zeros((n, 5))
for i in range(0, n):
  x_train, x_test, y_train, y_test = train_test_split(x, y, test_size = tr)
  y_hat = mul_lr_predict(x_train, y_train, x_test)
  ss = scores(y_test, y_hat)
  scores_record2[i,:] = ss[0], ss[1], ss[2], ss[3], ss[4]

end = time.time()
R2scores[:,1] = scores_record2[:,4]

print_scores('MLR', scores_record2)
print("\tRunning time:", end - start)
```

## Gaussian Process Regression (GPR)

```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn.gaussian_process.kernels import RBF, ConstantKernel as C
from sklearn.gaussian_process import GaussianProcessRegressor

def gpr_predict(x_train, y_train, x_test):
  # kernel = C(1.0, (1e-3, 1e3)) * RBF(10, (0.5, 2))
  # gp = GaussianProcessRegressor(kernel=kernel, n_restarts_optimizer=9)
  gp = GaussianProcessRegressor(n_restarts_optimizer=9)
  gp.fit(x_train, y_train)
  means, sigmas = gp.predict(x_test, return_std=True)
  y_hat = means
  return y_hat

start = time.time()

scores_record3 = np.zeros((n, 5))
for i in range(0, n):
  x_train, x_test, y_train, y_test = train_test_split(x, y, test_size = tr)
  y_hat = gpr_predict(x_train, y_train, x_test)
  ss = scores(y_test, y_hat)
  scores_record3[i,:] = ss[0], ss[1], ss[2], ss[3], ss[4]

end = time.time()
R2scores[:,2] = scores_record3[:,4]

print_scores('GPR', scores_record3)
print("\tRunning time:", end - start)
```

## Random Forest Regression (RFR)

```python
import pandas as pd
import numpy as np
from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestRegressor

def rfr_predict(x_train, y_train, x_test):
  regressor = RandomForestRegressor(n_estimators=60, random_state=0)
  regressor.fit(x_train, y_train)
  y_hat = regressor.predict(x_test)
  return y_hat

start = time.time()

scores_record4 = np.zeros((n, 5))
for i in range(0, n):
  x_train, x_test, y_train, y_test = train_test_split(x, y, test_size = tr)
  y_hat = rfr_predict(x_train, y_train, x_test)
  ss = scores(y_test, y_hat)
  scores_record4[i,:] = ss[0], ss[1], ss[2], ss[3], ss[4]

end = time.time()
R2scores[:,3] = scores_record4[:,4]

print_scores('RFR', scores_record4)
print("\tRunning time:", end - start)
```

## 不同方法各指标的对比

### 源码以及图示输出

```python
df = pd.DataFrame(R2scores, columns=['SVR', 'MLR', 'GPR', 'RFR'])
# print(np.std(R2scores[:, 3]))
print(scores_record4[:,4])
print(df.describe().round(3))
```

```python
plt.figure()
ax = plt.gca()
ax.spines['right'].set_visible(False)
ax.spines['top'].set_visible(False)
labels = 'SVR', 'MLR', 'GPR', 'RFR'
plt.boxplot(R2scores[:], labels = labels, showfliers=False)
plt.ylabel('R2 scores')
plt.show()
```

<!-- ```python
plt.figure()
ax = plt.gca()
ax.spines['right'].set_visible(False)
ax.spines['top'].set_visible(False)
labels = 'SVR', 'MLR', 'RFR'
plt.boxplot([R2scores[:,0], R2scores[:,1], R2scores[:,3]], labels = labels, showfliers=False)
plt.ylabel('R2 scores')
plt.show()
``` -->

```python
plt.figure()
ax = plt.gca()
ax.spines['right'].set_visible(False)
ax.spines['top'].set_visible(False)
methods = 'SVR', 'MLR', 'GPR', 'RFR'
x = [30.74, 14.74, 36.48, 753.44]
plt.bar(methods, x)
plt.ylabel('running time (s)')

for a,b in zip(methods, x):
  plt.text(a, b+0.05, '%.2f' % b, ha='center', va='bottom', fontsize=12)
  
plt.show()
```
