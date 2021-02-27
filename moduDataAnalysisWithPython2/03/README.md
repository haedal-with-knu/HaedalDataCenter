# 3.인구 공공 데이터

## unit 07.  우리 동네 인구 구조 시각화하기

1. ### 인구 공공 데이터 내려받기

   - 행정안전부에서 인구 데이터를 내려받기

2. ### 인구 데이터 살펴보고 질문하기

   - 본인 동네 찾아보기

3. ### 우리 동네 인구 구조 시각화하기

   1. 인구 데이터 파일을 읽어온다.

   2. 전체 데이터에서 한 줄씩 반복해서 읽어온다.

   3. 우리 동네에 대한 데이터인지 확인한다.

   4. 우리 동네일 경우 0세부터 100세 이상까지의 인구수를 순서대로 저장한다.

   5. 저장된 연령별 인구수 데이터를 시각화한다.

      데이터 불러오기

      ```python
      import csv
      f = open('age.csv')
      data = csv.reader(f)
      result=[]
      for row in data:
      	if '신도림' in row[0]:
      		for i in row[3:]:
      		result.append(int(i))
      print(result)
      ```

      시각화하기

      ```python
      import matplotlib.pyplot as plt
      plt.style.use('ggplot')
      plt.plot(result)
      plt.show()
      ```

      

## unit 08. 인구 구조를 다양한 형태로 시각화하기

​	먼저 인구 구조가 궁금한 지역의 이름을 input() 함수로 입력 받기.

```python
import csv
f = open('age.csv')
data = csv.reader(f)
result=[]
name = input('지역 입력:')

for row in data:
	if name in row[0]:
		for i in row[3:]:
		result.append(int(i.replace(',','')))

import matplotlib.pyplot as plt
plt.style.use('ggplot')
plt.rc('font', family = 'Malgun Gothic')
plt.title(name+'지역의 인구 구조')
plt.plot(result)
plt.show()
```



1. ### 막대그래프 그리기

   - bar() 함수

     bar(막대를 표시할 위치, 막대의 높이)

     

   - barh() 함수

     ```python
     plt.barh(range(101),result)
     ```

     

2. ### 항아리 모양 그래프 그리기

   - 데이터 수집하기

     ```python
     import csv
     import matplotlib.pyplot as plt
     
     f= open('gender.csv')
     data = csv.reader(f)
     m=[]
     f=[]
     
     for row in data:
         for i in row[3:104]:
             m.append(-int(i))
         for i in row[106:]:
             m.append(int(i))
     ```

     

   - 데이터 시각화하기

     ```python
     plt.barh(range(101),m)
     plt.barh(range(101),f)
     plt.show()
     ```

     

## unit 09. 우리 동네 인구 구조를 파이 차트로 나타내기

1. ### 제주도에는 여성의 비율이 더 높을까?

   - 항아리 모양 그래프

     ```python
     import csv
     import matplotlib.pyplot as plt
     
     f= open('gender.csv')
     data = csv.reader(f)
     m=[]
     f=[]
     
     for row in data:
         for i in row[3:104]:
             m.append(-int(i))
         for i in row[106:]:
             m.append(int(i))
     
     plt.style.use('ggplot')
     plt.figure(figsize=(10,5),dpi =300)
     plt.rc('font',family='Malgun Gothic')
     plt.rcParams['axes.unicode_minus'] = False
     plt.title(name+' 지역의 남녀 성병 인구 분포')
     plt.barh(range(101),m)
     plt.barh(range(101),f)
     plt.show()        
     ```

     

   - 데이터의 개숫를 출력

     ```python
     print(len(m), len(f))
     ```

     

   - 입력받는 코드 추가, break 추가

     ```python
     name = input('지역 입력:')
     for row in data:
     	if name in row[0]:
     	for i in row[3:104]:
     		m.append(-int(i))
         for i in row[106:]:
             f.append(int(i))
         break
     ```

     

2. ### 혈액형 비율 표현하기

   - pie() 함수

     ```python
     plt.pie([10,20])
     ```

     

3. ### 제주도의 성별 인구 비율 표현하기

   ```python
   import matplotlib.pyplot as plt
   plt.rc('font', family = 'Malgun Gothic')
   color = ['crimson', 'darkcyan']
   plt.axis('equal')
   plt.pie(size, labels = ['남', '여'], autopct='%.1%%', colors=color,startangle=90)
   plt.title(name+'지역의 남녀 성별 비율')
   plt.show()
   ```

   

## unit 10. 우리 동네 인구 구조를 산점도로 나타내기

1. ### 꺾은선 그래프로 표현하기

   ```python
   import csv
   import matplotlib.pyplot as plt
   
   f= open('gender.csv')
   data = csv.reader(f)
   m=[]
   f=[]
   
   name = input('동네 입력:')
   
   for row in data:
       if name in row[0]:
           for i in range(3,104):
               m.append(int(row[i]))
               f.append(int(row[i+103]))
           break
   
   plt.plot(m, label='Male')
   plt.plot(f, label='Female')
   plt.legend()
   plt.show()        
   ```

   

2. ### 막대그래프로 표현하기

   ```python
   import csv
   import matplotlib.pyplot as plt
   
   f= open('gender.csv')
   data = csv.reader(f)
   result=[]
   
   name = input('동네 입력:')
   
   for row in data:
       if name in row[0]:
           for i in range(3,104):
   	   		result.append(int(row[i])-int(row[i+103]))
           break
   
   plt.bar(range(101),result)
   plt.show()   
   ```

   

3. ### 산점도로 표현하기

   - 데이터 간의 관계를 파악하느데 도움이 되는 산점도

   - 산점도는 가로축과 세로축을 기준으로 두 요소가 서로 어떤 관계를 맺고 있는지를 쉽게 나타낸 그래프

   - 버블 차트: 데이터를 의미하는 점들의 분포로 상관관계를 파악할 수 있다는 점에서 산점도와 비슷

     

4. ### scatter() 함수로 표현하기

   ```python
   plt.scatter([1,2,3,4],[10,20,30,40])
   plt.show()
   ```

   

5. ### 버블 차트로 표현하기

   ```python
   plt.scatter([1,2,3,4],[10,20,30,40], s=[100,200,250,300], c=['red','blue','green', 'gold'])
   plt.show()
   ```

   ```python
   plt.scatter([1,2,3,4],[10,20,30,40], s=[100,200,250,300], c=range(4))
   plt.colorbar()
   plt.show()
   ```

   ```python
   plt.scatter([1,2,3,4],[10,20,30,40], s=[100,200,250,300], c=range(4),cmap='jet')
   plt.colorbar()
   plt.show()
   ```

   

6. ### 제주도의 연령대별 성별 비율을 산점도로 표현하기

   ```python
   import csv
   import matplotlib.pyplot as plt
   
   f= open('gender.csv')
   data = csv.reader(f)
   m=[]
   f=[]
   
   name = input('동네 입력:')
   
   for row in data:
       if name in row[0]:
           for i in range(3,104):
               m.append(int(row[i]))
               f.append(int(row[i+103]))
           break
   
   plt.scatter(m,f,c=range(101),alpha=0.5, cmap='jet')
   plt.colorbar()
   plt.plot(range(max(m)), range(max(m)),'g')
   plt.show()     
   ```

   