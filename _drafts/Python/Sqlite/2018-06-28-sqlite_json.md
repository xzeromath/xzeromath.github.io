---
title: "Sqlite3_사용예제(Json 파일 저장)"
date: "2018-06-27 16:44"
categories:
  #Computer,Python,Math,Django,Excel,AWS, Crawl
tag: "Python"
  #Computer,Python,Math,Django,Excel,AWS, Crawl, Etc

slug: db_json
header:
  teaser: /assets/images/18.png
---
## DB 저장예제
- https://jsonplaceholder.typicode.com/posts 연습
- 이 json자료를 나의 db에 저장해보는 연습

## Code

``` python
##
import requests
import sqlite3

URL ="https://jsonplaceholder.typicode.com/posts"
response = requests.get(URL)
print(response.status_code)
# print(response.text)
# print('type of response:',type(response)) #<class 'requests.models.Response'>
# print('type',type(response.json())) #list
# print(type(response.json()[0])) #<class 'dict'>

myjson = response.json()

conn = sqlite3.connect('./databases/sqlite_json_ex.db')
c = conn.cursor()
c.execute("CREATE TABLE IF NOT EXISTS json_ex(id INTEGER PRIMARY KEY, userId text, title text, body text )")

myData =[]

for data_dict in myjson:
    t = (data_dict['id'], data_dict['userId'], data_dict['title'], data_dict['body'])
    myData.append(t)

c.executemany("INSERT INTO json_ex(id, userId,title,body) VALUES (?,?,?,?)",myData)

conn.commit()
```
