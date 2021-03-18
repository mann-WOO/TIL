# Django CRUD project

> CRUD 기능을 가진 Django 프로젝트 처음부터 끝까지 만들어보기
>
> 아직 익숙하지 않고, 배우는 중이여서 최선의 순서로, 최적의 기능을 구현하지는 못하지만 CRUD가 작동하는 웹페이지를 제작합니다.

<br>

## 0. venv 설정

> 다른 작업 환경에서도 개발이 이루어질 수 있도록 가상환경에서 개발을 진행합니다.

1. 작업 폴더의 터미널에서 `python -m venv venv` 명령어로 가상환경 생성합니다.
2. `source venv/Scripts/activate` 명령어로 가상환경을 인터프리터로 설정합니다.
3. `pip install django`, `pip install django-bootstrap-v5`로 (현재 시점에서) 프로젝트에 필요한 django 프레임워크와 django html 내에서 bootstrap을 사용할 수 있게 하는 django-bootstrap을 설치합니다.
4. `pip freeze > requirements.txt`를 통해 현재까지 pip를 통해 설치한 라이브러리의 목록을 저장합니다. (추가로 설치할 때마다 같은 과정을 통해 업데이트)

<br><br>

## 1. django project / app / base 템플릿 생성

<br>

### 프로젝트와 앱 생성 및 등록

1. 작업 폴더의 터미널에서 `django-admin startproject crud .` 명령어로 crud 프로젝트를 생성합니다.

2. `python manage.py startapp articles` 명령어로 articles 앱을 생성합니다.

3. `crud/settings.py`의 `INSTALLED_APPS`에 생성한 앱, 3rd-party 앱(bootstrap)을 추가합니다.

4. `crud/urls.py`에서 `from django.urls import include`를 추가해 앱 url 목록을 이용할 수 있게 합니다.  `urlpatterns`에 `path('articles/', include('articles.urls'))`를 추가해 프로젝트 url 목록에 앱 url 목록을 추가합니다.

5. `articles/urls.py`에 `from django.urls import path`를 추가해 url path를 추가할 수 있게 합니다. `app_name = 'articles'`를 추가해 namespace를 설정합니다. `urlpatterns` 리스트를 생성합니다. `urls.py`는 아래와 같습니다.

   ```python
   from django.urls import path
   
   app_name = 'articles'
   
   urlpatterns = [
   ]
   ```

   <br>

### base 템플릿 생성

1. `crud/templates` 폴더를 생성하고 해당 폴더에 `base.html` 파일을 생성합니다.
2. html 기초 뼈대(! + tab)를 잡고, `{% load bootsrap5 %}`를 최상단에 입력해 부트스트랩 태그 라이브러리를 사용할 수 있게 합니다.
3. `<head>` 태그에 `{% bootstrap_css %}`, `<body>` 태그에 `{% bootstrap_javascript %}`를 추가해 부트스트랩 CSS와 JavaScript를 불러옵니다.
4. `{% block content %}`, `{% endblock %}` 태그로 현재 html 문서를 상속받아 작성할 부분을 표시합니다.
5. `crud/settings.py`의 `TEMPLATE` 리스트 내부 딕셔너리의 `DIR` 키의 값으로 `BASE_DIR / 'crud' / 'templates'`를 추가해 서버에서 base.html을 인식할 수 있게 합니다.

<br><br>

## 2. model과 form 생성

> db를 관리할 model과 db의 input을 관리할 form을 생성합니다.

<br>

### model 생성

1. `articles/models.py`를 아래와 같이 편집해 데이터를 저장하고 불러올 클래스 `Article`을 설정합니다.

   ```python
   from django.db import models
   
   class Article(models.Model):
       title = models.CharField(max_length=10)
       content = models.TextField()
       created_at = models.DateTimeField(auto_now_add=True)
       updated_at = models.DateTimeField(auto_now=True)
   ```

