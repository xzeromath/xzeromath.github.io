---
    title: binary 와 text
    tag: Python
    slug: binary_text
    header:
      teaser: /assets/images/12.png
---

## pickle 사용


  <div class="input_area" markdown="1">

```python
import pickle

bfilename = './test.bin'
tfilename = './test.txt'

data1 = 77
data2 = "hello world"
data3 =['car','apple','house']
```

  </div>

## binary와 텍스트 쓰기


  <div class="input_area" markdown="1">

```python
with open(bfilename, 'wb') as f:
    pickle.dump(data1,f) #dumps (문자열 직렬화)
    pickle.dump(data2,f)
    pickle.dump(data3,f)

with open(tfilename,'wt') as f:
    f.write(str(data1))
    f.write('\n')
    f.write(data2)
    f.write('\n')
    f.writelines('\n'.join(data3)) #리스트는 write로 안써짐
```

  </div>

## binary 읽기


  <div class="input_area" markdown="1">

```python
with open(bfilename,'rb') as f:
    b = pickle.load(f) #loads (문자열 역직렬화)
    print(type(b), b)
    b= pickle.load(f)
    print(type(b), b)
    b= pickle.load(f)
    print(type(b), b)
```

  </div>

  {:.output_stream}
  ```
  <class 'int'> 77
<class 'str'> hello world
<class 'list'> ['car', 'apple', 'house']

  ```

## 텍스트 읽기


  <div class="input_area" markdown="1">

```python
with open(tfilename, 'rt') as f:
    for i, line in enumerate(f,1):
        print(type(line), 'text' +str(i) +'|',line,end='')
```

  </div>

  {:.output_stream}
  ```
  <class 'str'> text1| 77
<class 'str'> text2| hello world
<class 'str'> text3| car
<class 'str'> text4| apple
<class 'str'> text5| house
  ```

- binary는 자료형도 그대로 유지함
- 텍스트는 읽어오면 그대로 텍스트임
