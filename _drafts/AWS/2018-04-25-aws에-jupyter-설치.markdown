---
#layout: "post"
title: "aws에 jupyter 설치"
date: "2018-04-25 21:52"
# categories: "Python"
  #Computer,Python,Math,Django,Javascript,Jupyter Notebook,Excel,TW
tag: "AWS"
slug: "aws_jupyter"
header:
  teaser: /assets/images/2.png
---

- 참고 [link](https://chrisalbon.com/software_engineering/cloud_computing/run_project_jupyter_on_amazon_ec2/)
- ssh와 custom TCP 만 보안그룹 규칙으로 추가함.
- https://[주소]:8888 로 접속하면 끝


## sage 설치
- ssh로 해당 리눅스 접속
- sage에서 파일 다운로드
- wget (sage 파일주소)
- 다운로드 위치에서 tar xvjf FILENAME.tar.bz2 으로 설치
- jupyter kernelspec install --user ./SageMath/local/share/jupyter/kernels/sagemath
로 커널 설치
- 처음에 python 오류가남 -> python 명령에 반응할수 있도록 파이썬 설치함.
- sage서버가 켰다가 자꾸 꺼짐 -> 오류메세지에 sage root에서 실행시키라고 함.
- SageMath 폴더에서 jupyter notebook을 실행하니까 됨.
- 하지만 다른 폴더에서는 실행하면 잠깐 실행되었다가 꺼짐 = SAGE_ROOT를 설정하라는 메시지뜸.
- SAGE_ROOT=/home/hvofak5s/SageMath/ jupyter notebook 와 같이 앞에 명령을 주고 실행시켜보니 됨.
- cd 명령어로 원하는 폴더로 이동후 위의 명령을 치니 잘 실행됨.
- 로컬 맥에서 /Applications/SageMath/sage -n jupyter 로 sage 주피터 실행가능
