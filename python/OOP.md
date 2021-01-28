# OOP

> 객체지향프로그래밍(Object Oriented Programming): 객체를 중심으로 한 프로그래밍
>
> 절차 지향 프로그래밍 / 객체 지향 프로그래밍은 하나의 **패러다임**이다.





## 객체(Object)

> Python의 **모든 것**은 **객체**다.
>
> 타입(type), 속성(attribute)와 조작법(method)을 가진다.

- `list`라는 클래스의 `student_names`가 있을 때, `studnet_names`라는 인스턴스는 당연히 객체이고(정확히는 `student_names`라는 변수 안에 있는 리스트 인스턴스가 객체이고, `student_names`는 그 인스턴스의 별명(변수)이다.), `list`라는 클래스 또한 객체이다. 클래스도 `type`이라는 타입을 가지고, class attribute를 가질 수 있고, class method 또한 가질 수 있다.

### type

> 객체가 어떤 클래스에서 생성되었는지 알려준다.

```
type(3)
out: int
type(3) is int 
out: True
type(3) == int
out: True
```

### attribute

> 객체가 가지고 있는 정보, 상태, 데이터를 뜻함.

```python
complex_num = 10+2j
print(complex_num.real, complex_num.imag)
out: 10.0 2.0
```

### method

> 특정 종류의 객체에서만 작동하는 함수.

```python
a = ['a', 'b', 'c']
print(a.pop(), a) # .pop()은 list 클래스의 객체에서 사용하는 method
out: 'c' ['a', 'b']
```





##  클래스(Class)

> 클래스의 이름은 파스칼 케이스(PascalCase)로 적는다.

```python
class ClassName():
    pass
```

- 위의 코드에서, `ClassName` 뒤의 괄호를 제거해도 작동하지만 이후 등장하는 상속 개념을 사용할 때 괄호를 사용하므로, 빈 괄호를 붙여 형태를 맞춰준다.
- 클래스 내부에는 **attribute**와 **method**를 정의할 수 있다.
- 클래스 내부에 클래스를 정의하는 것도 가능하다. 





## 인스턴스(Instance)

> 특정 클래스에 속하는 객체를 instance라고 한다.

```python
istance = ClassName()
print(type(instance))
out: ClassName
```





## 속성(Attribute)

### 인스턴스 속성(Instance Attribute)

> 특정 클래스의 인스턴스가 해당 인스턴스 안에 저장하고 있는 정보, 데이터, 상태 

```Python
class Student():
    def __init__(self, name, age):
        self.name = name
        self.age = age

s1 = Student('john', 17) # (1)인스턴스를 생성하고 (2)s1에 할당한다.
print(s1.name, s1.age)

out: 'john' 17
```

- 주로 생성자 메서드(`__init__(self, ...)`)에서 정의 해두고, 인스턴스를 생성할 때 값을 할당해준다.
- 인스턴스 생성 이후에도 `john.age = 15`와 같이 변경해 줄 수 있고,`s1.email = 'john@gmail.com'`처럼 클래스를 선언할 때 정의하지 않은 attribute를 추가해 줄 수도 있다.
- 하지만 하나의 클래스로 여러 개의 인스턴스를 생성해 사용한다면, attribute의 수와 종류는 `__init__()`으로 정의하고 통일시켜주는 것이 좋다.



### 클래스 속성(Class Attribute)

> 특정 클래스가 자체적으로 가지고있는 정보, 데이터, 상태

```Python
class Student():
    counter = 0
    
    def __init__(self, name, age):
        self.name = name
        self.age = age

s1 = Student('john', 17)        
print(Student.counter, s1.counter)

out: 0 0
```

- 위의 예에서, `s1.counter`의 경우, `s1`이라는 인스턴스가 `counter`라는 attribute를 가지고 있는지 확인 후, 가지고 있지 않기 때문에 클래스 내의 해당 attribute를 보여준다.



### 속성(attribute)의 위계

- 위의 예에서처럼, `instance.attirubte`를 실행하면 인스턴스 내의 attribute에 우선적으로 접근하고, 존재하지 않을 경우 클래스의 attribute에 접근한다. 즉 두 attribute 다른 위계를 가지고 있다.
  - "이름공간(namespace)가 다르다"고 말한다.
