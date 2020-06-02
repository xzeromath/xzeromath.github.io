---
# layout: "post"
title: "BeautifulSoup 예제 1"
slug: BeauS1
# categories: Crawl
tag: Crawl
header:
  teaser: /assets/images/8.png
---


## urljoin 사용법


  <div class="input_area" markdown="1">

```python
from urllib.parse import urljoin
baseUrl = "http://test.com/html/a.html"
print( urljoin(baseUrl, "b.html") )
print( urljoin(baseUrl, "sub/c.html") )
print( urljoin(baseUrl, "../index.html") )
print( urljoin(baseUrl, "../img/hoge.png") )
print( urljoin(baseUrl, "../css/hoge.css") )
```

  </div>

  {:.output_stream}
  ```
  http://test.com/html/b.html
http://test.com/html/sub/c.html
http://test.com/index.html
http://test.com/img/hoge.png
http://test.com/css/hoge.css

  ```

## 태그선택자


  <div class="input_area" markdown="1">

```python
from bs4 import BeautifulSoup

html = """
<html><body>
  <ul>
    <li><a href="http://www.naver.com">naver</a></li>
    <li><a href="http://www.daum.net">daum</a></li>
    <li><a href="https://www.google.com">google</a></li>
    <li><a href="https://www.tistory.com">tistory</a></li>
  </ul>
</body></html>
"""

soup = BeautifulSoup(html, 'html.parser')
links = soup.find_all("a")
print(links)
```

  </div>

  {:.output_stream}
  ```
  [<a href="http://www.naver.com">naver</a>, <a href="http://www.daum.net">daum</a>, <a href="https://www.google.com">google</a>, <a href="https://www.tistory.com">tistory</a>]

  ```


  <div class="input_area" markdown="1">

```python
for a in links:
    print('a' ,type(a) ,a )
    href = a['href']  # 또는 A.attrs['href']
    print('href',href)
    print('txt',a.text,) #또는 a.string

```

  </div>

  {:.output_stream}
  ```
  a <class 'bs4.element.Tag'> <a href="http://www.naver.com">naver</a>
href http://www.naver.com
txt naver
a <class 'bs4.element.Tag'> <a href="http://www.daum.net">daum</a>
href http://www.daum.net
txt daum
a <class 'bs4.element.Tag'> <a href="https://www.google.com">google</a>
href https://www.google.com
txt google
a <class 'bs4.element.Tag'> <a href="https://www.tistory.com">tistory</a>
href https://www.tistory.com
txt tistory

  ```


  <div class="input_area" markdown="1">

```python
a = soup.find_all("a", string='daum') # a 태그 중 문자가 daum 인 것
a
```

  </div>




  {:.output_data_text}
  ```
  [<a href="http://www.daum.net">daum</a>]
  ```




  <div class="input_area" markdown="1">

```python
for i in a:
    print(i.text)
```

  </div>

  {:.output_stream}
  ```
  daum

  ```


  <div class="input_area" markdown="1">

```python
b= soup.find_all("a", limit=3) #limit=0 무제한
b
```

  </div>




  {:.output_data_text}
  ```
  [<a href="http://www.naver.com">naver</a>,
 <a href="http://www.daum.net">daum</a>,
 <a href="https://www.google.com">google</a>]
  ```




  <div class="input_area" markdown="1">

```python
c = soup.find_all(string=['naver']) #보통은 정규표현식으로 사용
c
```

  </div>




  {:.output_data_text}
  ```
  ['naver']
  ```



## css selector

### [css 설명서](https://www.w3schools.com/CSSref/css_selectors.asp)
### [css 연습소](https://www.w3schools.com/CSSref/trysel.asp)


  <div class="input_area" markdown="1">

```python
html = """
<html><body>
<div id="main">
  <h1>강의목록</h1>
  <ul class="lecs">
    <li>Java 초고수 되기</li>
    <li>파이썬 기초 프로그래밍</li>
    <li>파이썬 머신러닝 프로그래밍</li>
    <li>안드로이드 블루투스 프로그래밍</li>
  </ul>
</div>
</body></html>
"""

soup = BeautifulSoup(html, 'html.parser')
h1 = soup.select("div#main > h1")
print(h1)
```

  </div>

  {:.output_stream}
  ```
  [<h1>강의목록</h1>]

  ```


  <div class="input_area" markdown="1">

```python
print(h1[0].text)
```

  </div>

  {:.output_stream}
  ```
  강의목록

  ```


  <div class="input_area" markdown="1">

```python
h11= soup.select_one("div#main > h1")
print(h11.text)
```

  </div>

  {:.output_stream}
  ```
  강의목록

  ```


  <div class="input_area" markdown="1">

```python
list_li = soup.select("#main > ul.lecs > li")
for li in list_li:
    print(li.text)
```

  </div>

  {:.output_stream}
  ```
  Java 초고수 되기
파이썬 기초 프로그래밍
파이썬 머신러닝 프로그래밍
안드로이드 블루투스 프로그래밍

  ```
