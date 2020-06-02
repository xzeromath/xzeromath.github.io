---
# layout: "post"
title: "View_save_snippets"
date: "2017-12-19 13:22"
# categories: Django #Computer,Python,Math,Django,Javascript,Jupyter Notebook,Excel,TW
tag: Django
header:
  teaser: /assets/images/10.png

---

# views에서 저장 로직
- 저장 기본 로직

``` python
from django.shortcuts import render, redirect
from .models import MyTest
from .forms import MyTestForm


def form1(request):
    mytest = MyTest.objects.all()
    if request.method == 'POST' :
        form = MyTestForm(request.POST)

        if form.is_valid():
            form.save()
            return redirect('sage:index')
    else:
        form = MyTestForm()

    return render(request,'formtest/form1.html',{'form':form})
```
