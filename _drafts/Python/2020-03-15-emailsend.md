---
# layout: 'single_math'
#post
title: Python으로 이메일(Gmail) 보내기
date: 2020-03-15
categories: 업무자동화
tag: Python
#AWS,Computer,Crawl,Docker,Python,Math,Django,Javascript,Jupyter,Excel,Etc,Matplotlib
slug:  
---
## 요구사항
- python을 이용하여 email을 보내는 방법을 알아보고자 한다.


## 첫번째 방법 - 기본 모듈 사용
[https://oceancoding.blogspot.com/2019/11/smtp.html](https://oceancoding.blogspot.com/2019/11/smtp.html)

```python
import smtplib
from email.mime.text import MIMEText
 
 # 세션 생성
s = smtplib.SMTP('smtp.gmail.com', 587)
 
# TLS 보안 시작
s.starttls()
 
# 로그인 인증
s.login('sender@gmail.com', '앱비번 16자리')
 
# 보낼 메시지 설정
msg = MIMEText('내용 : 한글 내용')
msg['Subject'] = '제목 : 제목입니다.'
 
# 메일 보내기
s.sendmail('sender@gmail.com', 'receiver@gmail.com', msg.as_string())  # 송신자, 수진자, 
 
# 세션 종료
s.quit()

```
- gmail을 2차인증으로 사용하는 경우 로그인이 안됨.
- 이때 2차인증에서 앱비번을 설정할 수 있음.
- 위의 로그인 시 비번은 메일비번이 아니라 2차 인증에서 설정한 앱비번 16자리임.

## 두번째 방법- yagmail 사용
[https://github.com/kootenpv/yagmail](https://github.com/kootenpv/yagmail)


```python
import yagmail
yag = yagmail.SMTP( user="sender@gmail.com", password="앱비번", host='smtp.gmail.com')

to = 'receiver@gmail.com'
subject = 'This is obviously the subject'
body = 'This is obviously the body'
html = '<a href="https://pypi.python.org/pypi/sky/">Click me!</a>'
img = 'djangoimg.png'

yag.send(to = to, subject = subject, contents = [body, html, img])

```
- 마찬가지로 앱비번사용
- html과 파일을 따로 넣을 수 있음.
- 구체적인 사용법은 위의 사이트 참조하면 됨.



