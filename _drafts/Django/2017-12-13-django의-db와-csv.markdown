---
# layout: "post"
title: "Django의 DB와 csv"
date: "2017-12-13 21:47"
# categories: "Django"
slug: Django_DB_csv
tag: Django
header:
  teaser: /assets/images/8.png

---

## Django의 DB의 내용을 CSV로 바꾸는 코드

> https://github.com/azavea/django-queryset-csv

{% highlight python %}
from djqscsv import render_to_csv_response

def csv_view(request):
  qs = Foo.objects.filter(bar=True).values('id', 'bar')
  return render_to_csv_response(qs)
{% endhighlight %}
- 위와 같이 하면 파일로 받아짐.


{% highlight python %}

from djqscsv import write_csv

qs = Foo.objects.filter(bar=True).values('id', 'bar')
with open('foo.csv', 'wb') as csv_file:
  write_csv(qs, csv_file)
{% endhighlight %}
- 위와 같이 하면 서버의 어디엔가에 csv로 저장됨.

## 그런데, 더 괜찮은 라이브러리 발견
> https://simpleisbetterthancomplex.com/packages/2016/08/11/django-import-export.html

이것으로 쓰면 될듯!!
