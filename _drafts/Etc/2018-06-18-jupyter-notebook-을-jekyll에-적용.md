---
# layout: "single_jupyter" # single_math
title: "jupyter_notebook 을 jekyll에 적용"
date: "2018-06-18 00:34"
# categories: Etc
  #Computer,Python,Math,Django,Excel,AWS, Crawl
tag: Etc
  #Computer,Python,Math,Django,Excel,AWS, Crawl

slug: "jupyter_jekyll"
header:
  teaser: /assets/images/3.png
---

## jupyter notebook을 jekyll 에 적용
- 아래를 참고하여 mytemplate.tpl을 작성하여 적당한 위치에 둠
```
jupyter nbconvert --to markdown --template ./mytemplate.tpl abc.ipynb
```
- 위의 명령을 통해 abc.md 가 만들어짐
- 그런데 위의 명령으로는 in과 out에 적당한 클래스이름이 만들어짐

## custom css 적용
- 그래서 jupyter_notebook 만의 레이아웃(single_jupyter)을 만들고 이 안에 custom css를 넣음

``` css
<style>
/* jupyter notebook 나의 설정 시작 */
.input_area div.highlighter-rouge {
  background-color: #263238  !important;
}
.output_stream, .output_data_text, .output_traceback_line {
  margin-left: 2% !important;
  border: none !important;
  border-radius: 4px !important;
  background-color: #36434a38 !important;
  box-shadow: 5px 10px 8px #888888 !important;
  color: #344e4e !important;
}
</style>
```
- 그런데 생각해보니 위의 style 을 기본 레이아웃에 포함시켜 별도의 레이아웃을 만들지 않는 것이 좋을 것 같음.

>  [참고](https://predictablynoisy.com/jekyll-markdown-nbconvert){:target="_blank"}
