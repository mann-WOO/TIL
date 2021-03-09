# Django Start

> 장고 프로젝트/앱/템플릿 생성 방법
>
> 템플릿 상속과 variable routing



## 프로젝트 생성

1. 폴더 생성 후 해당 폴더에서 터미널 실행
2. `django-admin startproject 프로젝트명 .` 
   - `django-admin startproject 프로젝트명`('.'을 제외)로 프로젝트를 생성하면 현재 폴더에 `프로젝트명` 폴더를 만들고 그 안에 장고 파일을 생성한다.



## 앱 생성 및 등록

1. 프로젝트 폴더의 터미널에서 `python manage.py startapp 앱이름`으로 앱 생성

   - 앱 이름은 항상 복수형으로 설정한다.
   - 앱은 기능별로 적절히 나누어 생성한다.

2. `프로젝트명/settings.py`의 `INSTALLED_APPS`리스트의 가장 상단에 `'앱이름'`을 추가하여 프로젝트에 앱을 등록한다.

3. `프로젝트명/urls.py`의 `urlpatterns` 변수에 생성한 앱의 `urls.py` 경로를 아래와 같이  추가한다.

   ```python
   from django.contrib import admin
   # 기본으로 path 함수만 import 되어 있으므로, include를 추가한다.
   from django.urls import path, include 
   
   urlpatterns = [
       # admin은 기본으로 추가되어 있다.
       path('admin/', admin.site.urls),
       path('앱 이름/', include('앱 이름.urls')),
   ]
   ```

   - 위와 같이 프로젝트의 `urls.py`에는 각 앱의 `urls.py`의 경로를 추가하고, 앱의 템플릿들은 각 앱의 `urls.py`에서 관리하여 프로젝트의 유지보수를 용이하게 한다.
   - 또한, 각기 다른 앱에 같은 이름의 템플릿이 존재할 때 아래의 `namespace`를 사용해 혼선이 발생하지 않게 한다. 

4. `앱이름/urls.py` 파일을 생성하고, 아래와 같이 초기화한다.

   ```python
   from django.urls import path
   from . import views
   
   # namespace: django html에서 {% url 'pages:index' %}의 형태로 찾아갈 수 있다.
   app_name = '앱이름'
   
   urlpatterns = []
   ```

   

## 템플릿 생성과 조작

1. `앱이름/urls.py`의 `urlpatterns`리스트에 `path('template/', views.template, name='template')`을 원소로 추가한다. `template`에는 템플릿의 기능을 알 수 있는 템플릿 이름을 지어 사용한다.

2.  `앱이름/views.py`에 해당 템플릿에 대한 함수를 아래와 같이 작성

   ```python
   from django.shortcuts import render
   
   
   # Create your views here.
   
   
   # index라는 이름을 가진 template에 대한 요청이 있을 때 작동하는 함수
   def index(request):
       return render(request, '앱이름/index.html')
   ```

3. `앱이름/templates/앱이름` 폴더를 생성하고, 해당 폴더에 `템플릿이름.html`파일을 생성한다. 해당 주소(`127.0.0.1/앱이름/템플릿이름`)를 요청했을 때 보여질 html 문서를 작성한다.

4. 필요할 경우 `앱이름/views.py`의 함수에서 해당 html 파일에서 사용할 변수들의 딕셔너리 `context`를 선언할 수 있다. `앱이름/urls.py`, `앱이름/views.py`, html 문서를 함께 조작하여 다양한 기능을 추가할 수 있다.



## 그 외의 기능

### 템플릿 상속

1. settings.py 에서 템플릿 디렉토리 설정: `'DIRS': [BASE_DIR / '프로젝트명' / 'templates']`

2. `'프로젝트명' / 'templates'` 폴더에 `base.html` 파일을 만들고 모든 앱들의 템플릿이 공유 할 기본적인 틀을 제작

3. `base.html`에서 템플릿마다 다르게 작성할 부분은 `  {% block content %}{% endblock content %}`으로 표기

4. 앱 내에 템플릿을 생성하고, `{% extends 'base.html' %}`을 입력해 아래와 같이 `base.html`의 요소를 상속받아 작성

   ```django
   {% extends 'base.html' %}
   
   {% block content %}
   {# 여기에 작성 #}
   {% endblock content %}
   ```

   

### 사용자 인풋(form)을 이용한 동적 웹(ex_검색창)

### variable routing을 이용한 동적 웹(ex) 게시판)

