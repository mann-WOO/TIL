# Python_basic

---

기초 문법, 자료형, 연산자



## 기초 문법

---

### 주석(comment)

- `# 주석`

- ```python
  """
  주석
  """
  ```

- 한 줄은 `#`, 여러 줄은 세 쌍의 `"`로 감싸서 쓴다.

### 코드 작성

- 반드시 한 줄에 하나의 statement만 작성한다.
- 두 줄 걸치면 run 불가.

### 변수(variable)

- `a = 3`의 형태로 변수를 할당한다.
  - `a = b = 3`의 형태로 동시에 여러 변수에 하나의 값을 할당할 수 있다
  - `a, b = 1, 3`의 형태로 동시에 여러 변수에 다른 값을 할당 할 수 있다.
    - `a, b = b, a`의 형태로 쉽게 두 변수의 값을 스왑할 수 있다.

### 식별자(Identifier)

- 변수, 함수, 모듈, 클래스 등을 식별하는 이름

- 첫 글자 숫자 금지

- ``` python
  import keyword
  print(keyword.kwlist)
  ```

  위의 코드로 식별자로 사용할 수 없는 키워드를 알 수 있음

- 명명법 세 가지

  - camel case: myVariableName
  - snake case: my_variable_name
  - pascal case: MyVariableName



## 자료형(Data Type)

---

### 숫자

- int

- float

  - 소수 부분의 표현 문제~ 2진수 표현 시 소수 표현이 부정확(부동소수점), 연산과 대소 비교 등에 문제 발생

  - ```python
    # 1
    import sys
    abs(a-b) <= sys.float_info.epsilon
    # 2
    import math
    math.isclose(a, b)
    ```

    위의 방법을 비교 가능

- complex

  - `complex('1+2j')`
  - 복소수, 자주 쓰이진 않음

### 문자(string)

- 인덱싱, 슬라이싱 가능
- escape sequence: `\`이용해 공백, 탭, 인용부호 등 사용
- 포맷팅(interpolation)
  - `'hello, {}'.foramt(name)`
  - `f'hello, {name}'`
  - `{}` 안에서 연산도 가능

### 참/거짓(Boolean)

- `True`/`False`
- `True`는 1, `False`는 0의 값을 가진다.
  - 0.0, 비어있는 리스트/튜플/딕셔너리/문자열, None 또한 False로 변환



## 연산자(Operator)

---

### 산술연산자, 비교연산자

### 논리연산자

- `and`는 모두 `True`일때 전체가 `True`
  - 따라서, 여러 값들을 `and`로 묶어두면 순서대로 연산해보고, 처음 만나는 `False`, 혹은 마지막에 멈추고 값을 반환한다.
  - `True and 3 and 'c'` 의 결과값은 `'c'`
  - `'a' and 3 and [] and True`의 결과값은 `[]`
- `or`은 하나라도 `True`이면 전체가 `True`
  - 따라서, 여러 값들을 `or`로 묶어두면, 순서대로 연산해보고, 처음 만나는 `True`, 혹은 마지막에 멈추고 값을 반환한다.
  - `False or False or [] or 0 or 3 or {}`의 결과값은 3
  - `False or 0 or False or None`의 결과값은 None





