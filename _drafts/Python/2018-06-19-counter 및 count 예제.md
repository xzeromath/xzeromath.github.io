---
# layout: post
title: counter 및 count 예제
# type: post
# status: publish
categories:
# - Etc
tag:
- Etc
slug: "counter_count"
header:
  teaser: /assets/images/13.png
---

  <div class="input_area" markdown="1">
  
```python
import collections
```

  </div>
  

  <div class="input_area" markdown="1">
  
```python
myList=['a','b','c','a','b','d']
```

  </div>
  

  <div class="input_area" markdown="1">
  
```python
myCounter=collections.Counter(myList)
```

  </div>
  

  <div class="input_area" markdown="1">
  
```python
myCounter
```

  </div>
  



  {:.output_data_text}
  ```
  Counter({'a': 2, 'b': 2, 'c': 1, 'd': 1})
  ```
  



  <div class="input_area" markdown="1">
  
```python
print(myCounter['a'])
```

  </div>
  
  {:.output_stream}
  ```
  2

  ```
  

  <div class="input_area" markdown="1">
  
```python
yourList=['a','b','b','e']
```

  </div>
  

  <div class="input_area" markdown="1">
  
```python
ourList=myList+yourList
```

  </div>
  

  <div class="input_area" markdown="1">
  
```python
ourList
```

  </div>
  



  {:.output_data_text}
  ```
  ['a', 'b', 'c', 'a', 'b', 'd', 'a', 'b', 'b', 'e']
  ```
  



  <div class="input_area" markdown="1">
  
```python
type(ourList)
```

  </div>
  



  {:.output_data_text}
  ```
  list
  ```
  



  <div class="input_area" markdown="1">
  
```python
ourCounter=collections.Counter(ourList)
```

  </div>
  

  <div class="input_area" markdown="1">
  
```python
ourCounter
```

  </div>
  



  {:.output_data_text}
  ```
  Counter({'a': 3, 'b': 4, 'c': 1, 'd': 1, 'e': 1})
  ```
  



  <div class="input_area" markdown="1">
  
```python
ourCounter.most_common(2)
```

  </div>
  



  {:.output_data_text}
  ```
  [('b', 4), ('a', 3)]
  ```
  



  <div class="input_area" markdown="1">
  
```python
ourCounter.keys()
```

  </div>
  



  {:.output_data_text}
  ```
  dict_keys(['a', 'b', 'c', 'd', 'e'])
  ```
  



  <div class="input_area" markdown="1">
  
```python
ourCounter.items()
```

  </div>
  



  {:.output_data_text}
  ```
  dict_items([('a', 3), ('b', 4), ('c', 1), ('d', 1), ('e', 1)])
  ```
  



  <div class="input_area" markdown="1">
  
```python
import itertools
```

  </div>
  

  <div class="input_area" markdown="1">
  
```python
for i in itertools.count(1,1): # 1부터 시작하여 1씩 증가 하는 카운터
    print(i)
    if i>10 :
        break
```

  </div>
  
  {:.output_stream}
  ```
  1
2
3
4
5
6
7
8
9
10
11

  ```
  

  <div class="input_area" markdown="1">
  
```python
k=itertools.count(1)
```

  </div>
  

  <div class="input_area" markdown="1">
  
```python
print(k)
```

  </div>
  
  {:.output_stream}
  ```
  count(1)

  ```
  

  <div class="input_area" markdown="1">
  
```python
print(k)
```

  </div>
  
  {:.output_stream}
  ```
  count(1)

  ```
  

  <div class="input_area" markdown="1">
  
```python
k
```

  </div>
  



  {:.output_data_text}
  ```
  count(1)
  ```
  



  <div class="input_area" markdown="1">
  
```python
print(iter(k),iter(k))
```

  </div>
  
  {:.output_stream}
  ```
  count(1) count(1)

  ```
  

  <div class="input_area" markdown="1">
  
```python
iter(k)
```

  </div>
  



  {:.output_data_text}
  ```
  count(1)
  ```
  

