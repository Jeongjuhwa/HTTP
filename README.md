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
![HTTP초기](https://user-images.githubusercontent.com/59909855/124380224-908a9980-dcf6-11eb-8d15-fb3e2470e2e6.PNG)  

## HTTP 지속연결  
![HTTP 지속](https://user-images.githubusercontent.com/59909855/124380226-92545d00-dcf6-11eb-8408-ff753c5885c2.PNG)  

## HTTP 메시지  
![HTTP 메시지 구조](https://user-images.githubusercontent.com/59909855/124380463-ab114280-dcf7-11eb-8e6f-2d837c6f44e0.PNG)  

## 시작 라인 - 요청 메시지  
* start-line = request-line  
* request-line = method SP(공백) request-target SP HTTP-version CRLF(엔터)  
* HTTP 메서드(GET:조회)  
* 요청 대상(/search?q=hello&hl=ko)  
* HTTP Version  

## 시작라인 - HTTP 메서드  
* 종류: GET, POST, PUT, DELETE ...  
* 서버가 수행해야 할 동작 지정  

## 시작라인 - 요청 대상  
* absolute-path[?query](/search?q=hello&hl=ko)  

## 시작라인 - HTTP 버전  
* HTTP Version(HTTP/1.1)  

## 시작라인 - 응답 메시지  
* start-line - status-line  
* status-line = HTTP-version SP status-code SP reason-phrase CRLF  

## HTTP 헤더  
![HTTP 헤더](https://user-images.githubusercontent.com/59909855/124380619-96817a00-dcf8-11eb-9e3e-369ac633b917.PNG)  
* HTTP 전송에 필요한 모든 부가정보  

## HTTP 메시지 바디  
* 실제 전송할 데이터  
* HTML, 이미지, 영상 JSON 등등 byte로 표현할 수 있는 모든 데이터 전송 가능  

## 단순함 확장 가능  
* HTTP는 단순함  
* HTTP 메시지 또한 매우 단순  

## HTTP 메서드(HTTP API 설계)  
#### 요구사항  
* 회원 목록 조회
* 회원 조회  
* 회원 등록  
* 화원 수정  
* 회원 삭제  

#### API URI 설계 고민  
* 가장 중요한 것은 리소스 식별  
* 리소스는? -> 미네랄을 캐라 -> 미네랄이 리소스!  
* 회원이라는 개념 자체가 바로 리소스가 됨  
* 회원이라는 리소스만 식별하면 된다 -> 회원 리소스를 URI에 매핑  

#### API URI 설계  
* 회원 목록 조회 -> /members  
* 회원 조회 -> /members/{id}  
* 회원 등록 -> /members/{id}  
* 회원 수정 -> /members/{id}  
* 회원 삭제 -> /members/{id}  

#### 리소스와 행위를 분리  
* URI는 리소스만 식별  
* 리소스는 명사, 행위는 동사  
* 행위의 구분은?(POST, GET 등등~)  

## HTTP 메서드 종류  
* GET: 리소스 조회  
* POST: 요청 데이터 처리, 주로 등록에 사용  
* PUT: 리소스를 대체, 해당 리소스 없으면 생성(중요한게 리소스 대체임-> 덮어쓰기 개념~ 예를들어 name 정 age 26저장 되어 있는데 put으로 age 27만 put으로 보내면 name필드 아예 사라짐)  
* PATCH: 리소스 부분 변경(PUT의 한계를 보완)  
* DELETE: 리소스 삭제  

## GET  
* 리소스 조회  
* 서버에 전달하고 싶은 데이터는 quesy를 통해 전달  
* 메시지 바디로 데이터 전달 가능함 -> 지원하지 않는 곳이 많아서 권장안함  

## POST  
* 요청 데이터 처리  
* 메시지 바디를 통해 서버로 요청 데이터 전달  
* 스펙: POST메서드는 대상 리소스가 리소스의 고유 한 의미 체계에 따라 요청에 포함 된 표현을 처리하도록 요청합니다(구글 번역~)  
* 정리: 리소스 URI에 POST요청이 오면 데이터를 어떻게 처리할지 리소스마다 따로 정해야 함  
* POST의 결과로 새로운 리소스가 생성되지 않을 수도 있음  
* JSON으로 조회데이터 넘길때 GEt 메서드 사용이 어렵고 애매하면 POST로 넘기자  

## HTTP 메서드의 속성  
* 안전  
* 멱등  
* 캐시가능  

![참고](https://user-images.githubusercontent.com/59909855/124381065-7a330c80-dcfb-11eb-93e4-6ea801031870.PNG)  

## 안전  
* 호출해도 리소스를 변경하지 않는다.  

## 멱등  
* 한 번 호출하든 두 번 호출하든 100번 호출하든 결과가 같음  
* 멱등 메서드  
  * GET: 여러번 조회해도 같은 결과 조회  
  * PUT: 결과를 대체한다. 따라서 같은 요청 여러번 해도 최종 결과 같음  
  * DELETE: 결과를 삭제. 같은 요청 여러번 해도 삭제된 결과 같음  
  * POST: 멱등아님!!! 결제를 두 번 호출하면 같은 결제 중복 발생!!!  
* 활용  
  * 자동 복구 메커니즘  
  * 서버가 TIMEOUT등으로 정상 응답 못주었을 때 클라이언트가 같은 요청을 다시 해도 되는지 판단하는 근거  

## 캐시가능  
* GET, HEAD, POST, PATCH 캐시 가능  
* 실제로는 GET, HEAD 정도만 캐시로 사용 -> POST, PATCH는 본문 내용까지 캐시 키로 고려해야 하는데, 구현 쉽지 않음  

## HTTP 메서드 활용  
* 쿼리 파라미터를 통한 데이터 전송: GET(주로 정렬 필터)  
* POST, PUT, PATCH(회원가입, 상품 주문, 리소스 등록, 리소스 변경)  

## 클라이언트에서 서버로 데이터 전송  
* 정적 데이터 조회  
* 동적 데이터 조회  
* HTML FORM을 통한 데이터 전송  
* HTTP API를 통한 데이터 전송  

## 정적 데이터 조회  
* 이미지, 정적 테스트 문서  
* 조회는 GET 사용  
* 쿼리 파라미터 없이 리소스 경로로 단순 조회  

## 동적 데이터 조회  
* 주로 검색, 게시판 목록에서 정렬 필터  
* 조회 조건을 줄여주는 필터  
* 조회는 GET 사용  
* GET은 쿼리 파라미터 사용해서 데이터 전달  

## HTML FORM 데이터 전송  
* HTML FORM submit시 POST 전송  
* Content-Type: application/x-www-form-urlencoded 사용  
* HTML FORM은 GET전송도 가능  
* Content-Type: multipart/form-data  
  * 파일 업로드 같은 바이너리 데이터 전송시 사용  
  * 다른 종류의 여러 파일과 폼의 내용 함께 전송 가능  
* HTML FORM 전송은 GET, POST만 지원  

## HTTP API 데이터 전송  
* 서버 to 서버(백엔드 시스템 통신)  
* 앱 클라이언트(아이폰, 안드로이드)  
* 웹 클라이언트(AJAX)  
* POST, PUT, PATCH: 메시지 바디를 통해 데이터 전송  
* GET: 조회, 쿼리 파라미터로 데이터 전달  
* Content-Type:application/json을 주로 사용  

## 간단한 HTTP API 설계  
#### API 설계 - POST 기반 등록  
* 회원 목록 /members -> GET  
* 회원 등록 /members -> POST  
* 회원 조회 /members/{id} -> GET  
* 회원 수정 /members/{id} -> PATCH, PUT, POST  
* 회원 삭제 /members/{id} -> DELETE  
##### 특징  
* 클라이언트는 등록될 리소스의 URI 모름  
* 서버가 새로 등록된 리소스 URI를 생성  
* 컬렉션  
  * 서버가 관리하는 리소스 디렉토리  
  * 서버가 리소스의 URI를 생성하고 관리  
  * 여기서 컬렉션은 /members  

#### API 설계 - PUT 기반 등록  
* 파일 목록 /files -> GET  
* 파일 조회 /files/{filename} -> GET  
* 파일 등록 /files/{filename} -> PUT  
* 파일 삭제 /files/{filename} -> DELETE  
* 파일 대량 등록 /files -> POST  

##### 특징  
* 클라이언트가 리소스 URI를 알고 있어야 한다 (PUT/files/star.jpg)  
* 클라이언트가 직접 리소스의 URI를 지정  
* 스토어  
  * 클라이언트가 관리하는 리소스 저장소  
  * 클라이언트가 리소스의 URI를 알고 관리  
  * 여기서 스토어는 /files  

#### API 설계 - HTML FORM 사용  
* 회원 목록 /members -> GET  
* 회원 등록 폼 /members/new -> GET  
* 회원 등록 /members/new OR /members -> POST  
* 회원 조회 /members/{id} -> GET  
* 회원 수정 폼 /members/{id}/edit -> GET  
* 회원 수정 /members{id}/edit OR /members/{id} -> POST  
* 회원 삭제 /members/{id}/delete -> POST  

##### 특징  
* HTML FORM은 GET, POST만 지원  
* AJAX같은 기술을 사용해서 해결 가능  
* 컨트롤 URI  
  * GET.POST만 지원해서 제약 있음  
  * 해결을 위해 동사로 된 리소스 경로 사용  
  * POST의 /new, /edit, /delete가 컨트롤 URI  

## 상태코드  

#### 2xx - 성공  
* 200 -> 요청 성공  
* 201 -> 요청 성공으로 새로운 리소스 생성  
* 202 -> 요청은 접수, 처리는 아직(ex 배치)  
* 204 -> no contents: 서버가 요청을 성공적으로 수행했지만, 응답에 보낼 데이터 없음  

#### 3xx -> 리다이렉션  
##### 참고: 웹 브라우저는 3xx응답 결과에 Location 헤더가 있으면, Location위치로 자동 이동  

#### 일시적인 리다이렉션  
* 302 Found -> 리다이렉션시 요청 메서드가 GET으로 변하고, 본문이 제거될 수 있음(거의 302 현업에서 많이 씀)  
* 307 Temporary Redirect -> 리다이렉트시 요청 메서드와 본문 유지(무조건 요청 메서드를 변경하면 안됨)  
* 303 See Other -> 리다이렉트시 요청 메서드가 GET으로 변경(무조건)  

#### PRG(post/redirect/get) 예시  
* PRG사용 전 -> post로 주문 후 웹 브라우저 새로고침의 경우  
 * 중복 주문 됨  
* PRG사용 후  
 * POST로 주문후에 주문 결과 화면을 GET 메서드로 리다이렉트  
 * 새로고침해도 결과 화면을 GET으로 조회  
 * 중복 주문 대신에 결과 화면만 GET으로 다시 요청  

![PRG](https://user-images.githubusercontent.com/59909855/125194071-a108ba00-e28a-11eb-92e9-1a2e843baf6b.PNG)  

#### 304 Not Modified  
* 캐시를 목적으로 사용  
* 클라이언트에게 리소스가 수정되지 않았음을 알려준다. 따라서 클라이언트는 로컬PC에 저장된 캐시를 재사용(캐시로 리다이렉트) -> ex) 이미지를 서버에서 다운 받고 새로고침 시 다시 다운 받는게 아니라 변경사항이 없으니 기존에 받은 이미지 그대로 사용  
* 304 응답은 응답에 메시지 바디를 포함하면 안된다. (로컬 캐시를 사용해야 하므로)  
* 조건부 GET, HEAD 요청시 사용  

#### 4xx -> 클라이언트 오류  
* 클라이언트가 잘못된 요청을 해서 서버가 요청을 처리할 수 없음  

#### 5xx -> 서버 오류  
* 서버 문제로 오류 발생  

#### 4xx과 5xx의 차이점은 5xx은 서버에서의 오류라 클라이언트가 5xx오류를 받고 시간이 지난 뒤 같은 요청을 보냈을 때 요청 성공할 수 있는데 4xx은 아님




























