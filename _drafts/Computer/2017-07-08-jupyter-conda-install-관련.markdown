---
layout: "post"
title: "jupyter conda install 관련"
date: "2017-07-08 09:50"
# categories: Computer
tag: 
- Jupyter
slug: conda
header:
  teaser: /assets/images/14.png
---
### 문제상황
- 학교 컴에서
현재 python3 와 주피터를 같이 쓰고 있는 상황
- 주피터에 패키지를 인스톨하기 위해 pip3를 사용하면 주피터가 아닌 python3에 패키지가 install 되는 경우가 많다.
  - [conda관련](http://egloos.zum.com/mcchae/v/11267105) : 이를 참조함

 ---

### 해결방안
- (windows경우) which conda 를 통해 위치를 파악해보려함.
하지만 환경변수에 등록되지 않아 conda명령어를 찾지 못함.
- 이를 해결하기 위해 컴의 내용을 검색해본 결과
C:\ProgramData\Anaconda3\exec\conda.bat
에 있음을 알수 있었음.
- 위치를 변경하고 conda를 실행하면 됨.
- conda install을 통해 패키지 인스톨.
- conda list를 통해 설치해 패키지를 확인하면 설치된 것을 알 수 있음.!
