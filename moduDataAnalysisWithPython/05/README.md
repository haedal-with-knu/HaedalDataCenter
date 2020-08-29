# 05. 파이썬 데이터 분석 라이브러리를 활용한 프로젝트

우리는 앞서 matplotlib 라이브러리를 활용해 데이터를 다양하게 시각화하는 방법을 배웠습니다. 다섯째 마당에서는 한 걸을 더 나아가, 여러 가지 숫자 데이터를 다룰 수 있는 numpy 라이브러리와 이를 기반으로 한 pandas 라이브러리 사용법을 알아보겠습니다.

## UNIT 13. 숫자 데이터를 쉽게 다루게 돕는 numpy 라이브러리

지금까지 우리가 다룬 matplotlib 라이브러리는 아주 기초적인 내용이고, 그중에서도 자주 사용되는 기능들을 중심으로 살펴보았습니다. 더 자세한 내용이 궁금한 사람을 위해 이번 장에서는 matplotlib 홈페이지를 살펴보고 여러 가지 숫자 데이터를 다룰 수 있는 numpy 라이브러리를 실습해 봅시다.

### 1. matplotlib 홈페이지

matplotlib 홈페이지는 데이터 시각화와 관련된 다양한 예시를 제공하고 있습니다. 원하는 예시를 클릭하면 해당 그래프를 어떻게 그렸는지 알 수 있는 코드도 함께 제시하고 있습니다.
matplotlib.org에 접속한 후 상단에 있는 tutorials 메뉴를 클릭합니다.

[그림 13-1]

튜토리얼(tutorial)은 자습서 또는 안내서 성격의 문서로, matplotlib 라이브러리 뿐만 아니라 새로운 내용을 배울 때 '(찾고자 하는)키워드 tutorial'과 같은 형태로 검색하면 처음 시작할 때 큰 도움이 되는 내용을 찾을 수 있습니다.
연습 삼아서 검색 창에 numpy tutorial이라는 검색어를 입력해보세요.

[그림 13-2]

검색 결과 페이지에서 스크롤을 내려 Pyplot tutorial을 클릭합니다.

[그림 13-3]

내용을 살펴보면 지금까지 배운 내용들이 잘 정리되어 있습니다. 그중에서 다음과 같은 코드와 실행 결과가 보입니다.

    import matplotlib.pyplot as plt
    import numpy as np
    t = np.arange(0., 5., 0.2)
    plt.plot(t, t, 'r--', t, t**2, 'bs', t, t**3, 'g^')
    plt.show()

[그림 13-4]

코드 2행을 보니 numpy 라이브러리를 np라는 별명으로 부르는 것을 확인할 수 있습니다. 이 코드는 파이썬 리스트를 사용해서 다음과 같이 구현할 수 있습니다.

    import matplotlib.pyplot as plt
    t = []
    p2 = []
    p3 = []
    for i in range(0, 50, 2) :
        t.append(i / 10)
        p2.append((i / 10) ** 2)
        p3.append((i / 10) ** 3)
    plt.plot(t, t, 'r--', t, p2, 'bs', t, p3, 'g^')
    plt.show()

실행하면 그림 13-4와 동일한 그래프가 나옵니다.
numpy 라이브러리를 사용한 코드와 파이썬 리스트를 사용한 코드의 실행 결과는 똑같지만, numpy 라이브러리를 사용한 경우가 훨씬 적은 수의 코드로 작성하여 간결합니다.
그리고 홈페이지에 소개된 내용을 더 살펴보면 이 예제뿐만 아니라 다른 예제에서도 np로 시작하는 numpy 라이브러리를 활용하는 코드들을 많이 볼 수 있습니다.
여러분도 이번 장에서 numpy 라이브러리를 배우면 숫자 데이터를 더 쉽게 다룰 수 있을 겁니다. 그러면 지금부터 numpy 라이브러리의 기초에 대해 하나씩 살펴 보겠습니다.

### 2. numpy 라이브러리 시작하기

먼저 간단한 함수부터 살펴보겠습니다. 다음 코드는 2의 제곱근을 출력합니다.

    import numpy
    print(numpy.sqrt(2))


    실행 결과: 1.4142135623730951

그리고 앞에서 잠시 살펴봤던 것처럼 보통의 경우에는 다음과 같이 numpy 라이브러리를 np라는 이름의 별명으로 줄여서 쓸 수 있습니다.

    import numpy as np
    print(np.sqrt(2))

이번엔 파이와 삼각함수를 사용하는 방법을 살펴보겠습니다. 다음과 같이 np.pi라고 작성하면 파이 값을 활용할 수 있습니다.

    import numpy as np
    print(np.pi)
    print(np.sin(0))
    print(np.cos(np.pi))


    실행 결과:   3.141592653589793
                0.0
                -1.0

