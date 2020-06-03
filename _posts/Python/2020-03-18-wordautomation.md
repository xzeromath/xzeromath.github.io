---
# layout: 'single_math'
#post
title: Python으로 MsWord 작성하기
date: 2020-03-18
categories: 업무자동화
tag: Python
#AWS,Computer,Crawl,Docker,Python,Math,Django,Javascript,Jupyter,Excel,Etc,Matplotlib
slug:  
---

## 요구사항
- 학교 공지사항을 크롤링하여 얻은 데이터가 존재함.
- 이 데이터를 Msword 로 저장하려 함.

## 과정
- 처음에 HWP자동화에 대한 유튜브 자료가 있어서 살펴봄.
- [회사원코딩](https://www.youtube.com/playlist?list=PLalzN02jITUtke62DP2PHZ6mkDid72IC_)
- 그런데 한글의 경우 python에 대응하는 api가 잘 나와있지 않아서 어려움이 있음.
- 그래서 라이브러리가 좀더 활성화된  Msword를 사용해서 작성해보기로 함.

## 참고
- 우선 라이브러리는 다음을 참고함.
- [python-docx](https://python-docx.readthedocs.io/en/latest/) 
- [참고1](https://nittaku.tistory.com/253)
- [참고2](https://m.blog.naver.com/PostView.nhn?blogId=12heejin&logNo=221397002037&proxyReferer=https%3A%2F%2Fwww.google.com%2F)

## 코드
```python
import pickle
from docx import Document
from docx.shared import Inches

with open("notice.pickle", "rb") as f:
    data = pickle.load(f)
data_short = data[:]

document = Document("form.docx")

paragraph = document.add_paragraph('Lorem ipsum dolor sit amet.')
prior_paragraph = paragraph.insert_paragraph_before('insert')
paragraph = document.add_paragraph('@@.')
table = document.add_table(rows=1, cols=3)
hdr_cells = table.rows[0].cells
hdr_cells[0].text = '번호2'
hdr_cells[1].text = '주소'
hdr_cells[2].text = '제목'
for i in data_short:
    print(i)
    row_cells = table.add_row().cells
    row_cells[0].width = Inches(1)
    row_cells[0].text = i['번호']
    # print("0",row_cells[0].width)


    row_cells[1].width = Inches(4)
    row_cells[1].text = i['주소']
    # print("1",row_cells[1].width)

    row_cells[2].width = Inches(3)
    row_cells[2].text = i['제목']

    # print("2",row_cells[2].width)

table.style="my"

document.save('demo65.docx')

```

## 설명
- table의 스타일이 잘 안됨. 기존의 것의 이름 적용이 잘 안되며, 새로운 스타일로 정의해서 사용하는 것은 잘 됨.
- table의 칸 크기 조절도 잘 안되는 경우가 있음. 분명 크기를 주었는데 자동으로 맞추는 것인지, 생각만큼 정교하게 조정이 되질 않음.
- 적당한 수준에서 꾸미는 게 좋을 것 같음.
- 위의 예시처럼 테이블로만 구성된 경우 엑셀로 만드는 것이 나을 듯 함.

## 결과물

![](/assets/contents_images/2020-03-18-10-21-05.png)

- 위의 주소는 홈페이지내에서 실행하는 자바스크립트 함수로 해당 내용의 자세한 페이지로 이동하도록 해줌.
- 위의 주소를 이용하여 세부 내역을 다시 정리해 볼 생각임.