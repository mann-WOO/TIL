# Error



## 오류(Error)

> 파이썬이 에러라고 한다: 잘 읽고, 이해하고, 고친다.

> Syntax Error, Index Error, Key Error가 주로 발생



## 예외 처리(Exception Hnadling - )

> `try ` and  `except`

### 기초 문법

```python
try:
    <code block1>
except:
    <code block2>
```

- `try` 코드블럭이 실행
- 에러가 발생하지 않으면 `except`는 실행되지 않음
- 에러가 발생하면 그 지점에서 멈추고 `except`  실행



## 예외 발생시키기

### raise

### assert

- TDD에서 자주 쓰인다.

- TDD: 테스트 주도 개발 - 테스트 코드를 먼저 작성하고, 테스트 코드를 통과하도록 개발하는 방법론

- 내가 생각한 결과와 실제 결과를 비교하고 에러를 발생시키는 방식