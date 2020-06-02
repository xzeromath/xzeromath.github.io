---
# layout: "post"
title: "Static_files"
date: "2017-07-24 10:28"
# categories: Django
tag: Django
header:
  teaser: /assets/images/8.png

---

## BASE_DIR
  - 설정파일에 설정함.
  - 보통 최상위root, 즉, manage.py가 있는 폴더를 말함

- staic_url이 staic 인 경우
  - http://localhost:8000/staic/blog/style.css 와 같은 요청을 static파일 요청으로 구분한다.

- askdjango/static/style.css (http://localhost:8000/static/style.css)
  - filesystemfinder (즉, STATICFILES_DIRS에 적용된 것)
- blog/static/blog/style.css(http://localhost:8000/static/blogstyle.css)
  - 개별앱에 적용된 것
- 이때 리스트는 개별앱에 대한 static가 우선순위
  - 만약 blog/static/style.css 라 설정하였고, http://localhost:8000/static/style.css 라는 요청이 들어오면 askdjango/static/style.css는 로드되지 않고 개별앱인 blog/static/style.css만 로드됨
  - 따라서 앱이름/static/앱이름/style.css 규칙을 따를 필요가 있음.

## style.css 사용
{% raw %}
{% load static%}
<link rel="stylesheet" href="{%static "style.css"%}"/> 삽입
<--! html 주석, django에서는 처리하지만 client에서 처리안함 -->
{% endraw %}

- static에 관한 어떠한 urls.py, views.py 같은 설정이 없어도 위의 접근이 가능한 이유는 debug=True이기 때문임. 즉 상용서버에서는 별도의 설정이 필요함.
- 우리는 S3의 도움을 받아 서빙하는 것임.
- collectstatic 의 명령을 통해 settings.STATIC_ROOT로 이것들이 자동 복사되고, 이를 웹서버가 참고하는 것임.
  -  askdjango/static/style.css 은 settings.STATIC_ROOT/style.css로 복사
  - blog/static/blog/style.css 은 settings.STATIC_ROOT/blog/style.css로 복사

> AskDjango EP26
