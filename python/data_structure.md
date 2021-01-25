# Data Structure

> 데이터에 접근, 조작, 변경: method



## 문자열(String)

> immutable, ordered, iterable
>
> **문자열은 immutable하기 때문에, method를 적용했을 때, 변화가 적용된 새로운 string을 return한다.**



### `.find(x)`

- ```python
  m = 'mann'
  m.find('n')
  
  out: 2
  ```

- x의 첫 번째 위치를 반환

- 없으면 -1을 반환s

### `index(x)`

- x의 첫번째 위치를 반환
- 없으면 `error`

### `.replace(old, new[, count])`

- ```python
  k = 'kkkkorea'
  k.replace('k', '')
  out:'orea'
  k.replace('k', '', 3)
  out:'korea'
  ```

- 기존 글자를 새로운 글자로 바꿔서 새로운 스트링을 반환

- count를 지정하면 해당 갯수만큼 시행

### `.strip([chars])`

- ```python
  `  mann  `.strip()
  out:`mann`
  'mann'.strip('nn'):
  out:'ma'
  ```

- 문자를 지정하지 않으면 양쪽 공백을 제거

- `.lstrip()`, `.rstrip()`를 이용하면 왼쪽 혹은 오른쪽을 선택 가능

- 문자열을 지정하면 지정한 문자열을 양쪽 끝에서 제거

### `.split()`

- 문자열을 특정 문자를 기준으로 나누어 리스트로 반환
- 문자를 지정하지 않으면 공백을 기준으로 나누어 리스트로 반환

### `'seperator'.join(iterable)`

- 반복 가능한 컨테이너의 요소들을 구분자로 합쳐 문자열로 반환

- ```python
  '?'.join('mann')
  out:'m?a?n?n'
  '?'.join([mann, woo])
  out:'mann?woo'
  ```

### etc

- `.capitalize()`
- `.title()`
- `.upper()`
- `.lower()`
- `.swapcase()`
- ...https://docs.python.org/ko/3/library/stdtypes.html#string-methods





## 리스트(list)

>mutable, ordered, iterable
>
>**리스트는 mutable하기 때문에, method를 적용했을 때, 바로 해당 리스트가 변경된다.**



### `.append(x)`

- 리스트에 `x`라는 원소를 추가

### `.extend(iterable)`

- 리스트에 iterable(list, tuple, range, string)의 요소들을 추가.
  - 문자열을 넣는다면, 요소별로 처리하기 때문에 한 글자씩 들어감

### `.insert(i, x)`

- 위치 `i`에 `x`를 추가 
- `i`가 리스트 전체 길이를 넘어간다면 마지막에 아이템이 추가됨

### `.remove(x)`

- 리스트에서 값이 `x`인 것을 삭제(앞의 것부터 하나씩)
- 값이 `x`인 아이템이 없다면  `error`

### `.pop(i)`

- 위치 `i`에 있는 아이템을 삭제하고, 그 아이템을 반환한다.
- `i`를 지정하지 않으면 마지막 항목을 삭제하고 반환.

### `.sort()`

- 리스트를 오름차순으로 정렬
  - `sorted(x)`는 정렬된 리스트를 반환하는 반면, .sort()는 해당 리스트 자체를 정렬시키고, None을 반환

### 리스트 복사법

- 슬라이싱(`[:]`)이용
- `list()`로 리스트를 리스트로 형변환

### list comprehension

```python
numbers = range(1, 11)

# 반복문
new_list = []
for num in numbers:
    new_list.append(num * 2)

# list comprehension
list(num * 2 for num in numbers)

# 1~10 중 짝수
[i for i in range(1, 11) if i % 2 == 0]
```



## 데이터 구조에 적용 가능한 Built-in Function

> 순호회 가능한(iterable) 데이터 구조에 적용 가능한 Built-in Function
>
> `map()`, `filter()`, `zip()`



### map(function, iterable)

> function에는 ()를 적어주지 않는다.

- ```python
  a = ['1', '2', '3']
  
  # 단순 반복
  b = []
  for i in a:
      b.append(int(i))
     
  # 리스트 컴프리핸션
  c = [int(i) for i in a]
  
  # map
  # interable의 모든 원소를 function의 인자로 사용
  d = list(map(int, a)) # a의 각 원소마다 int 함수를 적용
  
  #####
  a = input()
  b = map(int, a.split())
  # 위와 같은 형태로 많이 쓴다
  ```

  - #### lambda

### filter(function, interable)

> filter이기 때문에, function의 return은 True or False이어야 한다.

- ```python
  def odd(n):
      return n % 2
  
  a = [1, 2, 3, 4, 5]
  b = list(filter(odd, a))
  print(b)
  ```

### zip(*iterables)

- ```python
  alphabets = ['a', 'b', 'c']
  numbers = [1, 2, 3]
  pair = zip(alphabets, numbers)
  
  print(list(pairs))
  ```

- 복수의  iterable 객체를 모아준다.

- 튜플의 모음으로 구성된 `zip object`를 반환





## 세트(Set)

> mutable, unordered, iterable

### `.add(elem)`

- elem을 세트에 추가

### `.update(iterable)`

- 인자에 여러가지 값을 추가
- 반드시 iterable 데이터 구조를 입력받음

### `.remove(elem)`

- elem을 세트에서 삭제
- elem이 세트 내에 없을 때는 KeyError 발생

### `.discard(elem)`

- elem을 세트에서 삭제
- elem이 세트 내에 없어도 에러 발생하지 않음

### `.pop()`

- 임의의 원소 하나를 제거하고, 해당 원소를 반환





## 딕셔너리(Dictionary)

> mutable, unordered, iterable
>
> `key: value` pairs



### `.get(key[, default])`

- key를 통해 value를 가져옴. 해당 value를 반환
- KeyError 발생하지 않음. 
- 조회한 key가 존재하지 않을 경우 default를 반환. default의 기본값은 None

### `.pop(key[, value])`

- 딕셔너리에서 key: value 쌍을 제거하고 value를 반환
- 존재하지 않는 key를 조회시 default를 입력하면 default 반환, 입력하지 않으면 KeyError 발생

### `.update(dict)`

- 제공되는 key: value를 딕셔너리에 추가
- 이미 존재하는 key: value라면 덮어씀

### 딕셔너리 순회

> `for` 반복문을 사용할 때

- 반복문 사용시, 딕셔너리를 순회하면 key를 조회

- `.keys()`를 활용시 key들을 조회

  -  기본적인 딕셔너리 순회와 같지만, `.keys()`를 적어서 순회하는 것이 더 바람직하다.

- `.values()`를 활용시 value들을 조회

- `items()`를 활용시 key: value 쌍들을 tuple 형태로 조회

  - ```python
    for k, v in real_dict.items():
        print(k, v)
    ```

### Dictionary comprehension

- ```python
  b = [('jane', 2), ('kate', 3), ('steve', 4)]
  print({str(k): v for k, v in b})
  out: {'jane': 2, 'kate': 3, 'steve': 4}
  ```



