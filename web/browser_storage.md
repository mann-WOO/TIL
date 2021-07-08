# Cookie / Web Storage

Cookie / Web Storage(Local Storage / Session Storage)

<br>

## 개요

- Web 서비스 사용자는 브라우저를 통해 특정 도메인의 서비스를 이용한다. 브라우저는 요청에 대한 응답으로 받은 HTML, CSS, JavaScript 문서를 해석하고 실행한다.
- 하지만 브라우저가 단순히 문서를 보여주는 역할만 수행하지는 않는다. 브라우저는 사용자가 특정 도메인의 서비스를 더 효율적으로 이용할 수 있도록 다양한 정보를 저장한다. 이러한 저장소로 Cookie와 Web Storage가 있다.

<br>

## Cookie

> Cookie는 문자열 데이터만 저장할 수 있다.

- 도메인 별로 존재
- 서버에 요청 시 저장된 쿠키를 함께 전송
- HTTP 프로토콜의 무상태성(stateless)에서 상태 정보를 기억시켜 준다.
- 주 목적 세 가지
  - 세션 관리(로그인, 장바구니, 게임 스코어)
  - 개인화(사용자 선호, 테마 등의 세팅)
  - 트래킹(사용자 행동 기록 및 분석)

<br>

## Web Storage

> Web Storage에는 문자열 외에도 구조화된 객체를 저장할 수 있으며, 지속성에 따라 Local Storage와 Session Storage로 구분된다.

### Local Storage

- 영구저장소
- 도메인 별로 존재
- 브라우저를 닫았다 열어도 데이터가 남아있다.
- 유효기간 없이 데이터를 저장하며 JavaScript를 사용하거나 브라우저에서 직접 로컬 스토리지를 지워주지 않는 한 계속 유지된다.
- 저장 공간이 가장 크다.

### Session Storage

- 임시저장소
- 도메인 별로 존재
- 브라우저, 또는 탭이 닫힐 때 까지만 데이터를 저장한다. -> 같은 사이트의 같은 도메인이라도, 브라우저가 다르면 서로 다른 영역으로 Session Storage가 존재한다.
- 데이터를 절대 서버로 전송하지 않는다.
- 저장 공간이 쿠키보다 크다.

<br>

참고자료

- https://developer.mozilla.org/ko/docs/Web/HTTP/Cookies

- https://developer.mozilla.org/ko/docs/Web/API/Web_Storage_API
- https://velog.io/@design0728/%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80-%EC%A0%80%EC%9E%A5%EC%86%8C-LocalStorage-SessionStorage-Cookie
- https://velog.io/@gay0ung/%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80-%EC%A0%80%EC%9E%A5%EC%86%8C



