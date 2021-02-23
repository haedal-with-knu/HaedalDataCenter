# 03. 파이썬을 이용한 데이터 분석
## 3.1 파이썬을 이용한 기술 통계(1변량 데이터)
#### 3.1.1 통계 처리와 scipy
- 통계량의 계산이나 기본적인 데이터 분석에 사용되는 함수는 scipy패키지에 들어있음
```python
import numpy as np
import scipy as sp
```
#### 3.1.2 1변량 데이터의 관리
- 1변량 데이터:1가지 종류의 데이터만 가짐 ex.물고기의 몸길이
```python
fish_data = np.array([2,3,3,4,4,4,4,5,5,6])
```
```
array([2, 3, 3, 4, 4, 4, 4, 5, 5, 6])
```

#### 3.1.3 합계와 샘플사이즈
- 합계값을 계산하는 sp.sum() 또는 np.sum()
```python
np.sum(fish_data)
```
- 샘플 사이즈를 계산하는 파이썬 표준함수 len()
```python
len(fish_data)
```
#### 3.1.4 평균값(기댓값)
- 합계값 / 샘플사이즈
```python
N = len(fish_data) #샘플사이즈
sum_value = np.sum(fish_data) #합계값
mu = sum_value / N #평균값
```
- 버전에 따라 sp.mean() 또는 np.mean() 로 간단하게
```python
np.mean(fish_data)
```
#### 3.1.5 표본분산
- 분산:데이터가 평균값에서 얼마나 떨어져있는지 나타내는 지표
- 편차제곱의 합을 샘플사이즈로 나눔
```python
sigma_2_sample = np.sum((fish_data - mu) ** 2) / N
sigma_2_sample
```
- 버전에 따라 sp.var() 또는 np.var() 로 간단하게
```python
np.var(fish_data, ddof=0) #ddof=delta degree of freedom(자유도)
```
#### 3.1.6 불편분산
- 과소추정된 분산을 피하기 위해 샘플사이즈 - 1
```python
sigma_2 = np.sum((fish_data - mu)**2)/(N-1) #N이 아닌 N-1로 나눔
sigma_2 #분산이 조금 더 커진다
```
- np.var()쓸 땐 ddof = 1 로 지정
```python
np.var(fish_data, ddof=1) #자유도를 1로 지정
```
#### 3.1.7 표준편차
- 분산에 루트를 취함
```python
sigma = np.sqrt(sigma_2)
```
- sp.std() or np.std() 함수
```python
np.std(fish_data,ddof=1)
```
#### 3.1.8 표준화
- 데이터의 평균을 0으로, 표준편차(분산)를 1로 변환
- 모든 데이터에서 평균값을 빼고
- 모든 데이터를 표준편차로 나눈다
```python
standard=(fish_data - mu) / sigma #평균이 0, 표준편차가 1인 데이터로 변환
```
#### 3.1.9 그 외의 통계량
- 최대값, 최소값, 중앙값
```python
np.amax(fish_data) #최대값
np.amin(fish_data) #최소값
np.median(fish_data) #중앙값:데이터를 순서대로 늘어놓았을 때 중간에 있는 수치
```
- 극단적으로 큰 물고기 한마리가 있는 경우
- 아래 fish_data_2의 100과 같은 값을 이상치라고 한다
- 평균값은 이상치에 민감하다
```python
fish_data_2=np.array([2,3,3,4,4,4,4,5,5,100])
```
#### 3.1.10 scipy/stats와 사분위수
- 사분위수:데이터를 순서대로 늘어놓았을 때 아래에서부터 25%, 75%에 해당하는 값
```python
from scipy import stats #scipy 패키지 안에 있는 통계 분석에 특화된 함수
fish_data_3 = np.array([1,2,3,4,5,6,7,8,9])
stats.scoreatpercentile(fish_data_3,25) #25%에 해당하는 값
stats.scoreatpercentile(fish_data_3,75) #75%에 해당하는 값
```
## 3.2 파이썬을 이용한 기술통계:다변량 데이터
- 다변량 데이터:여러 개의 변수를 조합한 데이터 ex.구두 판매액과 구두 색의 조합
#### 3.2.1 깔끔한 데이터
- 깔끔한 데이터:분석하기 쉽게 정리한 표 형태의 데이터
- 깔끔한 데이터의 특징
 > 1. 개별 값이 하나의 셀을 이룬다
 > 2. 개별 변수가 하나의 열을 이룬다
 > 3. 개별 관측이 하나의 행을 이룬다
 > 4. 개별 관측 유닛 유형이 하나의 표를 이룬다
- 깔끔한 데이터를 사용하면 복잡한 데이터를 모을 때 통일성 있는 처리를 할 수 있다
#### 3.2.2 지저분한 데이터
- 깔끔한 데이터가 아닌 데이터
#### 3.2.3 교차분석표
- 의미는 명확하지만 깔끔한 데이터는 아닌 형식의 데이터
- 분할표라고도 함
- 데이터를 분석할 때는 가능한 한 깔끔한 데이터가 되게 관리하고, 필요시 교차분석표로 변환해야하는 것이 좋다
#### 3.2.4 다변량 데이터 관리하기
- 깔끔한 데이터는 pandas의 데이터프레임으로 간단하게 관리할 수 있다.
```python
import pandas as pd
fish_multi=pd.read_csv("3-2-1-fish_multi.csv")
print(fish_multi)
```
