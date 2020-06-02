---
# layout: "post"
title: "Model과 Model fields"
date: "2017-07-17 10:54"
# categories: Django
tags: Django
slug: model
header:
  teaser: /assets/images/11.png
---

## 파이썬 클래스와 데이터베이스 테이블의 매핑
- blog앱 Post모델 : blog_post 데이터베이스테이블
- blog앱 Comment모델: blog_comment 데이터베이스테이블
- model과 DB 테이블과 매핑
- model instance 는 DB 테이블의 하나의 row와 매핑

## 모델 클래스명
- 단수형으로 작성 (Post)

## 모델정의
- created_at = models.DateTimeField(auto_now_add=True)
  - 최초 저장일시가 자동 저장됨
- updated_at = models.DateTimeField(auto_now=True)
  - 업데이트된 일시가 자동 갱신됨

## Field Options
- null : DB필드에 NULL허용여부 (디폴트 : False) ,db 옵션
- unique , db옵션
- blank: 입력값 유효성 검사시에 empty 허용여부 (디폴트: False)
- default
- choices
  - 사용문법 {%highlight python%}
  choice=(
  ('제목1','제목1 레이블'),
  ('제목2','제목2 레이블')
  )
  {%endhighlight%}
  - 첫번째 인자는 저장될 값이고, 두번째 인자는 UI에 보여질 레이블
- validators
  - 사용문법 {%highlight python%}
  from django.forms import ValidationError

  def test_validator(value):
    if not re.match(..., value):
      raise ValidationError("여기가 오류메세지")

  Class Post(models.Model):
    test= models.CharField(max_length=50
      validators=[test_validator]),
        )
  {%endhighlight%}
- verbose_name
- help_text

> AskDjango 강의(https://nomade.kr)
