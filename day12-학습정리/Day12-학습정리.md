# Day12-학습정리

## **동기(Synchronized)**

프로그램이 순차적으로 실행되는것. blocking되고 결과값 기다리는 방식. 일반적인 방식

## **비동기(Asynchronized)**

- 프로그램이 실행되다 흐름이 분기가 되면 쓰레드를 분기시켜서 다음코드 이어서 실행하고 이어서 분기된 부분 완료되면 결과 반환받는 방식
- 구현하기 까다롭다
- 너무 남발하면 가독성 떨어진다 → js에서 promise객체, await, async문법 사용

## **Observer pattern**

- Observer가 관찰하고자하는 Subject들의 상태변화를 관찰하다 상태가 변화되면 객체에게 **직접** 통지하는 방식

## **Publisher, Subscriber pattern**

- Observer pattern에서 Observer, Subject의 관계를 분리시키기위한 방법
- 중간에 큐를 이용
- Publisher는 큐로 event 발생 알림 → 큐에서 event확인하고 해당 Subject에게 전달
- 같은 event기다리는 Subject가 많거나 Subject에로 전달하는 과정에서 에러가 발생하면 이후 작업 밀린다 → Subject로 event broadcast하는작업을 Asynchronized하게 구현

## **코루틴(Coroutine)**

- Sub Routine이란 진입점과 반환점이 1개씩인 반면 코루틴은 여러개. 아무데나 나가고 진입 가능
- 쓰레드보다 작은 작업단위로 context switching발생 x → 메모리 소모 많이 x
- 코루틴 시작은 GlobalScope.launch → 이후 job객체 반환 → 작업 취소가능
- 코루틴 내부에서 사용되는 함수는 suspend 키워드 사용
- coroutine라이브러리 설치 필요

[https://lwndnjs93.tistory.com/92](https://lwndnjs93.tistory.com/92)

### **Coroutine 주의사항**

코루틴이 선언되어 있는 **오브젝트가 활성화** 되어있어야한다(객체 생성) 안그러면 실행 x

### **코루틴(Coroutine)**

- 코루틴은 즉 **작업의 단위를 Thread가 아닌 Object로 축소**시켜 작업전환에 있어 다수의 Thread 불필요하게 한것
- 즉 Thread의 대안이 아닌 Thread를 더 잘게 쪼개어 사용하기 위한 개념
- 하나의 Thread가 다수의 코루틴 수행 가능
- Lightweight Thread라 부르기도 한다

### **async**

- coroutine제어하는 다른 방법
- launch는 수행 시 job객체를 반환하는 반면 async는 deferred객체 반환
- deferred객체는 반환값을 가진다
- job객체는 couroutine 제어만 가능 → job.cancel(). job.join()//coroutine 대기
- deferred객체는 제어 + 결과도 받을 수 있다 → await()//coroutine 대기

### CoroutineScope

- 코루틴의 범위, 코루틴 블록을 제어할 수 있는 단위
- GlobalScope는 CoroutineScope의 종류 → 프로그램 전반에 걸쳐 백그라운드에서 동작

```
    val scope = CoroutineScope(Dispatchers.Main)

    val job = scope.launch {
      // ...

      CoroutineScope(Dispatchers.Main).launch {
          // 외부 코루틴 블록이 취소 되어도 끝까지 수행됨
      }

      // ...
    }

    // 외부 코루틴 블록을 취소
    job.cancel()
```

외부 코루틴 블록 내부에서 새로운 coroutineScope생성 → job.cancel()로 취소 불가

### **Dispatcher**

어떤 쓰레드에서 해당 코루틴 실행시킬지 정할 수 있다

ex) Dispatchers.Default, Dispatchers.IO, Dispatchers.Unconfined

### **suspend → 콜백함수 대신 사용??**

- 코루틴 내부에서 사용할 함수에 붙이는 키워드 → 코루틴 외부에서 쓰면 에러
- 해당 함수는 언제든지 지연, 재개 가능

### **콜백, 리스너**

콜백 : 다른함수에 인자로 전달되는 함수. event발생하면 콜백함수 실행 (1개)

리스너 : event발생하면 연결된 리스너들에게 event전달(n개)

### **코루틴 사용 방법**

1. 사용할 Dispatcher 결정

 2. Dispatcher이용해 CoroutineScope생성

1. launch, async로 수행 코드 블록 작성

[https://medium.com/@limgyumin/코틀린-코루틴의-기초-cac60d4d621b](https://medium.com/@limgyumin/%EC%BD%94%ED%8B%80%EB%A6%B0-%EC%BD%94%EB%A3%A8%ED%8B%B4%EC%9D%98-%EA%B8%B0%EC%B4%88-cac60d4d621b)

### **소프트웨어 아키텍쳐 패턴(디자인 패턴)**

![Untitled](https://user-images.githubusercontent.com/52225690/128066090-7bd520a1-8991-4234-bc03-f4c6d8de3e87.png)

controller는 view(UI), model(데이터)  컨트롤해준다

controller에서 입력받고 작업 처리

view는 model이용하여 화면 업데이트(model→view notify / view가 model polling)

가장 단순 but view, model의 의존성 높아 유지보수 어렵다


![Untitled 1](https://user-images.githubusercontent.com/52225690/128066085-5ee78221-62ea-4e7d-9654-d80c6ec00e08.png)

Presenter는 controller보다 중재자 역할 → 간접적으로 데이터만 전달

MVC보다 UI종속적인 코드 제거된다

view, model간 의존성 문제 해결 but view, presenter의존성 높아짐

![Untitled 2](https://user-images.githubusercontent.com/52225690/128066089-ecb31fc6-893f-494a-aa10-e60516a54b33.png)

ViewModel은 View의 추상화 계층. 

ViewModel은 View, Model관계와 상관없이 자기 할일(event notify)만 하면된다

view-viewModel은 observer패턴/ view가 observer, ViewModel이 subject

데이터 갱신을 view가 자동으로 알 수 있다
