---
# layout: "post"
title: "Docker를 이용하여 Azure에서 배포하기"
date: "2018-02-08 22:02"
# categories: "Django"
  #Computer,Python,Math,Django,Javascript,Jupyter Notebook,Excel,TW
tag: "Docker"
slug: "docker_deploy"
header:
  teaser: /assets/images/12.png

---

## Askdjango print 참고

1. Resource Group 생성
    -종량제로 선택함
2. Storage Accounts 생성
    - blob에서 static, media 생성
    - Storage account name과 Key 조사
    - 지역은 모두 japan east
3. Azure Database for PostgreSQL 생성
    - pricing tier 설정하기(basic- 43994.15 KRW)
4. DB_HOST : (server name)
5. DB_USER : (Server admin login name)
6. DB_NAME : (아래쪽에 이름이 있음)
    - DB메뉴얼 : https://docs.microsoft.com/en-us/azure/postgresql/quickstart-create-server-database-portal
7. 방화벽 설치: connection security
    - 일단 모든 곳에 다되도록
8. docker 세팅
9. docker build -t matxzerodjango . 로 도커 빌드
10. sh dev.sh 로 환경변수 설정하여 도커실행
11. python3 manage.py collectstatic --no-input
12. python3 manage.py showmigrations
13. python3 manage.py migrate
14. python3 manage.py createsuperuser
15. docker build -t matxzerodjango . 로 도커 빌드
16. sh dev2.sh 로 환경변수 설정
17. http://localhost:8888/ 로 확인
18. docker login
19. docker build --tag hvofak5s/(이름:버젼) .
20. docker push hvofak5s/(이름:버젼)
22. Web app for container 설치
    - app service plan 설정 조심 :s1  (80,000원?)
23. 도커 이미지 설정
24. 환경변수 지정(6개)후 재시작
25. always on 설정
26. https://docs.microsoft.com/ko-kr/azure/app-service/app-service-ip-addresses 에서 아웃바운드 찾아서 DB에 설정

### 돈이 너무 많이 드는 듯함.