---
# layout: "post"
title: "synology ssh설정"
date: "2018-05-30 23:02"
# categories: "Computer"
  #Computer,Python,Math,Django,Javascript,Jupyter Notebook,Excel,TW
tag: "Computer"
slug: 'synology_ssh'
header:
  teaser: /assets/images/4.png

---
## DDNS 주소 설정
  > http://devks.tistory.com/19?category=686547
  위를 참고하여 DDNS 주소를 설정함. 이 주소로 접속가능함.

## SSH 활성화
  > http://ngee.tistory.com/625
  를 참고하여 SSH 활성화한다.
  - 포트를 설정한다.
  - 사용자 홈폴더 활성화
  - 처음 접속은 admin으로 가능함.
  - ssh -p 1111 admin@ddns주소
  (포트번호가 1111일 경우)
