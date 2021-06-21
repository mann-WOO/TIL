# https

> Hypertext Transfer Protocol Secure

<br>

## 개요

### http vs https

http는 서버와 클라이언트가 데이터를 주고 받는 통신규약이다. https는 주고받는 데이터를 암호화(encrypted)하여 데이터 통신의 보안성을 높인다.

<br>

### https가 필요한 이유

1. 개인정보보호(Privacy)

- 데이터를 암호화하지 않고 통신할 경우, 제 3자가 그 내용을 엿듣고 악의적으로 사용할 수 있다. (ex. 비밀번호, 주민등록번호, 카드번호 등)
- https는 암호화된 데이터를 송·수신하기 때문에 제 3자가 그 내용을 알 수 없다.

2. 데이터의 완전성(Integrity)

- http 통신은 서버와 클라이언트의 데이터 통신에서 데이터가  온전한 상태로 상대에게 도착하는지 확신할 수 없다.(통신 과정에서 제 3자에 의해 조작될 수 있다.)
- https는 서버와 클라이언트의 데이터 통신 과정에서 제 3자에 의한 데이터 조작을 막을 수 있다.

3. 신원 증명(Identification)

- https는 외부 기관에서 발급된 증명서(certificate)을 통해 서버와 클라이언트의 신원을 증명한다.
- 사용자는 현재 사용하고 있는 웹이 사용자가 방문하고자 하는 웹이 맞다는 것(해당 웹처럼 보이게 만들어진 가짜 웹이 아님)을 확신하게 해주고, 서버는 사용자가 보낸 데이터가 해당 사용자가 보낸 것임을 확인할 수 있게 해준다.

<br>

#### https를 사용하는 또다른 이유

- https를 이용하면 구글의 SEO(검색엔진최적화)에서 더 높은 점수를 받을 수 있다.
- aws등을 통해 배포한 웹 서비스에 DNS를 적용하기 위해서는 https 통신을 사용해야 한다. (cf. DNS over HTTPS) 

<br>

참고자료

- https://howhttps.works/why-do-we-need-https/
- http://blog.wishket.com/http-vs-https-%EC%B0%A8%EC%9D%B4-%EC%95%8C%EB%A9%B4-%EC%82%AC%EC%9D%B4%ED%8A%B8%EC%9D%98-%EB%A0%88%EB%B2%A8%EC%9D%B4-%EB%B3%B4%EC%9D%B8%EB%8B%A4/
- https://blog.naver.com/skinfosec2000/222135874222