다음으로 무작위 값을 생성하는 랜덤 함수를 살펴보겠습니다. random 라이브러리를 통해서도 다양한 랜덤 함수를 사용할 수 있었지요? numpy 라이브러리의 랜덤 함수와 어떤 차이점이 있을지 생각하며 실습해 봅시다.
numpy 라이브러리에는 다양한 서브(sub) 라이브러리가 있는데 그 중 random 서브 라이브러리에 있는 rand() 함수를 실행하면 0~1 사이에 있는 n개의 실수가 랜덤하게 생성됩니다.

    import numpy as np
    a = np.random.rand(5)
    print(a)
    print(type(a))


    실행 결과:   [0.49035568 0.69782018 0.12051989 0.27050388 0.73912559]
                <class 'numpy.ndarray'>

실행 결과를 확인해보니 리스트와 비슷하게 생긴 numpy.ndarray 타입의 데이터가 생성된 것을 볼 수 있습니다. ndarray에서 nd는 N - Dimensional, 즉 'N 차원'이라는 의미이고 array는 '배열'이라는 의미입니다.
이 코드는 어떻게 보면 random 라이브러리의 randint() 함수의 실수(real number) 버전이라고 생각할 수 있습니다.
그리고 이번에 살펴볼 choice() 함수는 random 라이브러리에서는 표현하기 어려운 랜덤 데이터를 생성합니다.

    import numpy as np
    print(np.random.choice(6, 10))


    실행 결과: [1 5 3 0 5 1 0 4 0 1]

실행 결과에서 짐작할 수 있듯이 0~5 사이의 숫자를 랜덤하게 10번 선택했습니다. 만약 한 번 뽑은 숫자를 다시 뽑지 못하게 하고 싶다면 replace 속성을 False로 설정하면 됩니다.
다음처럼 말이죠.

    print(np.random.choice(10, 6, replace=False))

    실행 결과: [1 8 3 4 7 2]

    Tip: 여기에서는 0~9 사이에 있는 숫자를 중복 없이 6번 뽑았습니다.

여기에 확률을 지정할 수 잇는 p 속성을 추가하겠습니다. p 속성은 각 경우의 수가 발생할 확률을 정할 수 있습니다. 0~5까지의 경우가 발생할 수 있으므로 0이 나올 확률부터 5가 나올 확률까지 하나씩 지정할 수 있습니다.
따라서 이 경우에는 p 속성에 6개의 확률이 있어야 하고 그 합이 반드시 1이어야 합니다. 0은 0.1, 1은 0.2, 2는 0.3, 3은 0.2, 4는 0.1, 5는 0.1의 확률을 지정하여 프로그램을 실행하겠습니다.

    import numpy as np
    print(np.random.choice(6, 10, p=[0.1, 0.2, 0.3, 0.2, 0.1, 0.1]))

    실행 결과: [4 1 1 2 2 1 2 2 1 3]

0과 5는 나오지 않았고 1이 네번, 2가 4번, 3이 1번, 4가 1번 나왔네요. 한 번 더 실행하겠습니다.

    실행 결과: [1 2 1 2 2 2 2 2 4 2]

이번에는 0과 3과 5가 나오지 않았고, 1이 2번, 2가 6번, 4가 1번 나왔습니다. 꼭 우리가 정한 확률대로 결과가 나오지는 않는 것 같습니다.
더 많은 숫자를 발생시킨다면 p 속성으로 지정한 확률에 대한 검증이 가능할 것 같습니다. 얼마나 많은 숫자를 발생시켜야 할까요?
궁금증을 가지고 다음 내용으로 넘어가 봅시다.

### 3. numpy 라이브러리를 활용해 그래프 그리기

0부터 5까지의 숫자가 랜덤으로 출력되는 실행 결과를 보며, 각 숫자가 출력되는 횟수를 쉽게 확인하는 방법을 고민할 수 있습니다. 히스토그램을 그려 각 숫자의 빈도가 한눈에 들어오도록 합시다.
그리고 numpy 라이브러리의 장점을 확인하기 위해 Unit 6에서 random 라이브러리와 리스트를 사용했던 코드와 비교해 보겠습니다.

**numpy를 사용한 코드**

    import matplotlib.pyplot as plt
    import numpy as np
    dice = np.random.choice(6, 10)

    plt.hist(dice, bins =6)
    plt.show()

**Unit 6에서 사용한 코드**

    import matplotlib.pyplot as plt
    import numpy as np
    dice = []
    for i in range(10) :
        dice.append(np.random.randint(1,6))
    
    plt.hist(dice, bins = 6)
    plt.show()

[그림 13_5]

두 코드를 비교하니 결과는 같지만, numpy를 사용한 코드가 더 간결합니다.
그러고 반복 횟수를 10번이 아니라 100만 번으로 바꿔서 각각의 코드를 실행하면 numpy를 사용한 코드의 실행 속도가 훨씬 빠르다는 것을 느낄 수 있습니다.
여기에서 다음과 같이 p 속성으로 확률을 설정항여 결과를 확인하겠습니다.

    import matplotlib.pyplot as plt
    import numpy as np
    dice = np.random.choice(6, 1000000, p=[0.1, 0.2, 0.3, 0.2, 0.1, 0.1])
    plt.hist(dice, bins = 6)  #0,1,2,3,4,5 중 랜덤으로 추출한 숫자를 히스토그램 표현
    plt.show()

[그림 13_6]

