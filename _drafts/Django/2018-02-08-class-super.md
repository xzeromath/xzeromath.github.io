---
# layout: "post"
title: "class에서 super용법"
date: "2018-02-08 22:02"
# categories: "Python"
  #Computer,Python,Math,Django,Javascript,Jupyter Notebook,Excel,TW
tag: "Python"
slug: "class_super"
header:
  teaser: /assets/images/14.png

---

``` python
class Animal():
  def __init__(self,name):
    self.name= name


class Person2(Animal):
  def __init__(self,name,key):
    super.__init__('nck')
    self.key=key

p4=Person2('myname','mykey')
p4.name #'nck'
p4.key #'mykey'


class Person3(Animal):
  def __init__(self,*args,**kwargs):
    super.init__(*args,**kwargs)
    #super(Person3,self).init__(*args,**kwargs) #위와 같은 명령
    self.name=kwargs['name']+"**"
    # self.key=key # error key라는

p12=Person3(name='lee')
p12.name # lee**
```
즉, 부모에 사용되는 변수를 잘모르지만, 하나의 변수를 알고 있을 때, 이 변수의 값을 수정할 때 유용한 것 같음.
