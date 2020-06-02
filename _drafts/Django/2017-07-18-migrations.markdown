---
# layout: "post"
title: "Migrations"
date: "2017-07-18 12:00"
# categories: Django
tag: Django
header:
  teaser: /assets/images/7.png

---

## Migrations 명령어
1. python manage.py makemigrations [앱이름]
2. python manage.py migrate [앱이름]
3. python manage.py showmigrations [앱이름] : 어떤 마이그레이션이 적용되었는지 안되었는지 확인가능.
4. python manage.py sqlmigrate [앱이름] [migration-name]

## Tip
- 적용하지않은 마이그레이션은 삭제해도 무방
- 하지만 적용한 마이그레이션은 함부로 삭제하면 안됨!!
- no such table, no such column 오류는 거의 마이그레이션이 안되어 나타나는 오류임

## 마이그레이션의 포워드, 롤백
- case 1
  - blog/001
  - blog/002
  - blog/003
  - blog/004 --여기까지 적용

위의 상황에서 004를 취소시키려면
python manage.py migrate blog 003 을 하면
003까지 적용된 버젼으로 바뀐다. 이후 004를 삭제하면 된다.

<hr/>
- case 2
  - blog/001
  - blog/002  --여기까지 적용
  - blog/003
  - blog/004

위의 상황에서
python manage.py migrate blog 003 을 하면
003까지 적용된 버젼으로 바뀐다.

<hr/>
## 기타
- python manage.py migrate zero로 하면
모든 마이그레이션이 취소가 된다.
- 단 이처럼 롤백을 하면 데이터가 모두 삭제될 수 있으니 유의해야 함.

> [AskDjang](https://nomade.kr) EP6. Migrations