- 클래스 attribute와 인스턴스 attribute의 식별자가 같을 때를 생각하면 쉽다.
  - 만약 `Person.species = 'human'`이라는 클래스 attribute가 존재하는데, `john.species = 'god'`이라고 할당한다면, 클래스 attribute를 변경하는 것이 아니라, `john`에 `species`라는 인스턴스 어트리뷰트가 생성되는 것이다.



## 메서드(Method)

> 메서드 설계의 규칙
>
> 클래스 자체와 그 attribute에 접근해야 한다면 클래스 메서드로 정의한다.
>
> 클래스/인스턴스 attribute 모두에 접근할 필요가 없다면 스태틱 메서드로 정의한다.

### 인스턴스 메서드(Instance Method)

> 인스턴스를 이용해서 어떤 작업을 실행하고 싶다면, 인스턴스 메서드를 정의하고 사용한다.
>
> 클래스 내부에 정의되는 메서드의 기본값
>
> 인스턴스 메서드를 호출 시, 자동으로 인스턴스 자신인 `self`를 첫번째 인자로 받는다.

```python
class Student():
    counter = 0
    
    def __init__(self, name, age):
        self.name = name
        self.age = age
    
    def greeting(self):
        print(f'hi! my name is {self.name}')
        
    def cheer(self):
        self.greeting()
        print('Cheer up!')
        print(Student.counter)
        
s1 = Student('john', 15)
s1.cheer()

out: hi! my name is john
	 Cheer up!
	 0
```

- 정의 시, self로 인스턴스 자신을 사용한다.
- 클래스 내부에 이미 선언된 method를 재사용 할 수 있다. 
- instance method의 정의에서 다양한 attrribute를 사용하고 싶을때 class attribute 는 `ClassName.attribute`로, instance attribute는 `self.attribute`로 사용한다
- `self`를 자동으로 첫 번째 인자로 받기 때문에, `s1.greeting()`은 `Student.talk(s1)`과 같다.
- 인스턴스는 클래스 메서드와 스태틱 메서드에도 접근할 수 있지만, **실제 프로그래밍에서는 호출하지 않는다**. 인스턴스에서는 인스턴스 메서드만 작동시키도록 설계해야 한다.



### 클래스 메서드(Class Method)

> 클래스를 이용해서 어떤 작업을 실행하고 싶다면, 클래스 메서드를 정의하고 사용한다.

> 인스턴스를 이용해서도 클래스 메서드를 사용할 수 있지만. **하지 않는다.**

> @classmethod 아래에 작성하여 정의한다.
>
> 클래스 메서드를 호출 시, 자동으로 클래스 자신인 `cls`를 첫번째 인자로 받는다

```python
class Student():
    counter = 0
    
    def __init__(self):
        Student.counter += 1
    
    @classmethod
    def get_counter(cls):
        print(cls.counter)
        
s1 = Student()
s2 = Student()
Student.get_counter()

out: 2
```

- `cls`를 자동으로 첫 인자로 받기 때문에, `Student.get_counter`는 `Student.get_counter(Student)`와 같다.
- 클래스 자신을 인자로 사용하기 때문에, 클래스 변수에 접근해 변경하거나, 이를 이용한 작업을 수행하기 좋다.
- 클래스에서도 `Student.talk(s1)`처럼 인스턴스 매서드에 접근할 수 있지만, 인스턴스 메서드는 클래스로 사용하지 않는다.



### 스태틱 메서드(Static Method)

> 인스턴스 attribute와 클래스 attribute를 사용하지 않고 특정 작업을 수행하고 싶을 때 정의하고 사용한다.
>
> @staticmethod 아래에 작성하여 정의한다.
>
> 스태틱 메서드는 호출 시 `cls`, `self`와 같은 인자를 자동으로 받지 않는다.
>
 ```python
 class MyClass
 
     @staticmethod
     def static_method(arg):
         return arg
 ```



#### 생성자/소멸자 메서드, 매직메서드

> 모두 `__str__` 와 같이, 밑줄 두개로 시작하고 끝나는 메서드들이다. 특수한 역할을 수행한다. 기본적으로 **인스턴스 메서드**다.

