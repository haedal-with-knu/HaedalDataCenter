# 2.데이터 시각화 기초

## unit 04. 기본그래프 그리기

1. ### matplotlib 라이브러리란?

   - 파이썬으로 데이터르 시각화하기 위해

   - pyplot 모듈 불러오기 

     ```python
     import matplotlib.pyplot as plt
     ```

2. ### 기본 그래프 그리기

   - 선그리기

     ```python
     import matplotlib.pyplot as plt
     plt.plot([10,20,30,40])
     plt.show()
     ```

     ```python
     import matplotlib.pyplot as plt
     plt.plot([1,2,3,4],[12,43,25,15])
     plt.show()
     ```

3. ### 그래프에 옵션 추가하기

   - 그래프에 제목 넣기

     ```python
     import matplotlib.pyplot as plt
     plt.title('plotting')
     plt.plot([10,20,30,40])
     plt.show()
     ```

   - 그래프에 범례 넣기

     ```python
     import matplotlib.pyplot as plt
     plt.title('legend')
     plt.plot([10,20,30,40], label='asc')
     plt.legend()
     plt.show()
     ```

   - 그래프 색상 바꾸기

     ```python
     import matplotlib.pyplot as plt
     plt.title('color')
     plt.plot([10,20,30,40],color='skyblue')
     plt.show()
     ```

   - 그래프 선 모양 바꾸기

     ```python
     import matplotlib.pyplot as plt
     plt.title('linestyle')
     plt.plot([10,20,30,40],linestyle='--')
     plt.show()
     ```

   - 마커 모양 바꾸기

     ```python
     import matplotlib.pyplot as plt
     plt.title('marker')
     plt.plot([10,20,30,40],'r.')
     plt.show()
     ```

     *색상과 선 모양과 마커 모양을 동시에 설정하고 싶을 때는 '색상-마커모양-선모양' 순으로 코드를 작성

     

## unit 05. 내 생일의 기온 변화를 그래프로 그리기

1. ### 데이터에  질문하기

   - 데이터 읽어오기

     ```python
     import scv
     f= open('seoul.csv')
     data = csv.reader(f)
     
     for row in data :
         print(row)
     ```

     

   - next() 함수 : 첫 줄 제외

     ```python
     import scv
     f= open('seoul.csv')
     data = csv.reader(f)
     next(data)
     
     for row in data :
         print(row[-1])
     ```

     

   - 데이터 리스트에 저장하기

     ```python
     import scv
     f= open('seoul.csv')
     data = csv.reader(f)
     next(data)
     result=[]
     
     for row in data :
        if row[-1] != '':
         result.append(float(row[-1]))
     print(result)
     ```

     

2. ### 데이터 시각화하기

   ```python
   import scv
   import matplotlib.pyplot as plt
   
   f= open('seoul.csv')
   data = csv.reader(f)
   next(data)
   result=[]
   
   for row in data :
      if row[-1] != '':
       result.append(float(row[-1]))
   
   plt.plot(result,'r')
   plt.show()
   ```

   

3. ### 날짜 데이터 추출하기 

   - split()

     ```python
     s='hello python'
     print(s.split())
     ```

     최고 기온, 최저 기온 데이터 나타내기

     ```python
     import scv
     import matplotlib.pyplot as plt
     
     f= open('seoul.csv')
     data = csv.reader(f)
     next(data)
     high=[]
     low=[]
     
     for row in data :
        if row[-1] != '' and row[-2] != '':
         if 1983 <= int(row[0].split('-')[0]):
             if row[0].split('-')[1] == '04' and row[0].split('-')[2] == '13':
                 high.append(float(row[-1]))
                 low.append(float(row[-2]))
     
     plt.rc('font', family='Malgun Gothic')
     plt.rcParams['axes.unicode_minus'] = False
     plt.title('내 생일의 기온 변화 그래프')
     plt.plot(high,'hotpink',label = 'high')
plt.plot(low,'skyblue', label = 'low')
     plt.legend()
     plt.show()
     ```
     
     

## unit 06. 기온 데이터를 다양하게 시각화하기

1. ### 데이터에  질문하기

   - 데이터도 보는 관점에 따라 다르게 해석될 수 있다.

2. ### 히스토그램

   - hist() 함수

     ```python
     import matplotlib.pyplot as plt
     plt.hist([1,1,2,3,4,5,6,7,8,10])
     plt.show()
     ```

     

   - 주사위 시뮬레이션

     ```python
     import random
     dice = []
     for i in range(100):
         dice.append(random.randint(1,6))
     print(dice)
     plt.hist(dice, bins=6)
     plt.show()
     ```

     

3. ### 기온 데이터를 히스토그램으로 표현하기

   - 1907년 ~ 2018년까지 수집된 서울의 기온 데이터 히스토그램

     ```python
     import matplotlib.pyplot as plt
     import csv
     
     f = open('seoul.csv')
     data = csv.reader(f)
     next(data)
     result = []
     
     for row in data:
         if row[-1] != '':
             result.append(float(row[-1]))
     plt.hist(result, bins= 100, color='r')
     plt.show()
     ```

   - 1월, 8월 데이터만 사용

     ```python
     import matplotlib.pyplot as plt
     import csv
     
     f = open('seoul.csv')
     data = csv.reader(f)
     next(data)
     aug = []
     jan = []
     
     for row in data:
         month = row[0].split('-')[1]
         if row[-1] != '':
             if month == '08':
             	aug.append(float(row[-1]))
             if month == '01':
             	jan.append(float(row[-1]))
                 
     plt.hist(jan, bins= 100, color='r')
     plt.hist(aug, bins= 100, color='r')
     plt.show()
     ```

     

4. ### 기온 데이터를 상자 그림으로 표현하기

   - boxplot()

     ```python
     import matplotlib.pyplot as plt
     import csv
     
     f = open('seoul.csv')
     data = csv.reader(f)
     next(data)
     aug = []
     jan = []
     
     for row in data:
         month = row[0].split('-')[1]
         if row[-1] != '':
             if month == '08':
             	aug.append(float(row[-1]))
             if month == '01':
             	jan.append(float(row[-1]))
                 
     plt.boxplot(jan)
     plt.boxplot(aug)
     plt.show()
     ```

     8월의 최고 기온 데이터와 1월의 최고 기온 데이터를 원소로 하는 리스트를 boxplot() 함수로 표현

     ```
     plt.boxplot([aug,jan]) 
     ```

   - 데이터를 월별로 분류하는 경우

     ```python
     import matplotlib.pyplot as plt
     import csv
     
     f = open('seoul.csv')
     data = csv.reader(f)
     next(data)
     
     month = [[],[],[],[],[],[],[],[],[],[],[],[]]
     
     for row in data:
         if row[-1] != '':
             month[int(row[0].split('-')[1])-1].append(float(row[-1]))
     plt.boxplot(month)
     plt.show()
     ```

     