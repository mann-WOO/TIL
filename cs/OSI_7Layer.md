# OSI 모형

> Open Systems Interconnection *Reference Model*: 네트워크 통신을 위한 기본 참조 모델(참조 목적이지만, 따르지 않을 경우 네트워크 통신이 어려울 수 있음)

### OSI 7계층

7계층(Application Layer): 전송하고자 하는 내용, 어플리케이션

- 사용자에게서 데이터를 입력받거나, 최종적으로 전달하는 역할 수행

6계층(Presentation Layer): 암호화, 압축, 인코딩 등 표현방식에 대한 규칙

- 인코딩, 암호화, 압축

5계층(Session Layer): 연결 - 회선의 생성, 유지, 종료에 대한 규칙

- TCP/IP 세션을 만들고 없앤다.

4계층(Transport Layer): 누가 보내서 누가 받는지(From/To) - port number + TCP/UDP의 결정(TCP:송신자 책임/ UDP:수신자 책임)

- 유효성을 제어한다.
- 상태개념이 있고, 연결 기반이다 -> 전송에 실패했을 때 재전송한다.

3계층(Network Layer): 목적지까지의 경로 설정과 도착지 주소(IP: Internet Protocol)

- 4계층/ 3계층(TCP/IP)는 운영체제 내부에 구현된다.
- 대표적인 장치로 라우터가 있다.

2계층(Data Link Layer): 도착지의 상세 주소, MAC(Media Access Control)

- 디지털 신호처리, 통신트래픽 제어 등의 기능이 논리회로로 구현된다.
- 1계층과 함께 칩 하드웨어로 구현된다.
- MAC address: 00:1A:2B:3C:4D:5E 형태로 이루어짐

1계층(Physical Layer): 디지털 신호를 전기 신호로 전송하는 규칙

- 전압, 전선의 명세
- 허브가 물리 계층의 장치임

<br>

### Encapsulation / Decapsulation

Encapsulation: 보내는 과정 (7->1 Layer)

Decapsulation: 받는 과정 (1->7 Layer)



참고자료

https://www.youtube.com/watch?v=aTPy201F0AA