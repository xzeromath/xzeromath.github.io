---
title: "Python으로 구글 스프레드시트 작업하기"
date: "2018-09-28 00:11"
# categories: Python
  #Computer,Python,Math,Django,Excel,AWS, Crawl
categories: 업무자동화
tag: Python
  #Computer,Python,Math,Django,Excel,AWS, Crawl

slug: google_doc
header:
  teaser: /assets/images/7.png
---

## 구글 스프레드 시트 

### 필요 라이브러리
- gspread
- oauth2client

### 구글 스프레드 시트 설정
- https://console.developers.google.com/
- Google Sheets API (읽고 쓰는데 필요)
- Google Drive API (파일을 새로 만드는데 필요)
- 컨트롤하는 계정을 다운로드 받는다(로봇키)
- 이 계정에 있는 이메일 주소를 스프레드 시트에 공유하는 과정 필요
- 실제 이 이메일은 접속하는데만 사용

### 읽고 쓰는 예제
``` python
import gspread
from oauth2client.service_account import ServiceAccountCredentials

scope = ['https://spreadsheets.google.com/feeds']
credentials = ServiceAccountCredentials.from_json_keyfile_name('cred.json',scope)

gs = gspread.authorize(credentials)

doc = gs.open_by_url('url 주소기입')
ws = doc.get_worksheet(0) # 첫번째 시트
# val = ws.acell("B1").value
# print(val)

# val = ws.row_values('1')
# print(val)

# val = ws.col_values(1)
# print(val)

val = ws.range("A2:B3")
print(val)

# ws.update_acell('B1','mydata')
ws.append_row(['kk','kkkf','kfalgs'])# 가장 아래쪽 데이터 밑에 행을 만듦.
```

### 새로운 파일을 만들고 공유하는 예제
``` python
import gspread
from oauth2client.service_account import ServiceAccountCredentials

scope = [
    'https://www.googleapis.com/auth/drive',
    'https://spreadsheets.google.com/feeds'
    ]
credentials = ServiceAccountCredentials.from_json_keyfile_name('cred.json',scope)

gs = gspread.authorize(credentials)

doc = gs.create('온라인테스트2')

ws = doc.get_worksheet(0)

for i in range(5):
    ws.append_row([i,str(i)+'data'])

doc.share('공유할 gmail ',perm_type='user',role='owner')
```