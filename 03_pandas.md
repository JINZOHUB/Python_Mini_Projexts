conda activate 로 가상환경 실행 후 

pip install pandas, numpy, matplotlib

```
import numpy as np

# np.array 는 베열을 정의하는 명령어
a = np.array([[2,3],[5,2]])   #2차원 배열 만들기 

a
array([[2, 3],
       [5, 2]])

d = np.array([[1,2,3,4,5],[2,4,5,6,7],[5,7,8,9,9]]) #3차원 배열 만들기 

d
array([[1, 2, 3, 4, 5],
       [2, 4, 5, 6, 7],
       [5, 7, 8, 9, 9]])

d[1:,3:] # 1행 다음 3열 다음꺼만 출력 

array([[6, 7],
       [9, 9]])

```
## 배열의 크기 알아내기 : shape
```
3 X 5 배열은 (3,5) 이런식으로 표현 

d = np.array([2,3,4,5,6])   # 1X5 행렬 만듦

d
array([2, 3, 4, 5, 6])

d.shape
(5,)   # d는 한개 리스트에 각 다섯 개의 원소를 가지고 있습니다.

e = np.array([[1,2,3,4],[3,4,5,6]]) #2X4 배열

e
array([[1, 2, 3, 4],
       [3, 4, 5, 6]])

e.shape
(2, 4)      #e는 두개 리스트에 각 네개의 원소를 가지고 있다는 의미 

```


## 배열의 원소 유형 확인하기 : dtype 

int (32,64)
unit(32,64) #부호가 없는 정수
float(32,64) 
complex #복소수 
bool 
string 
object
unicode


```
d.dtype     #배열 d의 자료형을 확인합니다.
dtype('int32')  #정수로 이뤄졌다는 의미 

```


## 배열 유형 바꾸기 astype()

```
data = np.arange(1,5)

data.dtype
dtype('int32')

data.astype('float64') # 배열 원소를 모두 실수로 변환
array([1., 2., 3., 4.])

data.astype('int32') #다시 정수로 바꿀 수도 있음
array([1, 2, 3, 4])

```

## 넘파이 함수 알아보기 
```
0 으로 이뤄진 배열만들기 : np.zeros()

np.zeros((2,10)) #행이 2이고 열이 10이며 각 원소가 0인 배열을 만듭니다.
array([[0., 0., 0., 0., 0., 0., 0., 0., 0., 0.],
       [0., 0., 0., 0., 0., 0., 0., 0., 0., 0.]])

1 로 이워진 배열 만들기 : np.ones()

np.ones((2,10))
array([[1., 1., 1., 1., 1., 1., 1., 1., 1., 1.],
       [1., 1., 1., 1., 1., 1., 1., 1., 1., 1.]])

연속형 정수 생성하기 : np.arange()
np.arange() 함수는 특정 범위에 있는 원소를 자동으로 만듭니다. 

np.arange(2,10)     #2 이상 10미만의 원소로 이루어진 1차원 배열을 만듭니다.
array([2,3,4,5,6,7,8,9])

array
array([2, 3, 4, 5, 6, 7, 8, 9])

행과 열을 바꾸기 : np.transpose()

a = np.ones((2,3))  # 원소가 전부 1인 2X3 배열을 만듭니다.
a
array([[1., 1., 1.],
       [1., 1., 1.]])

b= np.transpose(a)  # a에 저장된 배열의 행과 열을 바꿔 b에 저장
array([[1., 1.],
       [1., 1.],
       [1., 1.]])


```

## 배열의 사칙연산  (행렬의 사칙연산이 아님)

```

arr1 = np.array([[2,3,4],[6,7,8]])
arr2 = np.array([[12,23,14],[36,47,58]])

배열의 덧셈 

arr1 + arr2
array([[14, 26, 18],
       [42, 54, 66]])


배열의 곱셈 

arr1 * arr2
array([[ 24,  69,  56],
       [216, 329, 464]])

배열의 나눗셈 
arr1 / arr2

array([[0.16666667, 0.13043478, 0.28571429],
       [0.16666667, 0.14893617, 0.13793103]])

```

## 크기가 서로 다른 배열끼리 더하기 
```
arr1 = np.array([[2,3,4],[6,7,8]])
arr2 = np.array([[12,23,14],[36,47,58]])
arr3 = np.array([100,200,300])

arr1.shape
(2, 3)

arr3.shape
(3,)

arr1+arr3
array([[102, 203, 304],
       [106, 207, 308]])

arr4 = np.array([1,2,3,4,5,6,7,8,9,10])
arr4.shape
(10,)

arr1+arr4

Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ValueError: operands could not be broadcast together with shapes (2,3) (10,)
# 행과 열의 크기가 모두 다 다른 배열은 더할 수 없네요.


arr5 = np.array([[9],[3]])
arr5.shape
(2, 1)

arr1
array([[2, 3, 4],
       [6, 7, 8]])

arr5
array([9
       3])
arr5+arr1
array([[11, 12, 13],
       [ 9, 10, 11]])

#(2,3) 크기를 가지는 arr1 과 더하니 브로드캐스팅이 됩니다.

```


# 파이썬 리스트와 배열의 차이점 
```
d = np.array([[1,2,3,4,5],[2,4,5,6,7],[5,7,8,9,9]]) # () 배열은 괄호로 묶임

d_list =[[1,2,3,4,5],[2,4,5,6,7],[5,7,8,9,9]] #배열이 아니고 리스트임


d_list[:2]=0 #두번째 원소까지 슬라이싱을해서 0을 넣으라고 하면 오류가 발생
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: can only assign an iterable

d[:2]=0 # 두번째 대괄호 리스트까지 0으로 넣으라는 말
array([[0, 0, 0, 0, 0],
       [0, 0, 0, 0, 0],
       [5, 7, 8, 9, 9]])

```

# 인덱싱과 슬라이싱 연습하기
```
arr4 = np.arange(10)
arr4
array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])

arr1
array([[2, 3, 4],
       [6, 7, 8]])

arr4[:5]
array([0, 1, 2, 3, 4])

arr4[-3:]
array([7, 8, 9])

arr1[1,2]
8

arr1[:,2] #모든 리스트의 세번째 원소를 슬라이싱 합니다.
array([4, 8])


```