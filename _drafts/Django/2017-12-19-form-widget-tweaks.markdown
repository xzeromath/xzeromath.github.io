---
# layout: "post"
title: "Form_snippets"
date: "2017-12-19 12:54"
# categories: Django
tag: Django
  #Computer,Python,Math,Django,Javascript,Jupyter Notebook,Excel,TW

header:
  teaser: /assets/images/4.png

---

## Django form Html 꾸미기

### bootstrap을 사용하여 개별적으로 폼을 만드는 방법

{%highlight python%}
{%raw%}
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title></title>
  <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" />
  <script src="//code.jquery.com/jquery-2.2.4.min.js"></script>
</head>
<body>
  <div class="container">
    <form action="" method="post" class="form-horizontal" enctype="multipart/form-data">
      <legend>Post Form</legend>

           {% csrf_token %}


      {% for error in form.non_field_errors %}
      <div class="alert alert-danger">
        {{ error }}
      </div>
      {% endfor %}
      <!-- hidden fields는 위젯만 렌더링 -->

      {% for field in form.hidden_fields %}
      {{ field }}
     {% endfor %}

      <!-- visible fields는 모든 요소 렌더링 -->
      {% for field in form.visible_fields %}
      <div class="form-group">
        <label for="{{field.id_for_label}}">{{field.label}}</label> {{field}} {% for error in field.errors %}
        <span class="help-block">{{error}}</span> {% endfor %}

      </div>


      {% endfor %}
      <input type="submit" class="btn btn-primary btn-lg" />
    </form>
  </div>

</body>

</html>

{%endraw%}
{%endhighlight%}

### widget_tweaks을 사용하여 개별적으로 폼을 만드는 방법
- install apps : 'widget_tweaks'
- pip install django-widget-tweaks

{%highlight python %}
{%raw%}
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title></title>
  <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" />
  <script src="//code.jquery.com/jquery-2.2.4.min.js"></script>
</head>
<body>
{% load widget_tweaks %}
  <div class="container">
    <form action="" method="post" class="form-horizontal" enctype="multipart/form-data">
      <legend>Post Form</legend>
      {% csrf_token %}

      {% for error in form.non_field_errors %}
      <div class="alert alert-danger">
        {{ error }}
      </div>
      {% endfor %}

      <!-- hidden fields는 위젯만 렌더링 -->
      {% for field in form.hidden_fields %}
      {{ field }}
      {% endfor %}


      <!-- visible fields는 모든 요소 렌더링 -->
      {% for field in form.visible_fields %}
      <div class="form-group">
        <label for="{{field.id_for_label}}">{{field.label}}</label>
        {{ field|add_class:'form-control' }}
        {% if field.help_text %}<div class="help-block">{{ field.help_text }}</div>{% endif %}

        {% for error in field.errors %}
        <span class="help-block">{{error}}</span>
        {% endfor %}

      </div>
      {% endfor %}

      {% render_field form.title class="form-control" placeholder=form.title.label %}
      (참고) label 에는 verbose_name이 기재됨

      <input type="submit" class="btn btn-primary btn-lg" />
    </form>
  </div>

</body>

</html>

{%endraw%}
{%endhighlight%}

> https://simpleisbetterthancomplex.com/2015/12/04/package-of-the-week-django-widget-tweaks.html
