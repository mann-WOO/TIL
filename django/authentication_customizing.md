# Customizing authentication in Django

<br>

## Custom User Model 구현

> **프로젝트의 첫 번째 migrate와 전체 migrations의 시작 전에 커스텀 유저 모델로 대체해줘야 한다. - 프로젝트 생성과 동시에 진행하는 편이 좋다.**

1. `settings.py` 의 끝에 `AUTH_USER_MODEL = 'accounts.User(유저 모델 명)'` 추가

2. `accounts/models.py`에 다음과 같은 모델 추가

   ```python
   # accounts/models.py
   from django.db import models
   from django.contrib.auth.models import AbstractUser
   
   # Create your models here.
   
   class User(AbstractUser):
       pass
   ```

3. `UserCreationForm`, `UserChangeForm` 재정의하여 사용자화

### 유저 모델 참조

- `settings.AUTH_USER_MODEL`
  - models.py에서 유저 모델을 참조할 때 사용
  - 앱들의 호출 순서에 차이가 있기 때문에, `settings.py`의 문자열을 이용해 `User`를 참조한다.
  - 만약 `accounts` 앱이 `INSTALLED_APPS`의 최상단에 있다면 `get_user_model()`을 사용할 수도 있지만, 고려하기 쉽지 않고, 더 많은 경우에서의 에러 방지를 위해` models.py`에서는 이 방법을 사용한다.

- `get_user_model()`
  - 위 사항 외의 모든 경우 사용
  - 유저 모델이 커스터마이징 되어있다면 커스텀 유저 모델을 불러옴.

- 위의 두 방법은 커스텀하여 설정해둔 `User` 클래스를 반환한다.
  - `request.user`는 현재 접속하여 서비스를 사용중인 사용자의 유저 정보(`User` 인스턴스)를 반환한다.

<br>