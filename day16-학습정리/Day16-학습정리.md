# Day16-학습정리

[https://www.youtube.com/watch?v=xz7e-GL2g6g](https://www.youtube.com/watch?v=xz7e-GL2g6g)

### 데이터 주고받는 규약

- TCP(전화기), UDP(라디오)

### **TCP**

- 일대일 연결만 가능
- 손실되면 재전송 요청 → 수신 확인 + 신뢰도 ↑ (ex 야, 다시 말해봐)
- 데이터의 순서와 무결성이 보장됨
- 느리다(UDP에 비해)
- 높은 신뢰도를 요구하는 서비스에 적합

### **UDP**

- 일대다 연결 가능
- 정보 수신 확인안하고 일방적으로 전송
- 데이터의 순서와 무결성 보장x → 손실되도 나몰라
- 빠르다(TCP에비해)
- 빠른 서비스에 적합 ex)줌에서 소리 뭉게져도 그냥 넘어가~

**공통 : 통신할때 데이터는 패킷이라는 작은단위로 나뉘어서 전송된다**

### **TCP handshake**

- **3handShake** : 연결 시작할때
- **4handShake** : 연결 끊을때 (tcp는 양방향이므로)

### **http(Hyper Text Transfer Protocol)**

- tcp, ip주소 기반으로 돌아가는 프로토콜
- client, server사이에 이루어지는 요청, 응답 등의 통신규약

### **http동작**

1. 사용자가 url입력 or 폼 입력 .. → 명령 내리면
2. 브라우저가 명령을 요청 message로 바꿔서 서버로 request 메시지 보낸다
3. 서버가 응답 메시지 body에 실행결과나 정적파일 담아 전송
4. 브라우저는 응답 바탕으로 렌더링

### **http특징**

- **단방향성**(반드시 client→server 요청 먼저 그다음 server→client응답)
- **비연결성**(응답 끝나면 바로 연결 닫는다) → 서버 자원 절약 가능 ↔소켓 통신

    소켓통신 : 연결 쭉 유지 ex)영상 통신

- **무상태성**(비연결성이므로 상태 가지지 않는게 좋다 ex) 로그인 유지 불가) → 보완하기위해 쿠키, 세션, 토큰 사용

### **http응답코드**

2xx → success(요청 정상적으로 이루어짐)

3xx → success. but redirecting필요. 즉 다음 url로 가야 요청이 완전히 끝난다

4xx → error. 클라이언트 오류. ex) 클라이언트 입력 에러, 로그인 안됬거나, 쿠키 없을떄

5xx → error. 서버 오류 → 사용 불가

### API ( application programming interface)

해당 프로그램 구현 몰라도 프로그램이 제공하는 기능 쓸 수 있도록 해주는 인터페이스

### **API없으면**

- 직접 소스코드 제공 or 직접 구현 필요
- 프론트와 백엔드 분리 어렵다→ 주로 백엔드 코드를 프론트에서 api형태로 사용하나봄

    백엔드 고치면 프론트에도 코드 그대로 붙여넣기하고 다시 재배포해야함

- 불특정 다수에게 소스코드, db 접근권한 다 노출시켜야함 → 위험

### **REST(Represental state Transfer) - 표현 상태 전송**

- http의 디자인 패턴

### **REST 제약 조건 (6개)**

**Client-Server**

- client, server의 기능 완전히 분리(백엔드, 프론트가 완전히 분리되어야 한다)

**StateLess**

- 무상태(상태 가지면 안된다. http 디자인 패턴이므로 http 특징 따른다)

**Cacheable**

- 캐시처리기능(client는 응답 캐싱할 수 있어야 한다) → client의 중복 요청 해소가능 ex)새로고침

    by 쿠키

**Layered System**

- 계층화(서버를 한개가 아닌 여러개로 계층화 가능)

    ex) 캐시 서버 : 캐시기능 해주는 서버

    로드 밸런서 : 

**Code on demand**

- 코드 온 디맨드(server → client 로직 전송하여 client에서 client자원으로 실행 가능)

ex) 피카츄배구

**Uniform Interface ??**

- 각 요청이 uri를 통해 완전히 식별가능해야한다
- 서버가 가지고 있는 리소스는 client의 응답과 구별되어야한다
- 클라이언트는 서버로부터 받은 정보만으로 리소스 변경, 삭제 가능해야한다

    즉 GET으로 가져온 데이터로 회원정보 수정, 삭제 가능해야한다

- 각 요청은 처리방법에 대한 충분한 정보를 담고있어야한다. 즉 응답이 모호하면 안됨
- HATEOAS : 리소스에대해 할 수 있는 모든 동작에 대한 uri를 제공한다

ex) 로그인하면 가능한 글쓰기, 회원정보 수정방법에 대한 uri 제공한다

### **HTTP 캐시**

캐시 유효시간 존재→지나면 서버로부터 다시 읽어온다. 이때 eTAG같으면 update x

(modify bit같은건가봄)

### **REST API**

- '/'로 계층관계 나타낸다
- 리소스에 대한 행위는 HTTP 매소드를 이용(GET, POST, PUT, DELETE)

### **HTTP 메소드**

Create : **POST**

Read : **GET =** 요청에 body부분 없다 → 주소에 리소스 위치가 드러나있어서

Update : **PUT**

Delete : **DELETE** = 요청에 body 없다 → 주소에 리소스 위치가 드러나있어서

**공통: 모두 응답에는 body가 들어간다(정적파일이나, 실행결과)**

### **페이지 로딩되는 과정**

1. client→ server url로 데이터 요청
2. 서버로 부터 받은 html파일 → html parser 통해 DOM Tree 객체 생성
3. 서버로부터 받은 style sheet → CSS parser 통해 Style Rules생성
4. DOM Tree, Style Rules합쳐서 Render Tree 생성 → 
5. layout정보로 Render Tree 배치 + painting정보로 Render Tree painting 후 display

![Untitled](https://user-images.githubusercontent.com/52225690/128761501-780af78d-1c20-499f-aacc-9c7b68f1fc57.png)

### 브라우저(Browser)

- www에서 정보 검색, 표현, 탐색 위한 소프트웨어
- 주소 입력창(인터페이스) : 특정 정보로 이동 가능
- 네트워크 모듈 포함(서버와 HTTP로 정보 주고받음)
- 서버로부터 받은 html, css, javascript 해석, 실행하여 화면에 보여주기위한 parser 가진다

### **브라우저 역할**

1. 사용자가 입력한 웹페이지, 이미지, 동영상등을 서버에게 요청
2. 서버로부터 받은 자원을 화면에 출력

### **브라우저 구성요소**

![Untitled 1](https://user-images.githubusercontent.com/52225690/128761493-24d76742-ffef-4123-b6cf-24b584513b50.png)

**User interface** : 검색창, 앞으로 뒤로가기, 새로고침

**Browser Engine** : 핵심 엔진 (데이터 쓰고, 읽고, Rendering Engine 제어..

**Rendering Engine** : html, css 파싱하여 최종적으로 화면에 출력해준다

**Networking** : http요청 할 수 있게

**JS Engine** : javascript 코드 해석 + 실행

**UI BackEnd** : 기본 위젯 그리는 인터페이스

**Data Stroage** : 쿠키, Indexed DB 등 브라우저 메모리 활용하여 저장하는 영역
