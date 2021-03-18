# Django Intro



## Django

> 장고란 무엇일까

#### Django는 Python으로 작성된 오픈소스 웹 프레임워크이다.

- Python: 프로그래밍 언어
- 웹 프레임워크: 웹(페이지, 어플리케이션, 서비스)을 제작하는 도구. 웹을 구성하는 데에 필요한 함수, 라이브러리, 클래스 등 다양한 기능을 미리 만들고 묶어둔 것. 



## MVC

> 소프트웨어 디자인 패턴 중 하나

- Model: 데이터베이스 조작
- View: 사용자 인터페이스
- Controller: 로직

#### Django는 MVC와 동일하지만 이름만 다른 MTV 패턴을 사용한다.

- Model: MVC의 Model
- Template: MVC의 View
- View: MVC의 Controller



## Django Template Language

> Django의 Template(Django HTML)에서 사용하는 Django만의 언어

- 아래는 장고 공식 웹사이트에서 제안하는 템플릿

```django
{% extends "base_generic.html" %}

{% block title %}{{ section.title }}{% endblock %}

{% block content %}
<h1>{{ section.title }}</h1>

{% for story in story_list %}
<h2>
  <a href="{{ story.get_absolute_url }}">
    {{ story.headline|upper }}
  </a>
</h2>
<p>{{ story.tease|truncatewords:"100" }}</p>
{% endfor %}
{% endblock %}
```

- template은 html을 기반으로 한다. 따라서 css나 js도 적용할 수 있다.
- Django Template Language를 사용해 html만으로는 구현할 수 없는 다양한 기능(데이터 이동,  반복, 상속 등)을 구현할 수 있다.

### 자주 쓰는 DTL

추가 예정