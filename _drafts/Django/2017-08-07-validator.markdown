---
# layout: "post"
title: "Form-valid"
date: "2017-08-07 15:01"
# categories: Django
tag: Django
header:
  teaser: /assets/images/11.png

---
## form과 관련한 몇 가지 사실
1. 모델폼의 widget변경은 마이그레이션이 필요없다.
2. forms.py에서의 변경은 마이그레이션이 필요없다.
3. hidden input을 하면 폼에 포함되지만 화면에 나타나지 않는다.
4. is_valid()는 폼에서 지정한 필드에 대해서만 유효성검사를 하는 듯하다.


## form의 저장과 수정
  - (1) {%highlight python%}
if request.method=='POST':
        form=Webaddressform(request.POST)
        if form.is_valid():
            form.save()
            messages.info(request,"수정되었습니다.")
            return redirect('shortenwebadview')
{%endhighlight%}
  - (2) {%highlight python%}
if request.method=='POST':
        form=Webaddressform(request.POST,instance=posted)
        if form.is_valid():
            form.save()
            messages.info(request,"수정되었습니다.")
            return redirect('shortenwebadview')
{%endhighlight%}

  - (1)는 request에 대한 요청을 새롭게 저장한다.(즉, 수정이 아닌 추가이다.)
  - (2)은 instance에 대한 수정을 요청한다. 즉, 수정을 하기 위해서는 6번과 같이 적어줄 필요가 있다.
