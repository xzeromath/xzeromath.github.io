---
layout: "post"
title: "AWS Elastic Beanstalk SSH 접속"
date: "2018-01-06 22:01"
# categories: "Django"
  #Computer,Python,Math,Django,Javascript,Jupyter Notebook,Excel,TW
slug: "AWS_Elastic_Beanstalk_SSH"
tag: Django
header:
  teaser: /assets/images/16.png

---

## SSH 접속을 위한 삽질
- 우선 ec2에 ssh 접속이 가능하도록 해야 한다.
- 기존의 Elastic Beanstalk에 eb init -i 로 하면 새로운 설정이 가능하다.
- 그런데 위의 작업을 통해 ssh를 가능하도록 하면 복사된 ec2가 만들어지는 듯하다. 즉 수정이 아니라 새로운 환경이 만들어지는 듯
- 그리고 나니 원래 ec2의 배포가 원인을 모를 오류에 빠짐
- 처음의 환경을 복사한 후 로드하여 배포가 가능한 새로운 환경을 만들고 eb init -i 을 통해 이환경에 파일을 연결한 후 eb deploy를 통해 해결함.

## SSH 접속
- ssh -i  mykey.pem ec2-user@public dns 로 하니 접속가능함.
- 즉 아이디를 ec2-user로 설정해야 함.
- 그리고 나서 sudo find / -name urls.py 을 통해 파일의 위치를 검색해 봄
- /opt/python/bundle/6/app/ 에 내 파일들이 위치하고 있음을 알 수 있었음.
