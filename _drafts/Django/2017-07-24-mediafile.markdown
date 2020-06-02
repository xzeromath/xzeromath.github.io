---
# layout: "post"
title: "Mediafile"
date: "2017-07-24 10:14"
# categories: Django
tags: Django
header:
  teaser: /assets/images/8.png

---
## local server에서 S3로 mediafile 연결
- settings/dev.py 에서 아래와 같은 설정을 추가하여 S3에 media파일을 넣을 수 있었다.
``` python
DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.postgresql_psycopg2',
            'NAME': 'dbname',
            'USER': 'username',
            'PASSWORD': 'pw',
            'HOST':'hostname',
            'PORT': '5432',
        },
    }
    INSTALLED_APPS += ['storages']
    AWS_S3_HOST = 's3.ap-northeast-2.amazonaws.com'
    STATICFILES_STORAGE = 'mysite.storages.StaticS3Boto3Storage'
    DEFAULT_FILE_STORAGE = 'mysite.storages.MediaS3Boto3Storage'

    AWS_ACCESS_KEY_ID = ''
    AWS_SECRET_ACCESS_KEY = ''
    AWS_STORAGE_BUCKET_NAME = ''
```
  - 위의 내용들은 실제로 aws 서버에 환경변수로 등록되어 있는 값들이다.


- image는 저장이 되었고 admin에서도 파일경로가 보이는데, 클릭하면 404오류가 뜨는 이유
  - 이는 static과 달리 media는 파일서빙을 지원하지 않기 때문이다. 개발환경에서 지원하기 위해서는 룰을 추가하여야 한다.

``` python
  # prject/ urls.py
  from django.conf import settings
  from django.conf.urls.static import static

  urlpatterns +=static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
  # debug가 false이면 자동으로 빈문자열 리턴한다.
```

- 혹은 form enctype이 지정되지 않아서임.
- 혹은 view에서 request.FILES가 지정되어 있는지 확인

## 템플릿에서 mediafile처리
- photo가 필드명이면 여기에는 저장주소가 담김
- 이때.photo.url은 Media_url의 저장경로를 prefix로 붙여줌
- 따라서 아래와 같이 하는 게 좋음
```
{% raw %}
{% if post.photo %}
<img src=" { {post.photo.url} } ">
{% endif %}
{% endraw %}
```
- .path는 media_root를 prefix로 붙여줌.(서버에서 직접작업할 경우 사용)