2. `python manage.py makemigrations` 명령어로  `models.py`의 내용을 ORM을 통해 migration 파일을 생성합니다.
3. `python manage.py migrate` 명령어로 migration 파일이 생성된 `models.py`의 내용을 최종적으로 db에 반영합니다.

<br>

### form(ModelForm) 생성

1. `articles/forms.py`를 생성합니다. 아래와 같이 작성합니다.

   ```python
   # forms 라이브러리 불러오기
   from django import forms
   # 사용할 모델 불러오기
   from .models import Article
   
   # ModelForm 클래스 생성
   class ArticleForm(forms.ModelForm):
   
       # Meta 클래스 생성
       class Meta():
           # ModelForm의 데이터가 되는 model 설정
           model = Article
           # form으로 작성할 field(column) 설정 -> 작성 가능한 모든 것
           fields = '__all__'
   ```

<br>

<br>

## 3. Read 기능 구현

> index 페이지와 detail 페이지를 통해 Read 기능을 구현합니다.

<br>

### index 페이지 구현

1. `articles/urls.py`의 최상단에 `from . import views`를 추가해 views를 사용할 수 있게 합니다.  `urlpatterns` 리스트에 `path('', views.index, name='index')`를 추가합니다.

2. `articles/views.py`를 아래와 같이 편집해 index 함수를 생성합니다. 아직 아무런 데이터도 입력하지 않았지만, 추후 입력될 것이기 때문에 미리 페이지를 구성합니다.

   ```python
   # index 페이지의 요청이 있을 때 랜더링하여 반환하는 함수
   def index(request):
       # models.py의 Article 클래스에 속한 객체들의 Queryset을 articles에 할당
       articles = Article.objects.all()
       # articles를 html에서 사용하기 위해 context에 담는다.
       context = {
           'articles': articles
       }
       return render(request, 'articles/index.html', context)
   ```

3. `articles/templates/articles` 폴더를 생성하고 `index.html` 파일을 생성합니다.  dtl과 html, css를 이용해 적절하게 데이터의 목록을 표시합니다.

4. 각 글의 detail 페이지로 진입할 수 있는 링크를 생성해 둡니다. 에러 방지를 위해 url 입력부분을 `<a href="#"><h5>[Detail]</h5></a>`와 같이 비워둡니다. 새 글 등록을 위한 링크 또한 url을 비워 둔 채 구현합니다. 빈 url은 해당 기능을 구현하면 채워줍니다.

<br>

### detail 페이지 구현

1. `urlpatterns` 리스트에 `path('<int:pk>', views.detail, name='detail')`를 추가합니다.

2. `articles/views.py`를 아래와 같이 편집해 detail 함수를 생성합니다.

   ```python
   # pk를 추가적인 인자로 받는 detail 함수
   def detail(request, pk):
       # pk로 인자로 받은 pk의 값을 가지는 Article의 인스턴스를 article에 할당
       article = Article.objects.get(pk=pk)
       context = {
           'article': article
       }
       return render(request, 'articles/detail.html'. context)
   ```

3. `articles/templates/articles` 폴더에 `detail.html` 파일을 생성합니다. index와 마찬가지로 적절하게 데이터의 상세 정보를 표시합니다.

4. index로 돌아갈 수 있는 링크, 글을 수정 및 삭제할 수 있는 링크를 생성해 둡니다. index로 가는 링크는 `<a href="{% url 'articles:index' %}"><h5>[Back]</h5></a>`의 형태로 바로 입력하고, 수정 및 삭제 페이지는 비워둡니다.

<br>

<br>

## 4. Create 기능 구현

1. `urlpatterns` 리스트에 `path('create/', views.create, name='create')`를 추가합니다.

