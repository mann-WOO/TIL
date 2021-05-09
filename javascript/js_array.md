# Array (배열)

<br>

## 배열의 특징

- 참조 타입의 객체 자료형
- 순서를 보장
- 각 원소는 0부터 시작하는 인덱스를 가짐

<br>

## 배열 자료형 주요 메서드

- reverse(`myArray.reverse()`): 배열의 요소들을 반대로 정렬
- push&pop(`myArray.push(1)`/`myArray.pop()`): 배열 가장 뒤에 요소를 추가/제거
- unshif&shif(`myArray.unshift(1)`/`myArray.shift()`): 배열 가장 앞에 요소를 추가/제거
- includes(`myArray.include(1)`): 배열에 특정 값 존재하는지 판별하여 true/false 반환
- indexOf(`myArray.include(1)`): 배열에 특정 값 존재하는지 판별하여 해당 인덱스 반환
- join(`myArray.join('/')`): 배열의 요소 구분자 이용해 연결(기본값: ',')

<br>

## Array Helper Method

- 배열을 순회하며 특정 로직을 수행
- 인자로 callback 함수를 받는다.

### Array Helper Method의 종류

- **forEach**: 배열의 요소에 대해 각각 콜백 함수를 실행(return 값 없음)

- ```javascript
  const myArray = [1, 2, 3]
  const yourArray = []
  
  myArray.forEach((num) => {
      yourArray.push(num+1)
  })
  
  console.log(yourArray) // [2, 3, 4]
  ```

- **map**: 콜백 함수의 반환 값을 요소로 하는 새로운 배열 반환

- ```javascript
  const myArray = [1, 2, 3]
  const yourArray = myArray.map((num) => {
      return num + 1
  })
  
  console.log(yourArray) // [2, 3, 4]
  ```

- **filter**: 콜백 함수의 반환 값이 참인 요소들만 모아 새로운 배열 반환

- ```javascript
  const myArray = [1, 2, 3]
  const yourArray = myArray.filter((num) => {
      return num > 0
  })
  
  console.log(yourArray) // [1, 2, 3]
  ```

- reduce: 콜백 함수의 반환 값들을 하나의 값에 누적하여 반환 - 콜백 함수의 인자로 누적 값을 가지고 갈 변수를 입력해야 한다.(배열, 숫자 모두 가능)

- ```javascript
  const myArray = [1, 2, 3]
  const mySum = myArray.reduce((acc, num) => {
      return acc + num
  })
  
  console.log(mySum) // 6
  ```

- find: 콜백 함수의 반환 값이 참이면 해당 요소를 반환
- some: 콜백 함수의 반환 값이 하나라도 참이면 true 반환
- every: 콜백 함수의 반환 값이 모두 참이면 true 반환