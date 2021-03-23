# Django Authentication

> Django의 인증(Authentication)과 권한부여(Authorization)

<br>

## Authentication 개념

> Django는 인증과 권한부여 기능이 하나로 작동한다.

### Http의 특징

- http는 비연결지향(connectionless)와  무상태(stateless)의 특징을 가진다. 즉, 요청과 응답이 이루어지고 나면 다음 요청이 있을 때까지 사용자는 서버와 통신하지 않는다.
- 따라서, 웹서비스에서 인증(로그인) 상태를 유지하기 위해서는 통신이 아닌 다른 방법으로 인증 상태를 확인해야 한다. 이를 위해 쿠키와 세션이 이용된다.

### 쿠키

- 쿠키는 웹에서 사용한 데이터의 흔적을 남기는 것이다.
- 데이터의 흔적을 이용해 서버와 연결되지 않은 상태에서 사용자의 데이터를 유지시킬 수 있다.
- 쿠키는 사용자의 브라우저(크롬 등)이 관리한다.
- 쿠키는 누구나 접근할 수 있기 때문에 ID나 Password 등 인증을 위한 개인적인 정보를 쿠키에 저장하는 것은 위험하다. 따라서 인증을 위한 통신에서 최초 1회 ID와 Password를 확인하고, **세션**을 생성해 사용자의 쿠키와 서버에 각각 하나씩 보관한다. 이후 인증이 필요한 요청이 있을 때는 해당 세션을 대조하여 권한을 부여한다.

<br>

## Authentication 구현(CRUD)

> Django에 내장된 User 모델과 auth forms를 사용하여 기본적인 CRUD를 구현한다.

```python
# views.py 라이브러리 목록
from django.shortcuts import render, redirect, get_object_or_404
from django.contrib.auth.forms import (
    UserCreationForm, 
    AuthenticationForm, 
    UserChangeForm, 
    PasswordChangeForm,
)
from django.contrib.auth import update_session_auth_hash
from django.contrib.auth import login as auth_login
from django.contrib.auth import logout as auth_logout
from django.contrib.auth.models import User
from django.contrib import messages
```



### Create(회원가입)

```python
# views.py
def signup(request):
    # 데이터 저장 로직
    if request.method == 'POST':
        form = UserCreationForm(request.POST)
        if form.is_valid():
            form.save()
            return redirect('accounts:login')
    # 회원가입 폼 응답으로 보내주는 로직
    else:
        form = UserCreationForm()
    context = {
        'form': form
    }
    # 회원가입, 정보수정, 로그인 모두 form.html을 이용
    return render(request, 'accounts/form.html', context)
```



### Read(회원정보)

```python
def profile(request, username):
    user_info = get_object_or_404(User, username=username)
    context = {
        'user_info': user_info,
    }
    return render(request, 'accounts/profile.html', context)
```



### Update(회원정보 수정)

```python

```



### Delete회원탈퇴

```python

```



## Authentication 구현(login/logout)

### login

```python

```



### logout

```python

```



## 구현 과정에서 궁금한 것

### base.html에서 user 변수를 사용할 수 있는 이유

- settings.py의 TEMPLATES 리스트를 보면 장고에서 html을 렌더링할 때 기본적으로 전달하는 context들의 목록이 있다. 그 안에 들어있기 때문에 사용할 수 있다.
- request는 모든 함수에서 반드시 전달하도록 설정되어 있다. user는 request.user 와 같다.