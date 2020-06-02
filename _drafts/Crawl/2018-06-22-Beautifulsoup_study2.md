---
# layout: "post"
title: "BeautifulSoup 예제 2"
slug: BeauS2
# categories: Crawl
tag: Crawl
header:
  teaser: /assets/images/8.png
---

## beautifulsoup 문법


  <div class="input_area" markdown="1">

```python
from bs4 import BeautifulSoup
import re
```

  </div>


  <div class="input_area" markdown="1">

```python
html = """
<html><body>
  <ul>
    <li id="naver"><a href="http://www.naver.com">naver</a></li>
    <li><a href="http://www.daum.net">daum</a></li>
    <li><a href="https://www.google.com">google</a></li>
    <li><a href="https://www.tistory.com">tistory</a></li>
  </ul>
</body></html>
"""

soup = BeautifulSoup(html, 'html.parser')
test = soup.find('a',string='naver')
test
```

  </div>




  {:.output_data_text}
  ```
  <a href="http://www.naver.com">naver</a>
  ```




  <div class="input_area" markdown="1">

```python
test2 = soup.find(id='naver').string
test2
```

  </div>




  {:.output_data_text}
  ```
  'naver'
  ```



## 정규표현식


  <div class="input_area" markdown="1">

```python
li = soup.find_all(href=re.compile(r"^https://"))
print(li)
```

  </div>

  {:.output_stream}
  ```
  [<a href="https://www.google.com">google</a>, <a href="https://www.tistory.com">tistory</a>]

  ```


  <div class="input_area" markdown="1">

```python
for e in li:
    print(e['href'])
```

  </div>

  {:.output_stream}
  ```
  https://www.google.com
https://www.tistory.com

  ```

 - 잘사용하지는 않는 편임. css selector 사용

## css selector 연습


  <div class="input_area" markdown="1">

```python
fp = open('food-list.html',encoding="utf-8")
soup = BeautifulSoup(fp, "html.parser")
soup
```

  </div>




  {:.output_data_text}
  ```
  <html>
<body>
<div id="foods">
<h1>안주 및 주류</h1>
<ul id="fd-list">
<li class="food hot" data-lo="ko">닭도리탕</li>
<li class="food" data-lo="jp">돈까스</li>
<li class="food hot" data-lo="ko">삼겹살</li>
<li class="food" data-lo="us">스테이크</li>
</ul>
<ul id="ac-list">
<li class="alcohol" data-lo="ko">소주</li>
<li class="alcohol" data-lo="us">맥주</li>
<li class="alcohol" data-lo="ko">막걸리</li>
<li class="alcohol high" data-lo="cn">양주</li>
<li class="alcohol" data-lo="ko">동동주</li>
</ul>
</div>
<body>
</body></body></html>
  ```




  <div class="input_area" markdown="1">

```python
print(soup.select_one("li:nth-of-type(8)").string)
```

  </div>

  {:.output_stream}
  ```
  양주

  ```


  <div class="input_area" markdown="1">

```python
print(soup.select_one("#ac-list > li:nth-of-type(4)").string)
```

  </div>

  {:.output_stream}
  ```
  양주

  ```


  <div class="input_area" markdown="1">

```python
print(soup.select("#ac-list > li[data-lo='cn']")[0].string)
```

  </div>

  {:.output_stream}
  ```
  양주

  ```


  <div class="input_area" markdown="1">

```python
print(soup.select("#ac-list > li.alcohol.high")[0].string) # 두개의 클래스가 동시에 있을 때는 띄어쓰기가 아니라 .으로 연결
```

  </div>

  {:.output_stream}
  ```
  양주

  ```


  <div class="input_area" markdown="1">

```python
param = {"data-lo":"cn", "class":"alcohol"}
print(soup.find('li',param).string)
```

  </div>

  {:.output_stream}
  ```
  양주

  ```


  <div class="input_area" markdown="1">

```python
print(soup.find(id='ac-list').find("li",param).string)
```

  </div>

  {:.output_stream}
  ```
  양주

  ```


  <div class="input_area" markdown="1">

```python
for ac in soup.find_all("li"):
    if ac['data-lo'] == 'us':
        print('data-lo == us',ac.string)
```

  </div>

  {:.output_stream}
  ```
  data-lo == us 스테이크
data-lo == us 맥주

  ```


  <div class="input_area" markdown="1">

```python
fp.close()

cars_data="""
<ul id="cars">
  <li id="ge">Genesis</li>
  <li id="av">Avante</li>
  <li id="so">Sonata</li>
  <li id="gr">Grandeur</li>
  <li id="tu">Tucson</li>
</ul>
"""
```

  </div>


  <div class="input_area" markdown="1">

```python
fp = open('cars.html',encoding="utf-8")
soup = BeautifulSoup(fp, "html.parser")
soup
```

  </div>




  {:.output_data_text}
  ```
  <ul id="cars">
<li id="ge">Genesis</li>
<li id="av">Avante</li>
<li id="so">Sonata</li>
<li id="gr">Grandeur</li>
<li id="tu">Tucson</li>
</ul>
  ```




  <div class="input_area" markdown="1">

```python
def car_func(selector):
    print("car_func",soup.select_one(selector).string)

car_func("#gr")
```

  </div>

  {:.output_stream}
  ```
  car_func Grandeur

  ```


  <div class="input_area" markdown="1">

```python
car_func("li#gr")
```

  </div>

  {:.output_stream}
  ```
  car_func Grandeur

  ```


  <div class="input_area" markdown="1">

```python
car_func("ul > li#gr")
```

  </div>

  {:.output_stream}
  ```
  car_func Grandeur

  ```


  <div class="input_area" markdown="1">

```python
car_func("#cars #gr")
```

  </div>

  {:.output_stream}
  ```
  car_func Grandeur

  ```


  <div class="input_area" markdown="1">

```python
car_func("li[id='gr']")
```

  </div>

  {:.output_stream}
  ```
  car_func Grandeur

  ```


  <div class="input_area" markdown="1">

```python
print(soup.select("li")[3].string)
```

  </div>

  {:.output_stream}
  ```
  Grandeur

  ```


  <div class="input_area" markdown="1">

```python
print(soup.find_all("li")[3].string)
```

  </div>

  {:.output_stream}
  ```
  Grandeur

  ```

## 람다식을 이용


  <div class="input_area" markdown="1">

```python
car_lambda = lambda q : print("car_lambda",soup.select_one(q).string)
```

  </div>


  <div class="input_area" markdown="1">

```python
car_lambda("ul > li#gr")
```

  </div>

  {:.output_stream}
  ```
  car_lambda Grandeur

  ```
