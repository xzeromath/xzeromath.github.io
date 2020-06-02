---
# layout: "post"
title: "Django Admin"
date: "2017-07-18 13:29"
# categories: Django
tag: Django
header:
  teaser: /assets/images/6.png
---

- 장고의 admin은 staff/superuser 접근가능

{% highlight python %}
from django.contrib import Admin
from blog.models import Post

@admin.register(Post)
class PostAdmin(admin.ModelAdmin):
  list_display=['id','title']
  # 함수로 지정
  def content_size(self,post):
    return '{}글자'.format(len(post))
  content_size.short_description= "내용글자수"
  # 내용글자수가 admin에 표시됨.

{% endhighlight %}


## 예시) User 에서  is_active 를 False로 만드는 액션

{% highlight python %}

from django.contrib.auth.models import User

class UserAdmin(admin.ModelAdmin):
    actions = ['my_is_active']

    def my_is_active(self, request, queryset):
        updated_count = queryset.update(is_active="False")
        self.message_user(request,"{}건이 등록되었음".format(updated_count))
    my_is_active.short_description="is_active를 거짓으로 만듦."

admin.site.unregister(User)
admin.site.register(User, UserAdmin)
{% endhighlight %}

- queryset.update(is_active="False")은 내용을 업데이트하고 변경된 쿼리의 수를 리턴함.


-----
> [AskDjango](https://nomade.kr) EP8. Django Admin
