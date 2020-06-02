---
# layout: "post"
title: "Django_nomadcoder_study"
date: "2018-01-12 10:59"
# categories: "Django"
  #Computer,Python,Math,Django,Javascript,Jupyter Notebook,Excel,TW
tag: Django
header:
  teaser: /assets/images/19.png

---

## NomadeCoder의 백엔드 강의 1

1. pipenv
  - 그냥 python3 -m venv mysite 가 나은듯 함.
  - 왜냐면 pipenv는 활성화되어있는지 확인이 안되는 것 같음.
2. cookiecutter
  - 글로벌하게 설치할 필요가 있음.(각 프로젝트별로 항상 쿠키커터 필요)
  - 깃헙에서 프로젝트를 clone할때 원하는대로 설정(프로젝트이름등)을 바꿔서 사용할 수 있음.
  - cookiecutter https://github.com/pydanny/cookiecutter-django
  - 각종 템플릿, requirements 등이 포함되어 있음.
  - 기본적으로 많은 패키지가 깔림. 좀 과하다 싶은 느낌이 있음.
  - https://postgresapp.com/ DB 설치
  - 디버그 툴바, 부트스트랩등 기본적인 것이 모두 설치되어 있음.
  - 처음 연결하면 데이터베이스가 없어서 오류, postgresapp을 실행시켜 데이터베이스를 생성해주면 됨.
  - CREATE DATABASE 데이터베이스이름;
  - user 앱이 이미 생성되어 있음.
  - app 에서 이름을 바꿔서 등록함.
  - django-admin startapp 으로도 됨.

3. admin에 쓸수 있는 것
  - list_display_links
  - search_fields
  - list_filter 등,

4. property decorator
{% highlight python %}
@property
def like_count(self):
    return self.likes.all().count()
{% endhighlight %}
 - 이렇게 하니 like_count를 필드처럼 사용할 수 있었음.
 - 예를 들어 serializers.py에서 다음과 같이 사용가능.
{% highlight python %}
class ImageSerializer(serializers.ModelSerializer):

    comments = CommentSerializer(many=True)
    creator = FeedUserSerializer()

    class Meta:
        model = models.Image
        fields = (
            'id',
            'file',
            'location',
            'caption',
            'comments',
            'like_count',
            'creator'
        )
{% endhighlight %}
5. url을 다음과 같이 사용가능

url(
        regex=r'(?P<image_id>[0-9]+)/like/',
        view=views.LikeImage.as_view(),
        name='like_image'
    )