2. `articles/views.py`를 아래와 같이 편집해 detail 함수를 생성합니다.

   ```python
   # 새로운 데이터를 입력받을 form을 보여주거나 받은 데이터를 저장하는 create
   def create(request):
       # 제공한 form에 데이터를 받은 경우
       if request.method == 'POST':
           # ModelForm에 데이터를 입력
           form = ArticleForm(request.POST)
           # 유효성 검사(글자수, 타입 등)
           if form.is_valid:
               # 저장
               article = form.save()
               # 상세 페이지로 redirect
               return redirect('articles:detail', article.pk)
       # form을 제공해야 할 경우
       else:
           # Article 모델의 빈 form 생성
           form = ArticleForm()
       # context는 빈 form이나, 유효성 검사에 실패한 덜 에러가 있는 form
       context = {
           'form': form
       }
       return render(request, 'articles/form.html', context)
   ```

3. `form`을 이용해 새 글 작성 및 수정을 위한 `form.html` 파일을 생성 및 편집합니다. 아래와 같이 편집했습니다.

   ```django
   {% extends 'base.html' %}
   
   {% block content %}
     <form action="" method="POST">
     {% csrf_token %}
       {{ form.as_p }}
       <input type="submit" value="submit">
     </form>
   {% endblock  %}
   ```

<br>

<br>

## 5. Update 기능 구현

1. `urlpatterns` 리스트에 `path('<int:pk>/update', views.update, name='update')`를 추가합니다.

2. `articles/views.py`를 아래와 같이 작성해 update 함수를 구현합니다.

   ```python
   # 기존 데이터 업데이트를 위한 update 함수
   def update(request, pk):
       # 입력받은 pk를 이용해 기존 데이터 불러오기
       article = Article.objects.get(pk=pk)
       # 제공한 form에 데이터를 받은 경우
       if request.method == 'POST':
           # ModelForm의 기존 데이터에 받은 데이터를 업데이트
           form = ArticleForm(request.POST, instance=article)
           # 유효성 검사
           if form.is_valid:
               # 저장
               form.save()
               # 상세페이지로 redirect
               return redirect('articles:detail', article.pk)
       # form을 제공해야 할 경우
       else:
           # 기존 데이터가 입력되어 있는 form 할당
           form = ArticleForm(instance=article)
       context = {
           'form': form
       }
       return render(request, 'articles/form.html', context)
   ```

3. create 과정에서 사용했던 `form.html`을 재사용하기 때문에 추가적인 템플릿 파일의 작성은 필요 없습니다. Update는 Detail 페이지에서 링크를 통해 접근 가능합니다.

<br>

<br>

## 6. Delete 기능 구현

1. `urlpattenrs` 리스트에 `path('<int:pk>/delete', views.delete, name='delete')`를 추가합니다.

2. `articles/views.py`를 아래와 같이 작성해 저장된 데이터를 삭제하는 delete 기능을 구현합니다.

   ```python
   # 삭제하는 delete 함수의 로직
   def delete(request, pk):
       # 전달받은 pk에 해당하는 데이터를 article에 할당
       article = Article.objects.get(pk=pk)
       # 삭제
       article.delete()
       # Index 페이지로 redirect
       return redirect('articles:index')
   ```

3. delete 기능은 detail 페이지의 링크를 통해 작동하기 때문에 추가적인 템플릿 작성이 필요 없습니다.

<br>

<br>

## 7. 기타 사항

1.  admin 페이지를 구성하는 부분은 본 md 파일에 작성하지 않았습니다.

2. `articles/views.py`에서 `require` 데코레이터를 이용하여 각 페이지의 접근 방식을 제한해야 하지만 구현하지 않았습니다.

3. 웹페이지 제작 과정에서 오류, 설계 미스 등으로 뒤로 돌아가는 과정이 있어, 모든 과정이 기록되지는 않았습니다.

4. 최종적인 `articles/ulrs.py`의 구조는 다음과 같습니다.

   ```python
   from django.urls import path
   from . import views
   
   app_name = 'articles'
   
   urlpatterns = [
       path('', views.index, name='index'),
       path('<int:pk>', views.detail, name='detail'),
       path('create/', views.create, name='create'),
       path('<int:pk>/update', views.update, name='update'),
       path('<int:pk>/delete', views.delete, name='delete'),
   ]
   ```

   