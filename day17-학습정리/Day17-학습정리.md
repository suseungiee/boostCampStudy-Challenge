# Day17-학습정리

![Untitled](https://user-images.githubusercontent.com/52225690/128917745-e7747efe-95f7-4541-a332-09f2be0c4b0b.png)


안드로이드에서 view는 맨 좌측상단이 0,0으로 원점이다

이후로 오른쪽으로 가면 x값 증가. 밑으로 내려가면 y값 증가다

그림에서 주황색의 (10,10)은 상위 view인 흰색으로부터 가로 10, 세로 10만큼 떨어져있다는 말이다

즉 항상 상대좌표이다

ex)

파란색의 (70,10)은 상위 view인 주황색으로부터 가로 70, 세로 10만큼 떨어져있다는 의미이며

주황색은 최상위 view인 흰색으로부터 가로 10, 세로 10만큼 떨어져있다.

따라서 파란색의 절대좌표는 70+10, 10+10인 (80,20)이 된다.

### **getTouchable()**

특정 위치를 클릭했을때 어떤 view가 클릭되었는지를 확인하기위한 함수.

최하위(view를 추가할수록 하위라고한다)view부터 보면서 해당 view의 내부에 클릭한 점이 존재하는지 확인. 즉 쌓은 순서 역순으로 확인한다!!

이와같이 상위 frame의 origin값으로부터 상대좌표만 가지고 ui를 그리는것을 **frame-based**방식이라한다.

하지만 화면이 갑자기 커지거나, 작아지는 경우에도 적정 비율로 잘 보여주기위해 layout도입 

(ex 기기별 화면 크기 변화 대응, 언어별 문자크키 변화 대응 - 한글이 영어보다 짧다)

![Untitled 1](https://user-images.githubusercontent.com/52225690/128917733-562d4abd-15fe-4725-8ab1-d67b2188620c.png)


다음과같이 layout이라는 top, bottom, left, right값을 기준으로 frame들을 배치시킨다

### **layout 종류**

![Untitled 2](https://user-images.githubusercontent.com/52225690/128917742-6973b9b1-6ed9-4361-8cd6-404224dbec52.png)


**LinearLayout**

- 세로 또는 가로 단일 방향으로 모든 하위요소 배치
- 뷰 객체들은 위치 중복 x

**RelativeLayout**

- 자식, 부모 뷰 간의 관게에 따라 배치

**FrameLayout**

- 여러개의 뷰를 중첩으로 배치하고 그중 하나를 선택적으로 보여줄 때
- 주로 화면 전환에 사용

**TableLayout**

- 행, 열로 이루어진 표 형태의 구조 가진 레이아웃
- 좌, 우로 합치는 것만 가능

**GridLayout**

- TableLayout보완 → 직관적인 행렬선언, 셀 병합가능

**ConstraintLayout**

- RelativeLayout의 상대 위치 + LinearLayout의 가중치 기능
- 체인 기능으로 다른 레이아웃 없이 요소끼리 그룹화 가능

그외 다양한 layout 존재한다
