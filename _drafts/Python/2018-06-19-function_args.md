---
# layout: post
title: 함수 인자
categories:
# - Python
tags:
- Python
header:
  teaser: /assets/images/12.png
---

  <div class="input_area" markdown="1">
  
```python
def myf(**args):
    args['myname']='nck'
    for i in args:
        print(i)
    print(type(args))
    print(args)
```

  </div>
  

  <div class="input_area" markdown="1">
  
```python
myf(a=1,b=3)
```

  </div>
  
  {:.output_stream}
  ```
  a
b
myname
<class 'dict'>
{'a': 1, 'b': 3, 'myname': 'nck'}

  ```
  
args가 사전으로 역할을 함, 이 사전에 추가등을 할 수 있음


  <div class="input_area" markdown="1">
  
```python
test={'c':1,'d':6}
```

  </div>
  

  <div class="input_area" markdown="1">
  
```python
myf(test)
```

  </div>
  

  {:.output_traceback_line}
  ```
  ---------------------------------------------------------------------------
  ```
  
  {:.output_traceback_line}
  ```
  TypeError                                 Traceback (most recent call last)
  ```
  
  {:.output_traceback_line}
  ```
  <ipython-input-8-2e9661a3b0f2> in <module>()
----> 1 myf(test)

  ```
  
  {:.output_traceback_line}
  ```
  TypeError: myf() takes 0 positional arguments but 1 was given
  ```
  


  <div class="input_area" markdown="1">
  
```python
myf(**test)
```

  </div>
  
  {:.output_stream}
  ```
  c
d
myname
<class 'dict'>

  ```
  
test를 언팩킹하여 넣어줘야함


  <div class="input_area" markdown="1">
  
```python
a,b=1,2
```

  </div>
  

  <div class="input_area" markdown="1">
  
```python
a
```

  </div>
  



  {:.output_data_text}
  ```
  1
  ```
  



  <div class="input_area" markdown="1">
  
```python
b
```

  </div>
  



  {:.output_data_text}
  ```
  2
  ```
  



  <div class="input_area" markdown="1">
  
```python
c=1,4
```

  </div>
  

  <div class="input_area" markdown="1">
  
```python
c
```

  </div>
  



  {:.output_data_text}
  ```
  (1, 4)
  ```
  



  <div class="input_area" markdown="1">
  
```python
def packing(a,b):
    return a,b
```

  </div>
  

  <div class="input_area" markdown="1">
  
```python
packing(5,6)
```

  </div>
  



  {:.output_data_text}
  ```
  (5, 6)
  ```
  



  <div class="input_area" markdown="1">
  
```python
1,2
```

  </div>
  



  {:.output_data_text}
  ```
  (1, 2)
  ```
  


packing이 됨.


  <div class="input_area" markdown="1">
  
```python
dic1={'a':1,'b':2}
```

  </div>
  

  <div class="input_area" markdown="1">
  
```python
dic2={'c':3,'d':4}
```

  </div>
  

  <div class="input_area" markdown="1">
  
```python
dic1+dic2
```

  </div>
  

  {:.output_traceback_line}
  ```
  ---------------------------------------------------------------------------
  ```
  
  {:.output_traceback_line}
  ```
  TypeError                                 Traceback (most recent call last)
  ```
  
  {:.output_traceback_line}
  ```
  <ipython-input-5-a503c9b1cf15> in <module>()
----> 1 dic1+dic2

  ```
  
  {:.output_traceback_line}
  ```
  TypeError: unsupported operand type(s) for +: 'dict' and 'dict'
  ```
  


  <div class="input_area" markdown="1">
  
```python
dict()
```

  </div>
  



  {:.output_data_text}
  ```
  {}
  ```
  



  <div class="input_area" markdown="1">
  
```python
dict(**dic1)
```

  </div>
  



  {:.output_data_text}
  ```
  {'a': 1, 'b': 2}
  ```
  



  <div class="input_area" markdown="1">
  
```python
dict(**dic1,**dic2)
```

  </div>
  



  {:.output_data_text}
  ```
  {'a': 1, 'b': 2, 'c': 3, 'd': 4}
  ```
  

