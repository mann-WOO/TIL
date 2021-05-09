# Function (함수)

<br>

## JS 함수의 특징

- JS의 함수는 일급 객체이다
  - 변수에 할당이 가능하다
  - 함수의 매개변수로 전달 가능하다.
  - 함수의 반환값으로 사용 가능하다.
- `typeof`연산자의 결과는 `function`이다.

<br>

## 함수 작성법

### 함수 선언식

```javascript
function myFunction(arg1, arg2) {
    return arg1 + arg2
}
```

- 익명 함수 정의 불가능
- 호이스팅 발생(함수 호출 이후에 선언해도 동작함)

### 함수 표현식

```javascript
const myFunction = function (arg1, arg2) {
    return arg1 + arg2
}
```

- 익명 함수 정의 가능
- 호이스팅이 발생하지 않음(`var`로 변수를 정의하면 호이스팅 발생 - 함수로 사용할 수는 없지만, 해당 변수가 undefined로 초기화됨.)

### Arrow Function

```javascript
// arrow function 기본형
const arrowFunction = (arg) => {return `entered ${arg}`}
// 매개변수가 하나이고, 실행부가 하나의 표현식이므로 생략 가능한 부분 생략
const arrowFunction = arg => `entered ${arg}`
```

- 화살표(=>)를 이용해 함수를 정의한다.
- fucntion 키워드를 생략할 수 있다.
- 함수의 매개변수가 하나뿐이라면, '()'도 생략 가능하다.
- 함수의 실행부가 하나의 표현식으로 이루어져 있다면 return과 '{}'도 생략 가능하다.