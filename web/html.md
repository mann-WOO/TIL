# HTML

>Hyper Text Markup Language: 한 방향으로만 읽는 책이 아닌, 링크를 통해 순서 없이 접근할 수 있는 텍스트를 적는 언어.

## HTML

### Markup language

- 태그를 이용해 문서/데이터의 구조를 명시한다.
- 계산이나 저장이 이루어지지는 않는다.(일반적인 프로그래밍 언어와의 차이점)
- `<태그이름 속성="속성값">내용</태그이름>` 구조로 적을 수 있다.\
  - 이 구조만 알고 있다면, 태그와 속성은 검색해서 사용하면 된다.



## HTML의 기본구조

> DOM(Document Object Model) 트리: html은 태그들 간에 부모와 자식 관계를 가진다.
> => 들여쓰기로 구분한다.

> VSCode에서 `!`를 입력하면 기본 틀이 생성된다. 

### head

> 사용자에게는 보이지 않는 부분

#### - Open Graph

-  `<meta property="og.title" content="제목" />`과 같은 형태로 작성
- 카카오톡에서 링크를 보내면 보이는 웹사이트의 개략을 볼 수 있는 부분

### body

> 사용자에게 보여지는 부분

### 요소(element)

- ```<h1>contents</h1>```: HTML의 요소는 태그와 내용으로 이루어져있다.

### 속성(attribute)

- `<a href="https://google.com"></a>`
- 태그에 속성을 부여할 수 있다.

### 시맨틱 태그

> HTML5에서 의미론적 요소를 담은 태그의 등장
>
> 시맨틱 태그는 div와 완전히 동일하게 작동한다. 하지만 그 구역에 명확히 의미를 부여한다. 코드의 가독성을 높이고, 유지보수에 편리하다. 

- header, h1, strong 등
- non-semantic: div, spantag

### 블럭 vs 인라인

- 모든 태그는 박스다.
- `<span>contents</span>`
  - span은 인라인이라는 속성을 가지고 있다.
  - 컨텐츠의 내용만큼만 공간을 차지한다. 줄바꿈이 일어나지 않는다.

### 태그들

- `<li>`: 그룹으로 리스트를 작성
  - `<li>`태그들을 `<ol>`로 감싸면 숫자로 리스트화됨. `<ul>`은 점으로 표시
- `<a href="url">`: a는 anchor, href는 hypertext reference. 하이퍼링크를 이용하고 싶을 때 사용
- `<form>`: 데이터를 전송하기 위해 만들어진 태그
  - tags
    - action: href와 같은 역할을 한다. 입력받은 내용을 어디로 보낼 것인지 주소설정
- `<input>`: 데이터를 입력받기 위한 태그
  - 닫는 태그가 없다: 개발자가 컨텐츠를 작성할 필요가 없기 때문에.
  - tags
    - type: 입력받을 내용의 형태



### 참조 문서 및 툴

- Mozila Developers Network: 웹에 대한 첫 번째 참조 문서. 키워드 + mdn으로 검색.
- w3c school: reference의 HTML Tags를 자주 찾아보고 참조.
- https://jsfiddle.net/: web 소스코드를 작성하고 공유할 수 있다.