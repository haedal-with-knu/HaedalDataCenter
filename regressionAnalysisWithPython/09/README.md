# 09. 회귀모델의 실제 응용

9장은 이론적 설명 없이 선형모델을 사용해 해결된 실질적인 데이터 과학 문제의 네 가지 실제 예제로 구성됩니다.  
회귀문제, 불균형 및 다중 클래스 분류 문제, 순위 문제, 시계열 문제 중 회귀문제를 정리하였습니다.  

* 데이터셋 다운로드

```python
pip install requests
```
```python
try:
    import urllib.request as urllib2
except:
    import urllib2

import requests, io, os
import zipfile, gzip

def download_from_UCI(UCI_url, dest):
    r = requests.get(UCI_url)
    filename = UCI_url.split('/')[-1]
    print ('Extracting in %s' % dest)
    try:
        os.mkdir(dest)
    except:
        pass
    with open (os.path.join(dest, filename), 'wb') as fh:
        print('\tdecompression %s' % filename)
        fh.write(r.content)
        
def unzip_from_UCI(UCI_url, dest):
    r = requests.get(UCI_url)
    z = zipfile.ZipFile(io.BytesIO(r.content))
    print ('Extracting in %s' % dest)
    
    for name in z.namelist():
        print ('\tunzipping %s' % name)
        z.extract(name, path=dest)

def gzip_from_UCi(UCI_url, dest):
    response = urllib2.urlopen(UCI_url)
    compressed_file = io.BytesIO(response.read())
    decompressed_file = gzip.GzipFile(fileobj=compessed_file)
    filename = UCI_url.split('/')[-1][:-4]
    print ('Extracting in %s' % dest)
    try:
        os.mkdir(dest)
    except:
        pass
    with open( os.path.join(dest, filename), 'wb') as outfile:
        print ('\tgunzipping %s' % filename)
        cnt = decompressed_file.read()
        outfile.write(cnt)
```
### 회귀 문제
* 노래에 대한 일부 설명이 주어지면 노래가 만들어진 연도를 모델
* 결과를 평가하기 위해 테스트셋을 구성하는 노래의 예측 연도와 실제 제작 연도사이의 평균 절대 오차(MAE)를 메트릭으로 사용<br/>
#### 데이터셋 다운로드
```python
UCI_url = 'https://archive.ics.uci.edu/ml/machine-learning-databases/00203/YearPredictionMSD.txt.zip' 
unzip_from_UCI(UCI_url, dest='./msd')
```
   Extracting in ./msd   
       unzipping YearPredictionMSD.txt  <br/>
#### 데이터셋 로드 및 분할

```python
#데이터셋 로드
import matplotlib.pyplot as plt
%matplotlib inline

import numpy as np
import pandas as pd

dataset = pd.read_csv('./msd/YearPredictionMSD.txt', header=None)

#데이터셋 분할(훈련,테스트)
X_train = dataset.iloc[:463715, 1:]
y_train = np.asarray(dataset.iloc[:463715, 0])

X_test = dataset.iloc[463715:, 1:]
y_test = np.asarray(dataset.iloc[463715:, 0])
```  
<br/>
<br/>
1. 바닐라 선형회귀를 사용하여 훈련시간, 훈련 집합 및 테스트 집합의 MAE 출력<br/>
<br/>

```python
from sklearn.linear_model import LinearRegression, SGDRegressor
from sklearn.model_selection import KFold
from sklearn.metrics import mean_absolute_error
import time

regr = LinearRegression()

tic = time.perf_counter()
regr.fit(X_train, y_train)
print("Training time [s]:", time.perf_counter()-tic)

print("MAE train set:", mean_absolute_error(y_train, regr.predict(X_train)))

print("MAE test set:", mean_absolute_error(y_test, regr.predict(X_test)))
```

Training time [s]: 1.395022800001243  
MAE train set: 6.79557016726623  
MAE test set: 6.800496463186952  
<br/>
약 1.4초 만에 MAE 6.8을 얻을 수 있습니다.  
훈련 집합의 MAE와 테스트 집합의 MAE 사이에 거의 차이가 없으므로 학습자는 안정적이라고 할 수 있습니다.  
<br/>
2. **SDG 회귀**를 사용하여 훈련 시간, 훈련 집합 및 테스트 집합의 MAE 출력

```python
regr = SGDRegressor()

tic = time.perf_counter()
regr.fit(X_train, y_train)
print("Training time [s]", time.perf_counter()-tic)

print("MAE train set:", mean_absolute_error(y_train, regr.predict(X_train)))
print("MAE test set:", mean_absolute_error(y_test, regr.predict(X_test)))
```

Training time [s] 66.66515119999895  
MAE train set: 412291516418517.0  
MAE test set: 418348223735912.0  

