---
# layout: "post"
title: "python의 소소한 팁"
date: "2018-08-24"
# categories: Python
  #Computer,Python,Math,Django,Javascript,Jupyter Notebook,Excel,TW
tag: "Python"
slug: "python_tip"
header:
  teaser: /assets/images/7.png
---
> 참고: https://hackernoon.com/python-tricks-101-2836251922e0
---

1. 변수 값 서로 바꾸기
``` python
a, b = 5, 10
print(a,b) # 5 10
a, b = b, a
print(a,b) # 10 5
```
 이를 이용하여 피보나치수열 1,1,2,3,5,8... 을 만드는 함수를 구성
 ``` python
 def fibo(n):
    a, b = 1, 1
    for i in range(n):
        a, b = b, a+b 
    return a
``` 
2. 리스트의 원소로 문자열 만들기
``` python
a = ["python","is","awesome"]
print(" ".join(a)) #python is awesome
```
3. 리스트에서 가장 자주 나오는 문자 찾기
``` python
a = [1,2,2,3,3,3,3,4,4,5]
a.count(1) #1 개수 출력
print(max(set(a), key =a.count))
# 다른 방법
from collections import Counter
cnt = Counter(a) #Counter({3: 5, 1: 2, 2: 2, 4: 1})
cnt.most_common(3) #[(3, 5), (1, 2), (2, 2)]
```
4. 구성이 같은 것 찾기
예) aabc == abac # 참
   [1,1,2,3] ==[1,2,3,1] # 참
``` python
from collections import Counter
Counter(str1) = Counter(str2)
```
5. 글자 뒤집기
``` python
a = "abcdefg"
print(a[::-1])
```
6. zip함수 이용하여 다시 묶기
``` python
list(zip([1, 2, 3], [4, 5, 6]))
# [(1, 4), (2, 5), (3, 6)]
original = [['a','b'],['c','d'],['e','f']]
transposed = zip(*orginal)
print(list(transposed))
# [('a', 'c', 'e'), ('b', 'd', 'f')]
```
7. 비교 연산자
``` python
b = 6 
print(4<b<7)
#True
print(1==b<20)
#False
```
8. 리스트 
``` python
a=[1,2,3,4,5]
b = a #주소로 연결
b[0] =10
print(a,b) #[1,2,3,4,5] [1,2,3,4,5]
c = a[:] #새로운 객체생성
c[0] = 20
print(a,c) #[10, 2, 3, 4, 5] [20, 2, 3, 4, 5]
d= a.copy() #새로운 객체 생성
d[0]=30
print(a,d) #[10, 2, 3, 4, 5] [30, 2, 3, 4, 5]
from copy import deepcopy
e =deepcopy(a)
```
9. 사전에서 값 얻기
``` python
d = {'a':1,'b':2}
d.get('a','default') # 1
d.get('c','default') # default
```











