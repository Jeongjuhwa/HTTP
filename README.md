# HTTP

## IP(인터넷 프로토콜) 역할  
* 지정한 IP주소에 데이터 전달  
* 패킷이라는 통신 단위로 데이터 전달  

## IP(인터넷 프로토콜)의 한계  
* 비연결성(클라이언트와 서버)  
* 비신뢰성(패킷 도착순서나 중간에 노드가 끊어져 있을 경우)  
* 프로그램 구분(여러가지 애플리케이션일 경우) -> port할당  

## IP의 한계 해결 -> TCP(전송 제어 프로토콜)  
* 연결지향 - TCP 3 way handshake  
* 데이터 전달 보증  
* 순서 보장  
### 3 way handshake  
1. 클라이언트에서 서버로 SYN 보냄  
2. 서버가 받으면 다시 클라이언트로 SYN+ACK 보냄  
3. 클라이언트가 받으면 또 서버에 ACK보냄  
* ACK는 대답같은 느낌 -> 요즘은 클라이언트가 ACK보낼때 데이터도 같이 전송  

### 데이터 전달 보장  
* 클라이언트가 데이터 전송하면 서버에서 잘 받았다고 응답 줌  

### 순서 보장  
* 패킷이 보낸 순서와 도착 순서가 다른 경우 다른지점 패킷부터 서버가 클라이언트에게 다시 보내라고 요청  

## UDP  
* 거의 기능 없음  
* IP에 포트랑 체크섬 정도만 추가  
* 필요한 기능 애플리케이션에서 추가해서 사용하면 됨  
* 데이터 전달, 순서가 보장 안되지만 단순하고 빠름  

## PORT  
* 같은 IP내에서 프로세스 구분  

## TCP/IP 패킷정보에는 출발지 IP, PORT, 목적자 IP, PORT, 전송데이터 등등이 포함됨  

## DNS(Domain Name System)  
* 전화번호부 느낌  
* 도메인 명을 IP주소로 변환  
* 예를들면 DNS에 도메인명:aaa.com IP: 200.200.200.2 이렇게 저장하면 클라이언트는 도메인명으로 IP를 찾고 IP가 변경되도 도메인명으로 검색하기 때문에 상관 없음  


## URI, URL, URN  
* URL - Locator: 리소스가 있는 위치를 지정  
* URN - Name: 리소스에 이름 부여  
* 위치는 변해도 이름은 안변함  
* URN으로 실제 리소스 찾는 방법은 보편화 안됨  
* URI = URL 같은 의미라 봐도 될듯  

## URL 전체문법  

#### scheme://[userinfo@]host[:port][/path][?query][#fragment]  
#### https://www.google.com:443/search?q=hello&hl=ko  
* 프로토콜(https)  
* 호스트명(www.google.com)  
* 포트번호(443)  
* 패스(/search)  
* 쿼리 파라미터(q=hello&hl=ko)  
* port는 일반적으로 생략(http는 80 https는 443  

## HTTP 메시지 전송  
1. 웹 브라우저가 HTTP 메시지 생성  
  * HTTP요청 메시지EX) GET /search?q=hello&hl=ko HTTP/1.1 (공백) Host: www.google.com  
2. SOCKET 라이브러리를 통해 전달  
3. TCP/IP패킷 생성, HTTP메시지 포함  

## HTTP의 특징  
* 클라이언트 서버 구조  
* Stateful, Stateless  
* 비 연결성  
* HTTP 메시지  
* 단순함, 확장가능  

##### 사실상 HTTP메시지에 모든 것을 전송(HTML, TEXT, IMAGE, 영상, 파일, JSON, XML. 거의 모든 형태의 데이터)  

## 클라이언트 서버 구조  
* Request, Response 구조  
* 클라이언트는 서버에 요청을 보내고, 응답을 대기  
* 서버가 요청에 대한 결과를 만들어서 응답해줌  

## 무상태 프로토콜(Stateless)  
* 서버가 클라이언트의 상태를 보존 안함  
* 장점: 서버 확장성 높음  
* 단점: 클라이언트가 추가 데이터 전송해야 함  

## Stateful, Stateless  

#### Stateful EX  
* 고객: 이 노트북은 얼마인가요?  
* 점원: 100만원 입니다.
* 고객: 2개 구매하겠습니다  
* 점원: 200만원 입니다.  

#### Stateless EX  
* 고객: 이 노트북 얼마인가요?  
* 점원A: 100만원 입니다.  
* 고객: 2개 구매하겠습니다.  
* 점원B: ?무엇을 2개 구매하시겠어요?  

#### Stateless 사용 EX  
* 고객: 이 노트북 얼마인가요?  
* 점원A: 100만원 입니다.  
* 고객: 노트북 2개 구매하겠습니다.  
* 점원B: 노트북 2개는 200만원 입니다.  

## Stateful, Stateless의 차이  
* 상태 유지: 중간에 다름 점원으로 바뀌면 안됨  
* 무상태: 중간에 다른 점원으로 바뀌어도 됨  
* 무상태는 응답 서버를 쉽게 바꿀 수 있음 -> 무한한 서버 증설 가능  
* Stateful은 항상 같은 서버가 유지 되어야하는데 만약 서버 장애나면 망함  
* Stateless는 아무 서버나 호출 가능 -> GOOD  

## Stateless 실무 한계  
* 무상태로 설계 할 수 있는 경우도 있고 없는 경우도 있음 -> 그래도 최대한 무상태로 설계가 좋음  
* 무상태 EX) 로그인이 필요 없는 단순 서비스 소개 화면  
* 상태유지 EX) 로그인  
* 로그인한 사용자의 경우는 로그인 했다는 상태를 서버에 유지해야함(쿠키와 세션)  

## 비 연결성  
* HTTP는 기본적으로 연결을 유지하지 않는 모델  
* 일반적으로 초 단위 이하의 빠른 속도로 응답  
* 1시간 동안 수천명이 서비스를 사용해도 실제 서버에서 동시에 처리하는 요청은 수십개 이하  
* 서버 자원을 효율적으로 사용 할 수 있음  

## 비 연결성 한계와 극복  
* TCP/IP 연결을 계속 새로 맺어야 함 - 3 way handshake 시간  
* 웹 브라우저로 사이트 요청하면 html뿐 아니라 js, css, 추가 이미지 등 많은 자원 다운로드  
* 지금은 HTTP 지속 연결로 문제 해결  

## HTTP초기 - 연결, 종료 낭비  






