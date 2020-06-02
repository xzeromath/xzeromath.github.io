---
# layout: "post"
title: "Jupyter_settings"
date: "2017-08-30 08:16"
categories:
# - Python
tags:
- Python
header:
  teaser: /assets/images/6.png
---

### Jupyter notebook만 원하는 브라우저로 열기

1. cmd 창
```
jupyter notebook --generate-config
```
  - 위의 명령을 하면 다음과 같이 jupyter_notebook_config.py 가 생성된다.
  - ~/.jupyter/jupyter_notebook_config.py

2. 이제 위의 파일을 열어서 열려고 하는 브라우저가 있는 경로를 아래와 같이 삽입하면 된다.
- (기본)
  ```
  # c.NotebookApp.browser = ''
  ```
- (수정후)
 ```
 c.NotebookApp.browser = '/usr/bin/google-chrome'
 ```
