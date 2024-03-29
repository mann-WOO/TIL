# AJAX

> 비동기 자바스크립트와 XML (Asynchronous JavaScript and XML)

AJAX
Promise 객체
Axios

<br>

## 개요

### 새로고침

- JS를 이용하지 않고 HTML과 CSS만으로 웹 페이지를 구성할 때, 한 번의 요청으로 하나의 HTML 문서를 가져올 수 있다. CSS 등을 이용해 웹 페이지에 약간의 변화(hover 등)을 줄 수는 있지만, HTML 내부의 데이터 자체를 바꿀 수는 없다.
- JS를 사용하면 addEventListener를 이용해 웹 페이지 상에서 사용자가 특정 동작을 했을 때, 페이지 자체를 새로고침하지 않은 상태에서 HTML, CSS 요소에 변화를 줄 수 있다.
- 즉 addEventListener는 특정 동작으로 전체 페이지를 새로고침 하지 않고도 페이지에 변화를 줄 수 있다.  하지만 여전히 서버에 요청을 보내고 그 응답을 받아오기 위해서는 새로고침이 필요하다. 
- **ajax**를 이용하면 XML 문서(현재는 JSON)을 이용해 새로고침 없이도 서버와 통신할 수 있다. addEventListener에 ajax를 이용한다면, 특정 동작으로 1) 서버와 통신하고, 2) 그 결과를 반영해 사용자가 보고있는 HTML 문서를 수정할 수 있다.

### 비동기

- JS에는 동기적으로 작동하는 함수와 비동기적으로 작동하는 함수가 모두 존재한다.
- 동기적으로 작동하는 함수는 작업 흐름이 하나의 선으로 이어진다. A, B, C 세 가지 작업을 진행한다면, 어떤 순간에도 동시에 작업이 진행되는 일 없이 A 시작 - A 종료 - B 시작 - B 종료 - C 시작 - C 종료의 순서로 진행된다.
- 비동기적으로 작동하는 함수는 동시에 여러 작업을 진행할 수 있다. A가 비동기 함수라면, A 시작(Web API에서 작업 수행) - B 시작 / 끝 - C 시작 / 끝 - A 끝(B, C가 수행되는 동안 A도 처리되고 있었음)과 같은 순서로 작업을 진행할 수 있따.
  - *JS는 싱글스레드로 작업하기 때문에 물리적으로는 하나씩의 작업만 수행할 수 있지만, 실질적으로는 동시에 여러 작업이 이루어진다.(Concurrency model)

비동기 설명 - Event loop



정리

1. JS를 이용해 새로고침 없이 HTML 문서의 일부분을 수정할 수 있다.
2. AJAX 요청을 통해 새로고침 없이 서버와 데이터를 주고 받을 수 있다.(비동기적으로 일어난다. 왜? 서버에서의 응답을 기다려야 되니까!)
3. AJAX 요청을 통해, 새로고침 없이 서버와 데이터를 주고 받고, 이를 반영하여 HTML 문서를 수정할 수 있다.