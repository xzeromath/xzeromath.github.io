---
layout: "post" # single_math, single_jupyter
title: "jupyter를 md로 변환 자동화"
date: "2018-06-27 16:44"
categories:
  #Computer,Python,Math,Django,Excel,AWS, Crawl
tag: "Python"
  #Computer,Python,Math,Django,Excel,AWS, Crawl, Etc

slug: jupyter_to_md_auto
header:
  teaser: /assets/images/program1.png
---
## 자동화 필요성
- jupyter notebook을 jekyll로 올리기 위해 변환하는 과정
- 적당한 템플릿을 이용해 마크다운으로 변환함
- 이후 Front Matter를 적당하게 작성함
- 파일명을 규칙에 맞게 작성함
- 이 과정을 모두 자동화한 프로그램을 만들기로 함.


## PyQt5의 사용
- PyQt5를 이용하여 GUI프로그램 작성
- 코드는 아래와 같음.

``` python
import os
import sys
from PyQt5.QtWidgets import (QApplication, QWidget, QInputDialog,
QLineEdit, QFileDialog, QMainWindow, QPushButton, QCalendarWidget)

from PyQt5.QtCore import QDate
from PyQt5 import uic #ui 연결

form_class = uic.loadUiType("app_layout.ui")[0] # ui 연결


class MyWindow(QMainWindow, form_class):

    def __init__(self):
        super().__init__()
        # self.setupUI() #직접 레이아웃작성용
        self.setupUi(self)
        self.initAction()

    def initAction(self):
        self.radioButton.clicked.connect(self.radioButton_click)
        self.radioButton_2.clicked.connect(self.radioButton_click)
        self.radioButton_3.clicked.connect(self.radioButton_click)
        self.radioButton_4.clicked.connect(self.radioButton_click)
        self.radioButton_5.clicked.connect(self.radioButton_click)
        self.radioButton_6.clicked.connect(self.radioButton_click)
        self.radioButton_7.clicked.connect(self.radioButton_click)
        self.radioButton_8.clicked.connect(self.radioButton_click)
        self.radioButton_9.clicked.connect(self.radioButton_click)
        self.radioButton_10.clicked.connect(self.radioButton_click)
        self.ju_to_md.clicked.connect(self.btn1_clicked)
        self.insert_front.clicked.connect(self.btn2_clicked)
        self.spinBox.valueChanged.connect(self.spinBoxChanged)
        self.calendarWidget.clicked[QDate].connect(self.showDate)
        self.lineEdit.textChanged.connect(self.titleinput)
        self.lineEdit_3.textChanged.connect(self.sluginput)


    def radioButton_click(self):
        sender = self.sender() #버튼 눌렀을 때 받아오는 값
        self.radio_text= sender.text()
        print(self.radio_text)

    def spinBoxChanged(self):
        self.spin_value =self.spinBox.value() #Spin박스에서 받아오는 값
        print(self.spin_value)

    def showDate(self):
        # print(type(self.calendarWidget.selectedDate().toString("yyyy-MM-dd")))
        # print(self.calendarWidget.selectedDate().toString("yyyy-MM-dd"))
        self.setDay = self.calendarWidget.selectedDate().toString("yyyy-MM-dd")

    def titleinput(self):
        sender_text = self.sender()
        self.titletext = sender_text.text()

    def sluginput(self):
        sender_text = self.sender()
        self.slugtext = sender_text.text()

    def btn1_clicked(self):
        self.fname = QFileDialog.getOpenFileName(self,"변환할.ipynb선택")
        self.tname = QFileDialog.getOpenFileName(self,"템플릿파일 선택")
        self.savepath = os.path.dirname(self.fname[0]) # 변환할 파일 디렉토리이름
        print('savepath', self.savepath)
        self.filebasename = os.path.basename(self.fname[0]) # 변환할 파일이름
        print('filebasename', self.filebasename)
        self.filebasename_withoutext = os.path.splitext(self.filebasename)[0] # 확장자 제외 파일이름
        print('filebasename_withoutext',self.filebasename_withoutext)
        os.system(r'jupyter nbconvert --to markdown --template {} '.format(self.tname[0])+'"' +self.fname[0]+'"')
        # 여기까지가 md로 변환, 이후부터 front matter 작성

    def btn2_clicked(self):
        '''카테고리,티저번호를 받아서 삽입하기'''
        print("after self.fname",self.fname) #MyWindow.fname을 통해 클래스 변수 전달함.
        print("day",self.setDay)
        self.made_mdfilepath = os.path.splitext(self.fname[0])[0]+'.md' # 변환을 통해 만들어진 파일 위치
        self.newfilepath =  os.path.join(self.savepath , self.setDay + "-" + self.filebasename_withoutext +'.md') # 머릿말 추가 파일 위치
        with open(self.newfilepath,"w",encoding='utf-8') as g:
            g.write("""---
    title: {}
    tag: {}
    slug: {}
    header:
      teaser: /assets/images/{}.png
    ---
        """.format(self.titletext,self.radio_text,self.slugtext,self.spin_value))
            with open(self.made_mdfilepath,'r',encoding='utf-8') as f:
                lines = f.readlines()
                for line in lines:
                    g.write(line)
            print('quit'*19)

if __name__ == '__main__':
    app = QApplication(sys.argv)
    mywindow = MyWindow()
    mywindow.show()
    sys.exit(app.exec_())
```
***
## 프로그램 이미지
![자동화프로그램](/assets/images/program1.png)