반복 횟수를 늘려 더 많은 개수의 숫자를 랜덤으로 추출한 결과를 히스토그램으로 나타냈습니다. 그림 13-5와는 다르게 우리가 설정한 확률에 따라 각각의 값들이 나온 것을 확인할 수 있습니다.
다음은 Unit 10에서 그렸던 버블 차트를 numpy 라이브러리를 활용해서 다시 그리는 코드입니다. 반복문을 사용하지 않아서 코드가 간결해진 것을 느낄 수 잇을 겁니다.

<U>**코드**</U> **numpy를 사용한 버블 차트 그리기 코드**

    import matplotlib.pyplot as plt
    import numpy as np

    x = np.random.randint(10, 100, 200)
    y = np.random.randint(10, 100, 200)
    size = np.random.randint(100)

    plt.scatter(x, y, s=size, c=x, cmap='jet', alpha=0.7)
    plt.colorbar()
    plt.show()

<U>**코드**</U> **Unit 10에서 사용한 버블 차트 코드**

    import matplotlib.pyplot as plt
    import numpy as np

    x = []
    y = []
    size = []

    for i in range(200) :
        x.append(np.random.randint(10,100))
        y.append(np.random.randint(10,100))
        size.append(np.random.randint(10,100))

    plt.scatter(x, y, s=size, c=x, cmap='jet', alpha=0.7)
    plt.colorbar()
    plt.show()

[그림 13-7]

numpy.random.randint() 함수에 입력된 10, 100, 200의 의미를 생각해 봅시다. 먼저 10, 100은 랜덤으로 추출될 숫자의 법위, 즉 10부터 100까지의 범위 안에서 무작위로 숫자를 추출한다는 의미입니다.
따라서 10부터 100 사이에 정수 200개가 랜덤하게 생성됩니다.
명령어가 의미하는 바는 같지만, 코드는 다르게 작성된 것을 확인할 수 있습니다. numpy 라이브러리를 사용하여 코드를 작성하면 for 반복문을 사용하지 않고도 많은 숫자 데이터를 생성할 수 있습니다.

**TIP** np.random.rand(n)는 0~1 사이에 있는 n개의 실수(float)를 만들고, randitn(a,b,n)는 a 이상, b 이하인 정수 n개를 만드는 함수 입니다.

### numpy array 생성하기

numpy 라이브러리에서는 ndarray라는 특별한 데이터 타입의 배열이 사용됩니다. numpy를 사용하려면 ndarray 타입 배열을 다루는 데 익숙해질 필요가 있습니다.
'N 차원 배열'이라는 의미를 지는 ndarray 타입 배열을 지금부터는 배열 또는 array라고 부르겠습니다.
리스트와 같은 연속된 데이터는 다음과 같이 numpy array로 변환할 수 있습니다.

    import numpy as np
    a = np.array([1,2,3,4])
    print(a)

    실행 결과: [1 2 3 4]

실행 결과를 살펴보면 양 끝에 []가 붙는 점이 리스트와 비슷합니다. 하지만 numpy array는 리스트 내 요소를 구분하는 쉼표(,)가 없다는 차이점이 있습니다.
numpy array는 생긴 모습도 리스트와 비슷하지만, 리스트의 특징인 인덱싱과 슬라이싱을 할 수 있다는 점도 비슷합니다.

    import numpy as np
    a = np.array([1,2,3,4])
    print(a[1], a[-1])
    print(a[1:])

    실행 결과:   2 4
                [2 3 4]

ndarray의 특정 인덱스에 해당하는 값을 출력하거나 슬라이싱 결과를 출력하는 것이 잘 이루어짐을 확인할 수 있습니다.
그러나 정수, 문자열, 리스트 등 다양한 데이터 타입을 담을 수 있었던 리스트와는 달리 numpy array에는 한 가지 타입의 데이터만을 저장할 수 있습니다. 예를 들어,
숫자와 문자가 함께 저장되었다면 문자로 변환되어 저장되는 것이지요.
다음과 같이 3개의 정수와 1개의 문자가 저장된 리스트를 배열로 변환하면 모두 같은 문자 타입으로 변환됩니다.

    import numpy as np
    a = np.array([1,2,'3',4])
    print(a)

    실행 결과: ['1' '2' '3' '4']

배열을 생성하기 위해 꼭 리스트가 있어야하는 것은 아닙니다. zeros(), ones(), eye() 같은 다양한 함수를 사용해서 배열을 초기화할 수도 있습니다.

    import numpy as np
    a = np.zeros(10) # 0으로 이루어진 크기가 10인 배열 생성
    print(a)

    실행 결과: [0. 0. 0. 0. 0. 0. 0. 0. 0. 0.]


    import numpy as np
    a = np.ones(10)  # 1로 이루어진 크기가 10인 배열 생성
    print(a)

    실행 결과: [1. 1. 1. 1. 1. 1. 1. 1. 1. 1.]


    import numpy as np
    a = np.eye(3)  # 3행 x 3열의 단위 배열 생성
    print(a)

    실행 결과:   [[1. 0. 0.]
                [0. 1. 0.]
                [0. 0. 1.]]

앞서 