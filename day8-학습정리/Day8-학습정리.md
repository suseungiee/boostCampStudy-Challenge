# Day8-학습정리

(day8내용에 없는 내용만 추가)

**클로저(Closure), 함수(Function) 차이**

클로저 역시 함수지만 함수가 생성될 때 state를 점유하고 있다면 이는 클로저

ex) let f = makeInc(10)

f(5)

f(5)에서는 f는 10이라는 값이 전달 x but makxInc(10)에서는 10이라는 state 점유

즉 state 값을 점유하고 있는 함수(?)

### **클로저 표현방식**

{ {인자들} → 반환타입 in 로직 }

ex) let reverseNames = names.sorted(by: { (s1: String, s2: String) -> Bool in return s1 > s2})

### **클로저 축약**

- 타입 명시 생략 가능

ex) let reverseNames = names.sorted(by: {s1, s2 in return s1 > s2})

- 반환 키워드 생략 가능

ex) let reverseNames = names.sorted(by: {s1, s2 in s1 > s2})

- 인자이름 생략 가능

ex) let reversedNames = names.sorted(by: { $0 > $1 })

- 연산자만 남기기

ex) let reversedNames = names.sorted(by: > )

- 후행 클로저

ex) let reversedNames = names.sorted() { $0 > $1 }

### **etc 고차함수**

**fold**

reduce와 동일 but 초깃값 지정

ex) val arr = listOf(1,2,3,4,5)

val res = arr.fold(10,{first,second→first+second})  //10+1+2+3+4+5 → 25

**객체 지향 패러다임(견해, 인식체계)**

프로그램을 객체들의 모임으로 표현하는 프로그램 패러다임

**함수형 패러다임**

부작용을 최대한 제거하여 가능한 코드 대부분이 입력→출력의 관계를 갖게 하는 프로그램 패러다임

공통점??