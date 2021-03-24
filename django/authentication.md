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

<br>

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

- `UserCreationForm`은`ModelForm`이다.

### Read(회원정보)

```python
# views.py
def profile(request, username):
    user_info = get_object_or_404(User, username=username)
    context = {
        'user_info': user_info,
    }
    return render(request, 'accounts/profile.html', context)
```

- `username` 혹은 `pk` 값과 같은 유일한 정보를 통해 유저의 개별 정보에 접근한다. 

### Update(회원정보 수정)

```python
# views.py
def update(request):
    if request.method == "POST":
        form = CustomUserChangeForm(request.POST, instance=request.user)
        if form.is_valid():
            form.save()
            return redirect('articles:index')
    else:
        form = CustomUserChangeForm(instance=request.user)
    context = {
        'form': form,
    }
    return render(request, 'accounts/update.html', context)
```

- `UserChangeForm`은 관리자 권한 부여 등 일반 유저가 접근하기에 적절하지 않은 form들을 포함한다. 따라서 회원정보 수정 시 일반 유저가 변경해도 되는 적절한 항목들을 골라 `UserChangeForm`을 상속받은 `CustomUserChangeForm`을 만들어 사용한다.
- `UserCreationForm`과 마찬가지로, `ModelForm`과 같은 방식으로 사용한다.

### Delete(회원탈퇴)

```python
# views.py
def delete(request):
    if request.user.is_authenticated:
        request.user.delete()
    return redirect('articles:index')
```

<br>

## Authentication 구현(login/logout)

### login

```python
# views.py
def login(request):
    if request.user.is_authenticated:
        return redirect('articles:index')
    if request.method == 'POST':
        form = AuthenticationForm(request, request.POST)
        if form.is_valid():
            # 세션 생성
            auth_login(request, form.get_user())
            return redirect(request.GET.get('next') or 'articles:index')
    else:
        form = AuthenticationForm()
    context = {
        'form': form,
    }
    return render(request, 'accounts/login.html', context)
```

- `AuthenticationForm`은 `ModelForm`이 아닌 `Form`이다. `ModelForm`은 모델의 데이터를 생성 혹은 변경할 때 사용된다. `login`은 유저가 입력한 데이터가 모델의 데이터와 일치하는지 확인하고 세션을 발급하는 용도로 사용되기 때문에 `ModelForm`을 사용하지 않는다.
- `request.GET.get('next') or 'articles:index'`는 단축평가를 이용해 `GET` 메서드로 전달받은 `next` 값이 있을 시 로그인 후 바로 해당 페이지로 이동시켜주는 역할을 수행한다. `@login_required` 데코레이터에 의해 로그인 페이지로 이동된 경우 작동한다.
  - 이렇게 이동된 페이지는 마찬가지로 `GET` 방식으로 접근한다. 따라서  `POST` 방식의 접근만 허용된 페이지는 `next` 값을 통해 이동하게 되면 http 에러가 발생한다. 이를 해결하기 위해서는 `@require_POST` 데코레이터를 해제하고 내부 로직으로 `GET` 방식의 접근을 우회해 주는 등 다양한 방식의 고민이 필요하다.

### logout

```python
# views.py
def logout(request):
    auth_logout(request)
    return redirect('articles:index')
```



## 구현 과정에서 궁금한 것

### base.html에서 user 변수를 사용할 수 있는 이유

- settings.py의 TEMPLATES 리스트를 보면 장고에서 html을 렌더링할 때 기본적으로 전달하는 context들의 목록이 있다. 그 안에 들어있기 때문에 사용할 수 있다.
- request는 모든 함수에서 반드시 전달하도록 설정되어 있다. user는 request.user 와 같다.



