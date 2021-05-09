# JavaScript Basic

> JavaScript(ECMAScript6) Basic

<br>

## Identifier(식별자)

> Identifier(식별자, 변수명) 작성법

- 당연히, 다른 프로그래밍 언어들과 같이 대소문자를 구분한다.
- 문자, 달러사인($), 밑줄(_)로 시작한다. **숫자로 시작하지 않는다.**
- 예약어(파이썬의 <u>키워드</u>와 같음)를 변수명으로 사용할 수 없다.

### Naming Convention

- 변수, 객체, 함수: 카멜 케이스(`myVariable`, `myFunction`, `myObject`)
- 클래스, 생성자(ECMA6 이후  class 키워드 사용): 파스칼 케이스(MyClass, MyConstructor)
- 상수(변경될 가능성이 없는 값): 대문자 스네이크 케이스(MY_CONSTANT)

<br>

## Variable(변수)

> const, let, var* / 선언, 할당, 초기화

### const

- 재할당, 재선언 불가능: 주소를 바꿀 수 없다. 변수가 배열, 오브젝트 등일 때 그 내부의 데이터를 조작하는 것은 가능하다.

  - 반드시 선언과 동시에 초기화 해야한다.

  - ```javascript
    // good
    const myNum = 3
    // error
    const myConst
    ```

- 블록 스코프(블록({}) 내에서 선언한 경우 블록 밖에서 접근 불가): 함수도 블록 내에서 작동하므로 함수, if/for 문 등 모든 블록에 적용된다.

### let

- 재할당 가능 / 재선언 불가능
- 블록 스코프

### var

- ES6 이후에는 사용을 **지양**한다.

- 재할당, 재선언 가능
- 함수 스코프 - 함수 내에서 선언한 경우 함수 밖에서 접근 불가, if/for 문의 블록에서 생성된 것은 그 블록의 밖에서 접근 가능하다.

- <u>호이스팅(hoisting)</u>: 변수를 선언하기 이전에 참조할 수 있음. `undefined`를 반환한다.

- ```javascript
  // hoisting
  console.log(myVar)
  // undefined
  var myVar = 3
  
  // const는 같은 코드 실행 시 에러
  console.log(myConst)
  // error
  const myConst = 3
  ```

<br>

## Data Type

> JS의 모든 값은 데이터 타입을 가진다.

### 원시 타입(Primitive Type)

- 객체가 아닌 자료형
- 변수에는 해당 타입의 값이 할당된다.
- 다른 변수에 복사를 시도하면 실제 값이 복사된다.

### 원시 타입의 종류

- Number: 부동 소수점 사용, 계산할 수 없는 경우 NaN을 사용
- String: 템플릿 리터럴(python의 format) - backtick(`)과 ${} 를 이용
- Boolean: `true`/`false`, undefined, null, 빈 string, 0, NaN은 false 값을 가진다.
  - 모든 참조 타입 자료형은 true 값을 가진다
- undefined: 변수의 값이 할당되지 않을 때 자동으로 부여되는 자료형
- null: 변수의 값이 없음을 알리기 위해 사용하는 자료형. 직접 부여해야 한다.
  - null 타입은 원시 타입에 속하지만, <u>typeof 연산자의 결과는 object로 나온다.</u>

### 참조 타입(Reference Type)

- 객체 자료형
- 변수에는 해당 객체의 참조 값이 담긴다.
- 다른 변수에 복사하면, 참조 값이 복사된다. 즉, 복사한 변수를 변경하면 원래 변수도 변경된다.

### 참조 타입의 종류

- Objects: 객체(python의 dictionary와 유사)
- Array: 배열
- Function: 함수, 1급 객체
- ...

<br>

## 연산자

### 할당연산자

- ++ 사용 가능 `a++  =>  a += 1`

### 비교연산자

- `==`: 암묵적 형변환을 통해 타입을 일치시킨 후 비교, 두 피연산자 모두 객체일 경우 같은 객체를 참조하는지 판별 -> 예외 발생 가능성이 있어, 특별한 경우(`someObjectsOrPrimitve == null`: null 이나 undefined일 경우를 확인)를 제외하고는 사용하지 않는다.
- `===`: 두 비교 대상의 타입과 값이 모두 같은지 비교

### 논리연산자

- &&: 파이썬의 and
- ||: 파이썬의 or
- !: `3 != 4 -> true`와 같이 사용하기도 하고, 파이썬의 not의 역할도 한다.

<br>

## 조건문

### if

- 파이썬의 if 문과 거의 같다. () 안에 조건을, {} 안에 실행문을 작성한다. indent로 구분하는 건 파이썬이 특이한 것.

- 블록 스코프를 생성한다.

- ```javascript
  // if example
  const a = [1, 2, 3]
  if (a.length === 3) {
      a.push(4)
  } else if (a.length === 4) {
      a.push(5)
  } else {
      a.push(6)
  }
  ```

### switch

- 블록 스코프를 생성한다.

- () 의 결과값과 case 오른쪽 값을 비교하여 {} 의 실행문을 실행

- ```javascript
  // switch example - if문과 같은 로직을 switch로 구현할 때
  const a = [1, 2, 3]
  switch(a.length) {
      case 3: {
          a.push(4)
          break
      }
      case 4: {
          a.push(5)
          break
      }
      default: {
          a.push(6)
      }
  }
  ```

<br>

## 반복문

### for

- 블록 스코프를 생성한다.

- 기본형: `for(initialization; condition; expression) {//do something}`

- ```javascript
  // example
  for (let i = 0; i < 6; i++) {
      console.log(i)
  } // 0, 1, 2, 3, 4, 5
  ```

### for... in

- 블록 스코프를 생성한다.

- 오브젝트 순회 시 사용: 오브젝트 내의 모든 요소를 순회하기 때문에, 배열을 `for... in`을 사용하여 순회하면 원치 않는 요소까지 순회할 가능성이 있다.

- ```javascript
  const scores = {
      A: 100,
      B: 90,
      C: 70
  }
  for (let score in scores) {
      console.log(score)
  } // A, B, C
  ```

### for... of

- 블록 스코프를 생성한다.

- 반복 가능한 객체 순회 시 사용

- ```javascript
  const names = ['Jacob', 'Mathew', 'Marco']
  for (let name of names) {
      console.log(name)
  } // 'Jacob', 'Mathew', 'Marco'
  ```

