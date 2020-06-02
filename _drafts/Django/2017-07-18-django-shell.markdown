---
# layout: "post"
title: "Django Shell"
date: "2017-07-18 13:01"
# categories: Django
tag: Django
header:
  teaser: /assets/images/5.png

---
## Jupyter notebook을 통한 shell 접근

- 가상환경에서 pip3 install jupyter 을 통해 가상환경안에 주피터노트북 설치가능 (pip 하면 실패했는데, pip3로 하니 되었음. 그냥 접속 운? 인것 같음.)
- 설치이후 python manage.py shell 을 하면 ipython이 실행됨.
- shell로 실행하면, sys.path가 그냥 python을 했을때와 달라짐. 기본폴더가 경로에 잡히는 것 같음.
- pip install django-extensions 을 통해 설치하고
- django_extensions앱을 등록 (위에는 중간줄, 여기는 밑줄에 유의)
- python manage.py shell_plus --notebook (가운데 줄- 두개)
으로 주피터를 실행시킬수 있음.
  - 이것은 기본적인 세팅이 로드가 되고, 필요한 것들이 자동으로 임포트가 된 환경임.
  - 결과를 확인해보기 위해 사용해보는 데 좋음.

> [AskDjango](https://nomade.kr) EP7. Django Shell
