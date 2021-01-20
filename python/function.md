# 함수(function)

---

```python
def function(para1, para2):
    # code block
    return value
```



## 함수의 Output

### return

- 함수의 결과값
- 함수 내에 `return`이 없는 경우 `None`을 return
  - print() 함수는 결과값을 보여주지만, `None`을 return한다.
- `return x, y`처럼 2개 이상의 값을 return하면 tuple로 묶여 하나의 값으로 반환된다.



## 함수의 Input

### 매개변수(parameter)

- `def function(x)`에서 x를 매개변수라고 한다.
  - 함수 내에서 활용할 변수
  - 함수의 정의 부분에서 쓰임

### 인자(argument)

- `my_result = function(3)` 에서 3을 인자라고 한다.

  - 함수에 전달되는 입력값
  - 함수 호출 부분에서 쓰임

- 함수를 정의할 때 `def function(para1=value1)`의 형태로 **기본 인자 값**을 정할 수 있다.

  - 함수 호출 시 para1의 인자 값을 입력하지 않으면, value1을 인자로 사용한다.
  - 기본 인자 값이 없는데 인자 값을 입력하지 않으면 **Error** 발생
  - <u>기본 인자 값을 가지는 매개변수 다음에 기본 인자 값이 없는 매개변수를 사용할 수 없다.</u>
    - `def function(para1=arg1, para2)`는 **잘못된 함수**
    - 이는 인자의 순서를 파악할 수 없기 때문이다.
    - 옳은 방법: `def funtion(para1, para2=arg2)`

- **위치 인자**와 **키워드 인자**

  - *매개변수의 순서대로* 써주면 **위치 인자**, *직접 매개변수를 지정*해주면 **키워드 인자**
  - 위치 인자 사용법:`function(1, 2, 3, 'me')`
  - 키워드 인자 사용법: `function(para1=1, para3=3, para2=2, name='me')`
    - 순서를 무시해도 된다
    - <u>하지만, 키워드 인자를 사용한 다음에 위치 인자를 사용할 수 없다.</u>

- 가변(임의) 인자 리스트

  - 입력될 인자의 개수를 알 수 없을 때 사용한다.

    - ```python
      def greeting(*names):
          return(args)
      
      greeting('철수', '영희', '미애')
      ```

    - 위의 코드는 `('철수', '영희', '미애')`의 tuple을 return한다.

    - 가변인자 사용 이후에 인자가 더 있다면, 키워드를 입력해 가변인자 입력이 끝났음을 알 수 있게 한다.

      - ```python
        def greeting(*names,age):
            retunr args, age
           
        greeting('철수', '영희', '미애', age=25)
        ```

- **가변 키워드 인자**

  - 함수 정의 시, parameter의 수와 함께 키워드도 정해지지 않을 때 사용

  - 딕셔너리 형태로 return된다.

  - ```python
    # 정의
    def my_dict(**kwargs):
        return kwargs
    
    # 사용
    my_dict(location='서울', gear='노트북', place='카페')
    
    # 결과
    {'location': '서울', 'gear': '노트북', 'place': '카페'}
    ```




## 스코프(scope)

> 함수를 정의하면 스코프가 생성된다. 스코프 내에서 선언한 변수는 스코프 내에서만 유효하다.
>
> Python에서는 함수 안에서만 스코프가 생성되고, 루프 안에서 스코프가 생성되는 언어도 있다.

### 스코프의 우선순위(LEGB)

- Local scope:  정의된 함수
- Encloser scope: 상위 함수
- Global scope: 전역(함수 밖, import 된 모듈)
- Built-in scope: 파이썬 내장 함수 혹은 속성

### 스코프의 수명주기

- local scope: 함수가 호출될 때 생성, 함수가 종료되면 삭제
- global scope: 변수의 선언/모듈의 호출 시 생성, 인터프리터 종료되면 삭제
- built-in scope: 파이썬 실행과 동시에 생성, 계속 유지



## 재귀함수(recursive function)

>함수 내부에서 자기 자신을 호출 하는 함수

> function(n)을 funtion(n-1)에 대한 식으로 표현할 수 있다면 재귀로 표현 가능?

### RecursionError

- 파이썬에서는 최대 재귀 깊이를 1000으로 정해, 1000번 이상 재귀가 일어나는 코드는 Error가 발생한다.

### 재귀가능성

- 재귀가 불가능한 경우도 있다. 그리고 재귀가 시간적으로 빠르다고 볼 수도 없다.
- 상황에 맞게 사용하는 것이 중요하다.