```python
class Student():
    def __init__(self, name, age):
        self.name = name
        self.age = age
        print('생성')
        
    def __str__(self):
        return f'my name is {self.name}'
        
    def __del__(self):
    	print('삭제')

s1 = Student('john', 15)
print(s1)
del s1

out: 생성
	 my name is john
	 삭제
```

- **생성자 메서드**(`__init__()`)는 인스턴스를 생성할 때 호출되는 메서드이다. 인스턴스를 생성할 때는 생성자 메서드의 매개변수에 맞춰 인자를 넣어줘야한다.
- **소멸자 메서드**(`__del__()`)는 `del instance`로 인스턴스를 삭제할 때 호출되는 메서드이다.
- `__str__()`는 **매직메서드**의 일종으로, python의 내장함수 `print(instance)`를 실행했을 때 return할 내용을 설정한다. 이처럼 매직메서드는 특별한 역할들을 수행한다.



## 상속(Inheritence)

### 상속

> 기존에 존재하는 클래스를 재사용하여 다른 클래스를 정의하고 싶을 때 사용한다.

```python
# 사용법
class ChildClass(ParentClass):
    pass
```

- 부모 클래스의 모든 attribute, method가 자식 클래스에 상속된다.
- 상속받은 attribute와 method는 부모 클래스의 것이 그대로 복사되어 자식 클래스 내부에 존재한다. 매번 부모 클래스에 접근하는 방식은 아니다.
- 공통된 attribute나 method를 부모 클래스에 정의하고, 이를 바탕으로 다양한 자식 클래스를 만들수 있다.
- 상속의 단계는 더 늘어날 수 있다. ex) GrandParentClass -ParentClass - ChildClass 

상속 관계인 클래스들의 타입 판별

- `isinstance(instance, class)`

  - ```python
    isinstance(child1, ParentClass) #=> True
    isinstance(child1, ChildClass) #=> True
    ```

  - 부모 클래스를 입력해도 `True`를 return

- `type(instance)`

  - ```python
    type(child1) is ParentClass #=> False
    type(child1) is ChildClass #=> True
    ```

  - 정확한 해당 클래스를 return

### 메서드 오버라이딩(Method Overriding)

> 자식 클래스에서 부모 클래스의 메서드를 덮어쓰는(override) 것

```python
class ParentClass():
    @staticmethod
    def greeting():
        print('hi')

class ChildClass(ParentClass):
    @staticmethod
    def greeting():
        print('hello')
```

- 부모 클래스의 메서드를 자식클래스에서 같은 이름으로 재정의하면 덮어쓸 수 있다.

### super()

> 자식 클래스에서 메서드를 정의할 때, 부모 클래스의 메서드 중 하나를 사용하는 방법, 메서드 오버라이딩 시, 같은 이름의 메서드를 정의하면서 부모 메서드를 재활용하고 싶을 때 사용한다.

```python
class Rectangle:
    def __init__(self, length, width):
        self.length = length
        self.width = width
        
    def area(self):
        return self.length * self.width
    
class Square(Rectangle):
    def __init__(self, length):
        # 자식의 메서드 정의 안에서 부모의 메서드를 실행한다고 생각한다.
        # 인스턴스 메서드를 실행할 때는, self를 자동으로 받는다.
        # 따라서 나머지 매개변수에 해당하는 인자들을 채워준다.
        super().__init__(length, length)
        
s1 = Square(3)
s1.area() #=> 9
```

- 추후 사용하면서 배우고 익숙해지면 좋겠습니다. 아직은 조금 헷갈림



### 다중상속

> 두개 이상의 클래스를 상속받아 클래스를 생성하는 경우

```python
class child(Mom,Dad):
    pass
```

- 상속받은 두 클래스의 attribute와 method가 모두 복제되어 자식 클래스에 존재한다.
- 만약 부모 클래스에 중복된 attribute나 method가 존재한다면, 먼저 적힌 클래스(예시에서는 Mom)의 attribute나 method를 참조한다.
- 하지만, 일반적으로 **두 개 이상의 클래스를 상속받을 때는 attribute나 method를 중복하여 상속받지 않도록 설계**해야 한다.





### note

- 클래스에서 모듈을 사용할 때는 클래스 바깥 맨 위에서 호출하고 사용하는 것이 rule이다.

