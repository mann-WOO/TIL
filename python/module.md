# 모듈(module)

> 모듈: 특정 기능을 하는 코드를 담고 있는 파일(스크립트)
>
> 패키지는 모듈의 집합이다.
>
> 패키지는 라이브러리라고도 부른다.



## 모듈 사용법

> 패키지는 *폴더*, 모듈은 *.py 파일*, var/function/Class 는 .py 파일 안의 *코드*라고 생각할 수 있다.

#### `import module`

- 모듈을 불러오기
- `module.var` / `module.function()` / `module.Class` 로 사용

#### `from module import var, function, Class`

- 모듈에서 특정  변수 / 함수 / 클래스를 불러오기
- 불러온 항목에 따라 `var` / `function()` / `Class` 로 사용

#### `from module import *`

- 모듈 내의 모든 요소 불러오기
- `var` / `function()` / `Class` 모두 사용 가능

#### `from package import module`

- 패키지 내의 특정 모듈 불러오기
- `module.var` / `module.function()` / `module.Class` 로 사용

#### `from package.module import var, function, Class`

- 패키지 내에 존재하는 특정 모듈의 특정 변수 / 함수 / 클래스를 불러오기
- 불러온 항목에 따라 `var` / `function()` / `Class` 로 사용

