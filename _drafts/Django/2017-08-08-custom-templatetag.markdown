---
# layout: "post"
title: "Custom_template_tag"
date: "2017-08-08 12:37"
# categories: Django
tag: Django
header:
  teaser: /assets/images/12.png

---

[링크](http://oniondev.egloos.com/9862474) (이 내용을 정리)

## 재사용가능한 템플릿 태그 작성
1. 다른 앱에 설치되어 있어도 사용가능하다.
2. templatetags라는 폴더를 앱아래에 만든다
3. 이 폴더안에 my_filters.py 라는 이름으로 아래 코드를 작성한다.
  {% highlight python %}
  from django import template
  register = template.Library()

  @register.filter
  def get_item(dictionary, key):
      return dictionary.get(key)
  {% endhighlight %}
4. blabla.html 이라는 template 파일의 context 로 아래와 같은 정보가 넘어갔다고 하자.
{% highlight python %}
# === BlaBlaView ===
context['name_dic'] = {'shoe01':'컨버스', 'shoe02':'구두', 'shoe03':'군화'}
context['shoe_code'] = 'shoe02'
{% endhighlight %}
이때 template 에서 shoe_code 를 우리가 보기좋은 정보로 치환하기 위해서는 Dictionary의 Key값으로 조회하여 Value를 빼올 수 있는!!
내가만든 필터를 적용해야만 한다. 자 그럼 아래 코드를 보자.
{% highlight python %}
# === blabla.html ===
{% raw %}
{% load get_item from my_filters %}
...
<td>신발명</td>
<td>{{ name_dic | get_item:shoe_code }}</td>
{% endraw %}
{% endhighlight %}
