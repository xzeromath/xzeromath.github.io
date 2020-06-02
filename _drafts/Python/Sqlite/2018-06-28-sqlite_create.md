---
title: "Sqlite3_사용예제(생성)"
date: "2018-06-27 16:44"
categories:
  #Computer,Python,Math,Django,Excel,AWS, Crawl
tag: "Python"
  #Computer,Python,Math,Django,Excel,AWS, Crawl, Etc

slug: db_create
header:
  teaser: /assets/images/12.png
---
## DB생성예제

``` python
import sqlite3
import simplejson as json
import datetime

# DB 생성
conn = sqlite3.connect('./databases/sqlite1.db')  #,isolation_level=None) #Auto commit[ conn.commit()  생략가능]

# DB 생성(메모리에)
# conn = sqlite3.connect(':memory:')

#날짜 생성
now = datetime.datetime.now()
print('now',now)

nowDatetime = now.strftime('%Y-%m-%d %H:%M:%S')
print('nowDatetime',nowDatetime)

#sqlite3 버젼확인
print('sqlite3.versin',sqlite3.version)
print('sqlite3_version', sqlite3.sqlite_version)

#Cursor 연결
c = conn.cursor()
print(type(c)) #<class 'sqlite3.Cursor'>

#테이블 생성(sqlite3 데이터 타입 : TEXT, NUMERIC, INTEGER, REAL, BLOB)
c.execute("CREATE TABLE IF NOT EXISTS users(id INTEGER PRIMARY KEY, username text, email text, phone text, website text, regdate text )") #AUTOINCREMENT

#데이터 삽입
# c.execute("INSERT INTO users VALUES(1,'kim','dim@naver.com','01-0000-0000','kim.co.kr',?)",(nowDatetime,))

userList = (
    (2,'kim','dim@naver.com','01-0000-0000','kim.co.kr',nowDatetime),
    (3,'kim','dim@naver.com','01-0000-0000','kim.co.kr',nowDatetime),
    (4,'kim','dim@naver.com','01-0000-0000','kim.co.kr',nowDatetime),
)
# c.executemany("INSERT INTO users(id, username, email, phone, website, regdate) VALUES (?,?,?,?,?,?)",userList)

with open('./data/users.json','r') as infile:
    r = json.load(infile)
    # print('r',r)
    userData = []
    for user in r:
        t =(user['id'],user['username'],user['email'],user['phone'],user['website'],nowDatetime)
        # print('t',t)
        userData.append(t)
    # print('userData',userData)
    # print('userData',tuple(userData))
    c.executemany("INSERT INTO users(id, username, email, phone, website, regdate) VALUES (?,?,?,?,?,?)",userData)

## DB삭제 (구조는 남겨놓음)
# print('users db delete',conn.execute("delete from users").rowcount, "rows")
conn.commit()
conn.close()
```
