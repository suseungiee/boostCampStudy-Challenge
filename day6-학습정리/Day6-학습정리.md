# Day6-학습정리

## **리소스(Resource)**

- 안드로이드 리소스란 실행 가능 애플리케이션에 연결되어있는 파일이나 값을 의미
- app에서 다시 컴파일해서 deploy하지 않고도 변경될 수 있게 실행파일과 연결
- 보편화된 각종 UI프레임워크에서 매우 중요한 역할

ex)문자열 리소스, 레이아웃 리소스, 색상, 치수 ...

**레이아웃 리소스**

안드로이드 UI프로그래밍에 사용되는 필수적인 핵심 리소스

안드로이드에서 화면의 뷰는 XML파일로부터 로딩되는 경우가 많다

![Untitled](https://user-images.githubusercontent.com/52225690/127037622-3821bbbf-4a31-490f-8e17-9b0fb3eefc0e.png)

 ※리소스 종류에 상관없이 모든 안드로이드 리소스는 자바 소스코드안에서 각각의 id를 통해 식별, 참조된다.

## **DOM(Document Object Model)**

- Jsoup에서 사용했음
- html요소들의 구조화된 표현
- 트리구조

![Untitled 1](https://user-images.githubusercontent.com/52225690/127037618-f87bd4f9-9e93-40d6-bcfb-3dcd538ac427.png)

- ㅁ항상 유효한 html문서의 인터페이스 → 유효하지 않은 html코드도 교정되어 나온다
- 변경 가능한 동적 모델
- 가상요소 포함 x → ::after (?)
- 보이지 않는 요소 포함 o → display:none같은거

## **XPath**

- xml보다 쉽고 약어로 되어있다.
- xml문서의 노드를 정의하기 위해 경로식 사용

즉 html, xml상의 요소의 위치값 → 페이지의 UI 변경에 따라 값 변화 가능

[http://twinbraid.blogspot.com/2015/02/xpath.html](http://twinbraid.blogspot.com/2015/02/xpath.html)

체크포인트처럼 /vector/group/path[1]처럼 요소 이름을 써도되지만

다음과같이 패턴을 이용해도 된다

ex)

developer        : <developer>요소 모두 선택

/p_languages   : 루트 노드의 자식인 p_languages요소 선택 (절대 경로 탐색)

p_lang/lang : <p_lang> 요소의 자식 중 <lang>요소 모두 선택 (상대 경로 탐색)

//                    :루트 노드이ㅡ 하위 노드 모두 선택

//priority        : 위치에 상관없이 <priority>요소 모두 선택

.//                  : 현재 노드의 하위 노드 모두 선택

version/@status    : 모든 <version>요소의 status속성 노드 모두 선택

[http://mm.sookmyung.ac.kr/~sblim/lec/xml03/xml05-04a.htm](http://mm.sookmyung.ac.kr/~sblim/lec/xml03/xml05-04a.htm)

XML사용 이유

호환되지 않는 데이터타입 사용하는 시스템 간의 데이터교환에 많은 노력 필요 + 손실 발생 가능

but xml : 데이터를 텍스트형식으로 저장 → 소프트웨어, 하드웨어에 독립적

따라서 xml사용하면 운영체제, 프로그램, 브라우저에 상관없이 데이터 전달 가능

(앞서 말했듯 안드로이드 실행파일과 연결)

## **html, xml 차이**

xml : 데이터 저장, 전송 목적인 마크업 언어

html : 데이터를 웹 상에 표현하기 위한 목적

따라서 둘은 큰 차이가 없지만 html은 태그의 의미가 정확히 정해져있다

but xml은 태그의 의미 사용자가 마음대로 정의가능

## **JSON, XM**L

**공통점**

- 데이터 저장, 전달 목적
- 기계 + 사람도 이해 가능
- 계층구조
- parsing가능

**차이점**

JSON

- 종료 태그 사용 x
- XML 보다 구문 짧다
- XML보다 읽고 쓰는데 삐르다
- 배열 사용 가능
- 자바스크립트 표준 함수인 eval()함수로 파싱된다
- 전송받은 데이터의 무결성(데이터 신뢰도)을 사용자가 직접 검증해야한다

XML

- 배열 사용 불가
- xml 파서로 파싱된다

데이터 검증이 필요한 곳에서는 스키마를 사용해 데이터 무결성 검증 가능한 xml이 많이 쓰인다.
