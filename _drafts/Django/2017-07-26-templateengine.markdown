---
# layout: "post"
title: "TemplateEngine"
date: "2017-07-26 14:05"
# categories: Django
tag: Django
slug: Django template engine
header:
  teaser: /assets/images/9.png

---

## templage tag 관련
- 호출가능한 객체 cal에 대하여 {%raw%}{{ClassName.cal}}{%endraw%}  와 같이 불러낼 수 있다.
- tag와 filter는 모두 함수이다.
- tag는 {%raw%}{%%}{%endraw%}와 같이 사용
- 변수는{%raw%}{{ }}{%endraw%}를 사용
- 함수의 인자는 ()를 사용하지 않음.
- 인자사이에 ,를 넣지 않음.


## 주석관련
  - 템플릿 주석은 {%raw%}{% comment "notename,option"%} {% endcomment%}{%endraw%}
  - 자바스크립트 주석은  {%raw%}/% %/{%endraw%}
  - html주석은  {%raw%}< !--  --!>{%endraw%}
  - 자바스크립트와 html주석은 서버단에서는 랜더링!!

## 기타
  - [날짜 출력 포맷](https://docs.djangoproject.com/en/1.10/ref/templates/builtins/#std:templatefilter-date)
  - [custom 탬플릿 tag 만드는법](https://blueshw.github.io/2016/03/03/django-using-custom-templatetags/)

 - 장고에서 시간표시
   {%highlight python%}
        from django.utils import timezone
        timezone.now().strftime("%Y-%m-%d %H:%M:%S")
        # 2017-070-26 16:40:30
   {%endhighlight%}



> [AskDjango](https://nomade.kr) EP.16 Django Template Engine
