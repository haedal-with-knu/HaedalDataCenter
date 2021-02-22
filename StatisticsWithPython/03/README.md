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
fish_data
```
