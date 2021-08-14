# Day19-학습정리

proxy서버

- 클라이언트와 서버 사이에 존재
- 보안(방화벽), ip변조, 캐시 등의 기능으로 사용된다
- 캐시 기능을 사용하게되면 외부와 불필요한 연결 x → 네트워크 병목현상 방지

Forward 프록시

![Untitled](https://user-images.githubusercontent.com/52225690/129254306-7d0a550d-0ddb-4f41-b449-79f7e82a5d2f.png)

- 인터넷앞, 클라이언트 뒤에 위치
- 사용자가 웹 브라우저를 이용해 프록시서버 사용설정 해야한다
- 사용자의 정해진 사이트만 연결가능
- 저렴하다

Reverse 프록시

![Untitled 1](https://user-images.githubusercontent.com/52225690/129254298-c3f77dad-da1c-478a-a5e7-9dcaebe01c1b.png)

- 프록시서버를 인터넷 리소스 앞에 위치
- 보안 위함/ WAS(DB서버와 연결)가 앞에있으면 위험
- 사용자는 프록시 서버에 연결되었음을 모른다
- 약간 api같은 개념인것같다. 코드에 직접 접근 못하게하기 위함

HTTP/3

- stream다루는 전송 프로토콜인 QUIC를 위해 설계
- QUIC = UDP기반 프로토콜
- 빠르고 신뢰도 높다 → 3handshake x + 다른방법으로 신뢰성 확보
- HTTP/2의 HOLB(head of line blocking 병목현상) 해결하기위해 나옴

    TCP : 패킷 순서가 중요 + 손실시 재전송 요청 → 병목현상 발생

HTTP/2

- TCP를 위해 설계 → HTTP계층에서 stream 다룬다

공통

- 서버 푸시 지원
- 헤더압축을 제공
- 스트림에 우선순위를 정한다
- 

QUIC

- TCP의 핸드쉐이크 과정을 최적화하는데 초점을 맞추었다
- UDP = 데이터그램 방식 사용 → 패킷 간의 순서가 없는 독립적
- UDP = 신뢰성 없는대신 빠르다 → 데이터 전송만 구현해놓은 프로토콜이므로 customizing 가능
- 3handshake 대신 데이터와함께 연결정보 전송 or 이전에 연결정보 캐시해놓는다
- 데이터 손실나면 손실데이터 빨리 파악해서 재전송 요청하는것같다(?)

[https://evan-moon.github.io/2019/10/08/what-is-http3/](https://evan-moon.github.io/2019/10/08/what-is-http3/)

### Status Code (상태 코드)

상태 코드에는 굉장히 많은 종류가 있다. 모두 숫자 세 자리로 이루어져 있으며, 아래와 같이 크게 다섯 부류로 나눌 수 있다.

- 1XX (조건부 응답) : 요청을 받았으며 작업을 계속한다
- 2XX (성공) : 클라이언트가 요청한 동작을 수신하여 이해했고 승낙했으며 성공적으로 처리했음을 가리킨다.
- 3XX (리다이렉션 완료) : 클라이언트는 요청을 마치기 위해 추가 동작을 취해야 한다.
- 4XX (요청 오류) : 클라이언트에 오류가 있음을 나타낸다.
- 5XX (서버 오류) : 서버가 유효한 요청을 명백하게 수행하지 못했음을 나타낸다.

http request 메시지 예시

```
GET https://velog.io/@surim014 HTTP/1.1								// 시작줄
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) ...			  // 헤더
Upgrade-Insecure-Requests: 1
```

### 1. 시작줄 (첫 줄)

첫 줄은 시작줄로 메서드/구조/버전으로 구성되었다.

GET : HTTP 

Method[https://velog.io/@surim014](https://velog.io/@surim014) : 사이트 주소

HTTP/1.1 : HTTP 버전

### 2. 헤더 (두 번째 줄부터)

두번째 줄부터는 헤더이며 **요청에 대한 정보**를 담고 있다. 

User-Agent, Upgrade-Insecure-Requests 등등이 헤더에 해당되며 헤더의 종류는 매우 많다.

### 3. 본문 (헤더에서 한 줄 띄고)

본문은 요청을 할 때 함께 보낼 데이터를 담는 부분이다. 현재 예시에는 단순히 주소로만 요청을 보내고 있고 따로 데이터를 담아 보내지 않기 때문에 본문이 비어있다.

http response 메시지 예시

```
HTTP/1.1 200 OK														// 시작줄
Connection: keep-alive												 // 헤더
Content-Encoding: gzip
Content-Length: 35653
Content-Type: text/html;

<!DOCTYPE html><html lang="ko" data-reactroot=""><head><title...
```

### 1. 시작줄 (첫 줄)

첫 줄은 버전/상태코드/상태메시지로 구성되어 있다. 200은 성공적인 요청이었다는 뜻이다.

### 2. 헤더 (두 번째 줄부터)

두 번째 줄부터는 헤더로 응답에 대한 정보를 담고 있다.

### 3. 본문 (헤더 뒤부터)

응답에는 대부분의 경우 본문이 있다. 보통 데이터를 요청하고 응답 메시지에는 요청한 데이터를 담아서 보내주기 때문이다. 응답 메시지에 HTML이 담겨 있는데 이 HTML을 받아 브라우저가 화면에 렌더링한다.

출처 : [https://velog.io/@surim014/HTTP란-무엇인가](https://velog.io/@surim014/HTTP%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80)
