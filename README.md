# HTTP

## 출처 - https://inf.run/5K7o

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

## HTTP 헤더  
#### 용도  
* HTTP 전송에 필요한 모든 부가정보(ex: 바디의 내용, 바디의 크기, 압축, 인증, 요청 클라이언트, 서버정보, 캐시 등등)  

## HTTP 바디  
![HTTP메시지 구성](https://user-images.githubusercontent.com/59909855/125455654-a2507821-bf1b-4056-8eda-a9ce61441939.PNG)  

* 메시지 본문을 통해 표현 데이터 전달  
* 표현은 요청이나 응답에서 전달할 실제 데이터  
* 표현 헤더는 표현 데이터를 해석할 수 있는 정보 제공  

#### 표현  
* Content-Type: 표현 데이터의 형식  
* Content-Encoding: 표현 데이터의 압축 방식  
* Content-Language: 표현 데이터의 자연 언어  
* Content-Length: 표현 데이터의 길이(전송 코딩을 사용하면 Content-Length사용 금지)  
* 표현 헤더는 전송, 응답 둘다 사용  

## 협상(콘텐츠 네고시에이션)  
* Accept: 클라리언트가 선호하는 미디어 타입 전달  
* Accept-Charset: 클라이언트가 선호하는 문자 인코딩  
* Accept-Encoding: 클라이언트가 선호하는 압축 인코딩  
* Accept-Language: 클라이언트가 선호하는 자연 언어  
* 협상 헤더는 요청시에만 사용  

## 협상과 우선순위1  
![협상과 우선순위 Lang](https://user-images.githubusercontent.com/59909855/125456623-be81dc17-c0e1-48f2-851e-32ef48791a3c.PNG)  
* Quality Values(q)값 사용  
* 0~1, 클수록 높은 우선순위  
* 생략은 1  

## 협상과 우선순위2  
![협상과 우선순위2](https://user-images.githubusercontent.com/59909855/125456848-b9f6e101-2d22-4825-931a-9611fac1656e.PNG)  

* 구체적인 것이 우선  

1. text/plain;format=flowed  
2. text/plain  
3. text/*  
4. */*  

## 전송 방식  
* 단순 전송  
* 압축 전송  
* 분할 전송  
* 범위 전송  

## 일반 정보  
* From: 유저 에이전트의 이메일 정보  
* Referer: 이전 웹 페이지의 주소  
* User-Agent: 유저 에이전트 애플리케이션 정보  
* Server: 요청을 처리하는 오리진 서버의 소프트웨어 정보  
* Date: 메시지가 생성된 날짜  

#### From  
* 일반적으로 잘 사용되지 않음  
* 검색 엔진 같은 곳에서 주로 사용  
* 요청에서 사용  

#### Referer  
* 현재 요청된 페이지의 이전 웹 페이지 주소  
* A -> B로 이동을 위해 요청할 때, Referer:B를 포함해서 요청  
* Referer를 사용해서 유입 경로 분석 가능  
* 요청에서 사용  

#### User-Agent  
* 클라이언트의 애플리케이션 정보  
* 통계정보  
* 어떤 종류의 브라우저에서 장애가 발생하는지 파악 가능  
* 요청에서 사용  

#### Server, Date  
* 응답에서 사용  

## 특별한 정보  
* Host: 요청한 호스트 정보(도메인)  
* Location: 페이지 리다이렉션  
* Allow: 허용 가능한 HTTP메서드  
* Retry-After: 유저 에이전트가 다음 요청을 하기까지 기다려야 하는 시간  

#### HOST  
![Host](https://user-images.githubusercontent.com/59909855/125458346-0ee96ae2-79ed-4972-b1e8-b6a22e3e74a8.PNG)  
* 요청에서 사용  
* 필수값  
* 하나의 서버가 여러 도메인을 처리해야 할 때  
* 하나의 IP 주소에 여러 도메인이 적용되어 있을 때  

#### Location  
* 웹 브라우저는 3xx응답의 결과에 Location헤더가 있으면, Location위치로 리다이렉트  

#### Allow  
* 405(Method Not Allowed)에서 응답에 포함->GET,HEAD,PUT  

#### Retry-After  
* 503(Service Unavailable): 서비스가 언제까지 불능인지 알려줌  


## 인증  
* Authorization: 클라이언트 인증 정보를 서버에 전달  
* WWW-Authenticate: 리소스 접근시 필요한 인증 방법 정의  

#### Authorization  
* Authorization: Basic xxxxxxxxxxxxxxxx  

#### WWW-Authenticate  
* 401 Unauthorized응답과 사용  
* WWW-Authenticate: Newauth realm="apps", type=1, title="Login to \"apps\"", Basic realm="simple"  

## 쿠키  
* Set-Cookie: 서버에서 클라이언트로 쿠키 전달(응답)  
* Cookie: 클라이언트가 서버에서 받은 쿠키를 저장하고, HTTP 요청시 서버로 전달  

#### Stateless  
* 쿠키 미사용 -> 로그인 하고 새로고침하면 로그인 정보 사라짐  
* HTTP는 무상태 프로토콜  
* 클라이언트와 서버가 요청과 응답을 주고 받으면 연결 끊김  
* 클라이언트와 서버는 서로 상태를 유지하지 않음  

#### 쿠키  
* 서버에서 쿠키를 받으면 다음 모든 요청에 쿠키 정보 자동 포함  
* 예) set-cookie: sessionId=abcde1234; expires=Sat, 26-Dec-2020 00:00:00 GMT; path=/; domain=.google.com; Secure  
* 사용처  
  * 사용자 로그인 세션 관리  
  * 광고 정보 트래킹  

* 쿠키 정보는 항상 서버에 전송  
  * 네트워크 트래픽 추가 유발  
  * 최소한의 정보만 사용  
  * 서버에 전송하지 않고, 웹 브라우저 내부에 데이터를 저장하고 싶으면 웹 스토리지 사용  



#### 쿠키-생명주기(Expires, max-age)  
* Set-Cookie: expires=Sat, 26-Dec-2020 04:39:21 GMT(만요일이 되면 쿠키 삭제)  
* Set-Cookie: max-age=3600 (3600초) -> 0이나 음수를 지정하면 쿠키 삭제  
* 세션 쿠키: 만료 날짜를 생략하면 브라우저 종료시 까지만 유지  
* 영속 쿠키: 만료 날짜를 입력하면 해당 날짜까지 유지  

#### 쿠키-도메인  
* 예) domain=example.org  
* 명시: 명시한 문서 기준 도메인 + 서브 도메인 포함  
  * domain=example.org를 지정해서 쿠키 생성  
   * example.org, dev.example.org 접근 가능  

* 생략: 현재 문서 기준 도메인만 적용  
 * example.org 에서 쿠키를 생성하고 domain 지정을 생략  
  * example.org 에서만 쿠키 접근  
  * dev.example.org는 쿠키 미접근  

#### 쿠키-경로  
* 예) path=/home  
*  경로를 포함한 하위 경로 페이지만 쿠키 접근  
*  일반적으로 path=/ 루트로 지정  

#### 쿠키-보안  
* Secure  
  * 쿠키는 http, https를 구분하지 않고 전송  
  * Secure를 적용하면 https인 경우에만 전송  

* HttpOnly  
  * XSS 공격 방지  
  * 자바스크립트에서 접근 불가(document.cookie)  
  * HTTP 전송에만 사용  

* SameSite  
  * XSRF 공격 방지  
  * 요청 도메인과 쿠키에 설정된 도메인이 같은 경우만 쿠키 전송  


## 캐시와 조건부 요청  
#### 캐시가 없을 때  
* 데이터가 변경되지 않아도 계속 네트워크를 통해 테이터 다운로드 -> 비효율적  

#### 캐시 적용  
![캐시1](https://user-images.githubusercontent.com/59909855/125774685-f623708b-d8f8-4b16-9166-9b9a9b6ee2a5.PNG)  
![캐시2](https://user-images.githubusercontent.com/59909855/125774716-b3b368fe-ad25-401c-80fc-29ac9d091731.PNG)  

* 캐시 덕분에 캐시 가능 시간동안 네트워크 사용 x
* 비싼 네트워크 사용량 줄일 수 있음  
* 브라우저 로딩 속도 빠름  

## 캐시 시간 초과  
* 캐시 유효 시간이 초과하면 2가지 상황 나타남  

1. 서버에서 기존 데이터 변경  
2. 변경x  

* 캐시 만료후에도 데이터 변경 안했으면 재사용 가능 -> 대신 클라이언트 데이터와 서버 데이터가 같다는 사실 확인할 수 있는 방법 필요  

![검증헤더 1](https://user-images.githubusercontent.com/59909855/125775612-1da46d06-fdb3-4dfd-8304-68dac0ec9330.PNG)  
![검증헤더2](https://user-images.githubusercontent.com/59909855/125775614-896fe434-9d37-4f57-b168-7dd94b687db5.PNG)  
![검증헤더3](https://user-images.githubusercontent.com/59909855/125775615-fc4dca89-64bf-487d-b009-a9131690fc68.PNG)  
![검증헤더4](https://user-images.githubusercontent.com/59909855/125775616-ccb268f1-f886-4349-a1fa-b47f0e62c07b.PNG)  
![검증헤더5](https://user-images.githubusercontent.com/59909855/125775617-23cfe479-62e0-4869-8f3f-f63cf93a6498.PNG)  
![검증헤더6](https://user-images.githubusercontent.com/59909855/125775620-d0b19b19-cce4-47ea-90b2-825c71987d88.PNG)  
![검증헤더7](https://user-images.githubusercontent.com/59909855/125775622-d5d99a28-4ca4-4afb-a9f7-b2718148358a.PNG)  
![검증헤더8](https://user-images.githubusercontent.com/59909855/125775625-87b542b2-3a57-4d3e-b3ff-17dc1ad0092f.PNG)  







































