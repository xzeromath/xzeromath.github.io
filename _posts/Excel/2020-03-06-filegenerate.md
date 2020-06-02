---
# layout: 'single_math'
#post
title: VBA로 엑셀파일에 특정한 문자열을 넣어서 새로 생성하기
date: 2020-03-06
categories: 업무자동화
tag: Excel
#AWS,Computer,Crawl,Docker,Python,Math,Django,Javascript,Jupyter,Excel,Etc,Matplotlib
slug:  
---

## 요구사항
- 파일이 있는 현재 위치에 원하는 파일명으로 파일을 생성함.
- 이때 파일안에 적당한 위치에 원하는 문자열을 넣어서 생성함.

---
## 코드
``` visualbasic

Sub FileGen(FileName As String, word As String)  'FileGen() 함수 시작

    '생성할 파일이 이미존재하는지 여부확인 시작
        If Len(Dir(ThisWorkbook.Path & "\" & FileName & ".xlsx")) Then
        ' 현 워크북 파일 디렉토리에 FileName 변수값의 엑셀파일이 있다면  True
        
        MsgBox "파일명이 존재합니다."  '메시지 띄움
        
        Exit Sub  'FileGen() 함수 종료
        
        End If
    '생성할 파일이 이미존재하는지 여부확인 끝

Workbooks.Add  '워크북 추가
ActiveWorkbook.Worksheets(1).Range("a1") = word # 원하는 문자열을 기록함

ActiveWorkbook.SaveAs Filename:=ThisWorkbook.Path & "\" & FileName & ".xlsx"
'추가된 워크북 파일 저장 / 저장장소 = 현 워크북 파일 디렉토리 / 저장명 = FileName 변수값

End Sub  'FileGen() 함수 종료


Sub main()

Call FileGen("testfile", "testword")

End Sub

```

- 위와 같이 main을 실행하면 testfile.xlsx 가 생성되고 그 안에 a1셀에 testword 라는 단어가 기록된채 저장됨.