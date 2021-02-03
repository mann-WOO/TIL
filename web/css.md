# CSS

> Cascading Style Sheet: 스타일, 레이아웃 등을 통해 HTML을 표시하는 방법을 지정



## CSS 정의 방법

1. 인라인(inline): html 태그의 `style` 속성에 CSS 코드를 넣기
2. 내부 참조(embedding): head 태그 내에  `<style>` 태그를 지정하고 그 안에 코드 넣기
3. **외부 참조**: 외부 CSS 파일을 `<head>` 내 `<link>`를 통해 불러오기



## CSS 기본 구조



### 선택자(selector)

- 전체 선택자

- 요소 선택자

- 클래스 선택자

  - 마침표(.)로 시작한다.

- id 선택자

  - \# 문자로 시작한다.
  - 한 id는 문서당 한 번만 사용할 수 있고, 요소에는 단일 id 값만 적용할 수 있다.

  

## CSS 적용 우선순위(cascading order)

### 1. 중요도

- !important: 알고만 있고, 사용하지는 않는다.

### 2. 우선 순위(Specificity)

- 인라인 / id 선택자 / class 선택자 / 요소 선택자
  - 코드 량이 늘어나면 우선 순위가 복잡해지기 때문에, 가급적 class 선택자를 우선적으로 이용한다.

### 3. 소스 코드 순서



## CSS 상속

> CSS는 상속을 통해 부모 요소의 속성을 자식에게 상속한다.

- property 중에는 상속이 되는 것과 되지 않는 것이 있음.
- 상속 되는 것: text 관련 요소(폰트, 색상, 정렬). opacity, visibiliy
- 상속 되지 않는 것:
  - Box model 관련 요소
  - position  관련 요소



## CSS 단위

### 상대 크기 단위

- px(픽셀): 사용하는 화면의 해상도가 다양해지면서, 잘 사용하지 않게 되었다.
- %
- em: 배수 단위, 요소에 지정된 사이즈에 상대적인 사이즈를 가짐
- rem: 최상위 요소(html)의 사이즈(16px)를 기준으로 배수 단위를 가짐
- **Viewport** 기준 단위: vw, vh, vmin, vmax => **주로 사용하게 될 단위**

### 색상 단위

1. 색상 키워드
2. RGB 색상
   - '#' + 16진수 표기법
   - rgb() 함수형 표기법
3. HSL 색상
   - 색상, 채도, 명도



## CSS Box model

> CSS의 모든 것은 박스(네모)로 이루어져 있다.

### Box model 구성

> shorthand(ex_`1px solid black`)로 쓸 수 있다.

- Margin
- Border
- Padding
- Content



## CSS 레이아웃 테크닉

> CSS를 이용해 웹의 레이아웃을 설정하는 테크닉

- display: inline, blcok...
- position: static, relative, absolute, fix, sticky 
- float
- **flexbox**
- grid



## CSS Display

### display

- display: block
  - div, p, form 등
- dsplay: inline
  - span 등
- display: inline-block
- disply: none
  - 온오프 기능으로 사용하는 경우가 많다: 스크롤을 내리면 사라지는 블럭 등



## CSS Position

### static

- 기본값. 왼쪽 위부터 차례대로 쌓아지는 위치

### relative

- static의 위치를 기준으로 이동시키는 값. 
- 본래의 위치를 차지하지 않음. 즉 다음 블럭이 앞으로 당겨져서 자리를 차지함.
- `<right: 100px;>`은 static 위치에서 오른쪽에 100 픽셀의 여유를 둔다. 곧 왼쪽으로 100 픽셀 이동

### absolute

- 부모의 위치를 기준으로 이동시키는 값.
- 본래의 위치를 차지하고 있음. 이동시키더라도 본래의 위치는 공백으로 유지됨.

### fixed

- 스크롤을 움직여도 사용자의 화면(viewport)에 고정되어 있음.



## float

> 박스를 글씨와 어울리게 하는 기능, `float: left`로 설정

- float을 적용하면 `position: absolute`와 같이 자신의 자리를 잃어버린다.
- 따라서 float 박스 다음에 float이 아닌 박스가 오면 겹치게 된다.

### clearfix::after

> float 박스를 다른 박스가 침범하지 못하도록, 가상의 블럭을 설정



## flexbox

> container 안에 여러가지 내용물이 들어있는 형태. 왼쪽에서 오른쪽으로 컨테이너를 꽉 채워 줄을 바꾸지 않고 정렬되는 것을 기본값으로 가진다.

### flexbox control

> flexbox의 정렬 등은 container 태그에서 이루어진다.
>
> 정렬은 `justify-content`, `align-items`으로 대부분의 경우 해결 가능하다.

- `display: flex`: flexbox로 설정
- `flex-direction: row(-reverse), column(-reverse)`: flexbox의 메인축 방향 설정
- `flex-wrap: nowrap(default), wrap(-reverse):`: 줄바꿈 여부 설정
- `justify-content: flex-start, flex-end, center, space-between, space-round, space-evenly`: 메인축 방향의 정렬 방식 설정
- `align-items`: <u>줄바꿈이 일어나지 않았을 때</u> 교차축 방향의 정렬 방식 설정
- `align-content`: <u>줄바꿈이 일어났을 때 때</u> 교차축 방향의 정렬 방식 설정
- `align-self`: <u>felxbox의 아이템 태그에서 설정</u>, 교차축 방향의 정렬 방식
- `order`: <u>flexbox의 아이템 태그에서 설정</u>, 0을 기본값으로 순서를 설정



## CSS 코딩 tip

> CSS는 기능별로(사이즈, 바탕색, 글색, 글꼴, 테두리 등등) 클래스를 구성하고, 그 기능이 필요한 태그에 기능에 해당하는 클래스들을 부여하여 재사용 유지보수에 용이하도록 한다. -> bootstrap 등의 framework 이용방식