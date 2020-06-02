---
title: "Sqlite3_사용예제(읽기)"
date: "2018-06-27 16:44"
categories:
  #Computer,Python,Math,Django,Excel,AWS, Crawl
tag: "Python"
  #Computer,Python,Math,Django,Excel,AWS, Crawl, Etc

slug: db_read
header:
  teaser: /assets/images/13.png
---
## DB read 예제

``` python
import sqlite3
# DB 생성
conn = sqlite3.connect('./databases/sqlite1.db')  #,isolation_level=None) #Auto commit[ conn.commit()  생략가능]

#커서 바인딩
c = conn.cursor()

#데이터 조회
c.execute("SELECT * FROM users")

# #1개 로우 선택
# print(c.fetchone())
#
# #지정로우 선택
# print(c.fetchmany(size=4))
#
# #전체로우 선택
# print(c.fetchall())
# print(c.fetchone()) # 순회가 끝나서 커서가 마지막으로 감. 출력되는 것이 없음.

#순회1
# rows = c.fetchall()
# for row in rows:
#     print('usage1 > ',row)

#순회2
# for row in c.fetchall():
#     print("usage2>" ,row)

#순회3
# for row in c.execute("SELECT * FROM users"):
#     print('usage3>', row)

#조건조회1
# param1 = (1,)
# c.execute("SELECT * FROM users WHERE id=?",param1)
# print(c.fetchall()) # type: list

#조건조회2
param2 = 1
c.execute("SELECT * FROM users WHERE id='%s'" % param2)
print(c.fetchall()) # type: list

#조건조회3
c.execute("SELECT * FROM users WHERE id=:id",{"id":1})
print(c.fetchall())

#조건조회4
param4 =(1,4)
c.execute("SELECT * FROM users WHERE id IN(?,?)", param4)
print(c.fetchall())

#조건조회5
c.execute("SELECT * FROM users WHERE id=:id1 OR id=:id2",{"id1":1,"id2":4})
print(c.fetchall())

#dump
with conn:
    #Dump 출력 백업용으로 좋음.
    with open('./data/test.dump','w') as f:
        for line in conn.iterdump():
            f.write('%s \n' % line)
        print("Dump write complete")

```
