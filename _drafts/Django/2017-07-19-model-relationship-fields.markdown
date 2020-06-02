---
# layout: "post"
title: "Model Relationship Fields"
date: "2017-07-19 11:25"
# categories: Django
tags: Django
header:
  teaser: /assets/images/9.png
---

### 1-N 관계
장고
```python
class Post(models.Model):
  title = models.CharField(max_length=10)
  content = models.TextField()

class Comment(models.Model):
  post = models.ForeignKey(Post)
  message = models.TextField()

```


- 위에서 Comment 는 DB에 blog_comment 라는 이름으로 테이블 생성
- 외래키로 지정된 post는 DB에 post_id 라는 fields 생성
- 위에서  post = models.ForeignKey(Post)는
post = models.ForeignKey('Post') 로 쓸 수 있다.
- 이때,
  1. post = models.ForeignKey(Post)
  - 반드시 Post가 위에 정의되어 있어야 함.
  2.post = models.ForeignKey('Post')
  - 어디에 있든 상관없음.
  3. 다른 앱에 있는 경우에는
post = models.ForeignKey('appname.Post')
와 같이 지정하면 된다.

### Tip
```python
Post.objects.filter(tag_set__name='askdjango')
Post.objects.filter(tag_set__name__in=['askdjango','Python'])
```

와 같이 쿼리셋을 찾을 수 있다.

### user과 관계 추천 설정
```python
from django.conf import settings
user = models.OneToOneField(settings.AUTH_USER_MODEL)
profile.user_id  # id번호
profile.user # 작성자
```

- 즉, 모델을 구성할 때,
```user = models.OneToOneField(settings.AUTH_USER_MODEL)```
일때 Fetch가 되는 것이 아니라,
```python
profile.user_id  # id번호
profile.user # 작성자
```
와 같은 명령어가 나올때 fetch가 된다. (laze)

### ForeignKey에서 related_name
post, comment 가 있을때
```python
post= Post.objects.first()
Comment.objects.filter(post=post) # 방법1
post.comment_set.all() #방법2 -related name 사용
comment= Comment.objects.first()
comment.post
```

- 중간에 외래키로 연결된 user를 삽입한 경우 이미 생성된 값들에
어떠한 값을 연결할지 묻는 질문이 나옴.
- 이때 넣는것은 user의 값이 아니라, user_id의 값을 묻는 것임.
따라서 User.objects.get(pk=1) 이라 하면 안되고
숫자 1은 된다.


> [AskDjang](https://nomade.kr) EP11. Model Relationship Fields
