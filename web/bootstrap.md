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

