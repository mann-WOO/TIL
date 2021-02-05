# Bootstrap

> CSS와 Javascript로 작성한 프론트엔드 프레임워크
>
> Bootstrap 공식 사이트의 docs를 참조

- bootstrap-reboot.css: 브라우저의 css설정을 초기화시키는 코드



## Bootstrap의 사용

> 기능 단위별 class를 이용한다.

- bootstrap의 css , js 파일을 불러와 사용하기 때문에, 필요한 클래스를 태그에 추가하는 작업을 반복한다.



## cf) Content Delivery(Distribution) Network

> 세계 각지의 외부 서버를 이용해 CSS, JS 등을 사용할 수 있게 해주는 네트워크

- 부트스트랩 파일을 첨부하지 않고, 코드의 링크를 통해 부트스트랩을 사용할 수 있다.



## cf) Responsive Web Design

> 다양한 화면 크기에 반응하는 웹 디자인 방식: 웹 접근 디바이스의 다양화에 대응



## Grid System

> Bootstrap의 Grid System: 12 column, 6 tiers of grid option

- 12 columns: 적당히 작은 수 중 많은 **약수**(1,2,3,4,6,12)를 가져 다양한 레이아웃을 구성
  - nested grid도 12 columns로 구성되어 있다.
  - 5개의 항목을 작성하고 싶을 때는 양끝의 하나씩을 비우고 사용할 수 있다.
  - 보통 3~5개의 항목으로 구성한다.
- 6 tiers of grid option: 반응형 계층 breakpoint - 6가지 구간의 화면 크기에 따라 다른 구성이 보이도록 설정 가능
- **CSS의 grid와는 다르다** => Bootstrap의 grid system은 flexible box를 기반으로 한다.



## container

> bootstrap으로 코드를 짤 때, 대부분의 경우 container 안에 넣어준다. menu, footer 등 제외.

- 양쪽에 여백을 줘서 보기 편하게 해준다.



#### cf)html에서 케밥케이스(kebab-case)를 사용하는 이유

- 하이퍼링크 등이 밑줄 처리 되기 때문에 언더바가 보이지 않는다.
- 대소문자 구분이 안되는 경우가 있다.



## Bootstrap 기능

### navbar

- 기본적으로 상단에 고정(fixed-top) 되는 네비게이션 바를 생성
- 드롭다운 메뉴, 토글(햄버거) 메뉴 등 반응형으로 사용할 수 있다.
  - 토글 메뉴 사용시 components-collapse 참조

### modal

- 현재 페이지를 유지한 채 추가적인 창(로그인 등)을 띄우고 싶을 때 사용
- modal을 구현한 후, 버튼/하이퍼링크 등과 연동하여 사용

### carousel

- 여러 이미지를 바꿔가며 보여준다.
  - 자동으로 넘기는 기능과, 화살표 및 인덱스를 추가하는 기능이 있다.

