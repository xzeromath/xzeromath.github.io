---
# layout: "post"
title: "Templates"
date: "2017-07-20 12:06"
# categories: Django
tag: Django
header:
  teaser: /assets/images/9.png

---

## 주피터 노트북 사용
python manage.py shell_plus --notebook

- 1:1 OneToOneField로 연결된, user와 profile관계에서 profile에 해당하는 user호출 예시
<script src="https://gist.github.com/nck2/ac7d813751f6869cb181271ef767c5da.js"></script>

## staticfile 사용

- 앱/static/앱/css/style.css 생성
- 템플릿 파일위에
`html
{% raw %}
{% load static %}
{% endraw %}
`추가
- 탬플릿 파일에 `<link rel="stylesheet" href="{ % static 'askdjango/css/style.css' %}" />` 같이 추가

개수를 카운트할때
Post.objects.all().count() 이다.
탬플릿에서는 괄호를 제거하고 Post.objects.all.count 이다.
마찬가지로 탬플릿단에서 쿼리셋전체는 Post.objects.all 이다.
부트스트랩의 css와 js 가 커스텀으로 로드되어 있으면 다음 명령은 생략해도 된다. (부딪혀서 의도치 않은 오류가 발생하기도 한다.)
{ % bootstrap_css %}
{ % bootstrap_javascript %}


- form에서 오류 메세지(부트스트랩은 자동으로 출력해주는듯)

1.
{ % for error in form.non_field_errors %}
  {{error}}
{ % endfor %}

2.
{ % for field in form.visible_fields %}
    { % for error in field.errors %}
      {{error}}
    { % endfor %}
{ % endfor %}
