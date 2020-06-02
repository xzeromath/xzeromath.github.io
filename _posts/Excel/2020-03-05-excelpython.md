---
# layout: 'single_math'
#post
title: Python으로 특정폴더 내 파일이름 읽기 및 엑셀 내용 읽기 
date: 2020-03-05
categories: 업무자동화
tag: 
- Excel
- Python
#AWS,Computer,Crawl,Docker,Python,Math,Django,Javascript,Jupyter,Excel,Etc,Matplotlib
slug:  
---

## 요구사항
- 파이썬으로 특정폴더안의 파일 이름을 읽는다.
- 또한 특정 파일의 시트이름을 읽는다.
- 내용을 읽어와 pandas의 객체로 반환한다.

---

## 파일이름 얻기

현재 파일의 구조는 아래와 같다.

![](/assets/contents_images/2020-03-05-22-32-40.png)

파일의 이름을 얻어보자.

``` python
import os
from openpyxl import load_workbook
import pandas as pd

for (path, dir, files) in os.walk("/Users/xzero/excel_test/"):
    print("path:",path, "dir:", dir, "files:",files)

# path: /Users/xzero/excel_test/ dir: ['testdir'] files: ['test2.xlsx', '~$test1.xlsx', 'test1.xlsx']
# path: /Users/xzero/excel_test/testdir dir: [] files: ['test2.xlsx']
```


- 현재 폴더의 파일 이름 얻기

``` python
## 현재 폴더에서 파일 이름 리스트를 얻기
path = "/Users/xzero/excel_test/"
file_list = os.listdir(path)
print ("file_list: {}".format(file_list))
# file_list: ['test2.xlsx', 'testdir', 'test1.xlsx']

## 파일중 엑셀파일 리스트 얻기
exfile_list =[i for i in file_list if os.path.splitext(i)[-1]==".xlsx"]
print("excel:", exfile_list)
# excel: ['test2.xlsx', 'test1.xlsx']

## 엑셀 시트 이름 얻기
wb = load_workbook(filename = "/Users/xzero/excel_test/test1.xlsx")
print (wb.sheetnames)
# ['1번', 'two']

## 엑셀 내용을 pandas 데이터프레임으로 얻기
customer_data_file = "/Users/xzero/excel_test/test1.xlsx"
customers = pd.read_excel(
    customer_data_file,
    sheet_name="two",
    header=1, # 몇 번째행을 header로 할지? 첫째행=0
    usecols="A:B", #사용할 열
)
print(customers.head(5))

#    순번 제목
# 0   1  a
# 1   2  b
# 2   3  c
# 3   4  a
# 4   5  a

```


