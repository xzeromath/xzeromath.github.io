---
# layout: "post"
title: "user custom후 eb에 배포"
date: "2018-08-06 22:51"
# categories: Django
  #Computer,Python,Math,Django,Javascript,Jupyter Notebook,Excel,TW
tag: "AWS"
slug: "awsssh2"
header:
  teaser: /assets/images/1.png
---

## AWS EB에 배포 중 몇가지 문제 직면
- accounts의 마이그레이션 중 auth에 종속성을 가짐.
- 실제로 accounts의 마이그레이션 파일을 보면 아래 코드가 있음.
``` python
    dependencies = [
        ('auth', '0009_alter_user_last_name_max_length'),
    ]
```
- 시도 결과 먼저 auth가 migrate되고 난 뒤, accounts가 migrate 되야 함
- 보통 migrate는 알파벳순으로 위의 원칙이 지켜지지 않는 것 같음.
- 로컬에서는 되지만 이후 rds에서는 계속 <code>django.db.utils.ProgrammingError: column course_classdata.created_at does not exist</code>와 같은 오류가 뜸.

## 몇가지 팁
- 로컬에서 다 한뒤 <code>export DJANGO_SETTINGS_MODULE=sshsapp2.settings.aws_prod</code> 와 같은 명령으로 현재 켜진 zsh에 환경변수를 등록해 줌(DB까지 모두)
- 이후 <code>python manage.py makemigrations --settings=sshsapp2.settings.aws_prod</code> 와 같은 명령으로 로컬에서 DB, S3를 연결한 채로 테스트 가능함.
- 위의 테스트가 끝나면, EB에 실제 환경변수를 등록하여 배포하면 됨.
- <code>python manage.py showmigrations --settings=sshsapp2.settings.aws_prod</code> 을 통해 내역을 확인
- <code>python manage.py migrate auth --settings=sshsapp2.settings.aws_prod</code> 
- <code>python manage.py migrate --settings=sshsapp2.settings.aws_prod</code>  
- 위의 순서대로 auth 를 migrate하고 나머지를 함.
- eb에서는 makemigration은 의미가 없는 것 같고, migrate가 의미있는 것 같음
- craetesuperuser도 같은 방식으로 로컬에서 진행하면, RDS에 기록됨.(!!)
## 테이블 존재 오류 해결
- <code>django.db.utils.ProgrammingError: column course_classdata.created_at does not exist</code>와 같은 오류가 뜸.
- DB를 날리고 새로운 DB에서 진행하니 해결됨.

