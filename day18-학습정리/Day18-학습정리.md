# Day18-학습정리

### **RDB(Relational Database)**

- 관계형 데이터 모델에 기초를 둔 데이터베이스
- 모든 데이터를 2차원의 테이블 형태로 표현한 것(row, column)
- 데이터 독립성이 높으며 DML이용해 결합, 제약 등 표현능력 높일 수 있다

### **SQL(Structured Query Language)**

- RDBMS의 데이터 관리위해 사용되는 프로그래밍 언어
- SQL의 문법 3가지로 DML, DDL, DCL이 존재한다

### **DML(Data Manipulation Language)**

- 데이터 관리하는데 도움되는 SQL

 ex)select, update, insert, delete...

### **DDL(Data Definition Language)**

- 객체 생성, 변경,  SQL

ex)create, alter, drop..

### **DCL(Data Control Language)**

- 객체 권한 부여 SQL
- 데이터 보안, 무결성, 회복, 병행 제어 정의

ex) commit, rollback, grant..

### **RDBMS(RDB+Management System)**

- RDB생성하고 수정을 할 수 있는 소프트웨어

ER Model(Entity-Relationship)

- ERM의 결과물로 ER다이어그램(ERD)가 나온다
- Entity란 1개의 table, 객체? 라 봐도될듯

장점

- 그래픽형태로 이해 쉽다
- 특정 RDBMS에 종속적x
- 확장 가능
- 단순, 일반 모델에 적합

단점

- 복잡한 분야에 부적함
- (재사용, 상속, 다형성)x → 객체지향 모델링에 적용 hard → EER 모델 이용

![Untitled](https://user-images.githubusercontent.com/52225690/129091964-31f49c56-ba64-43e3-8af1-10a46018d954.png)

네모는 entity, 동그라미는 attribute, 선은 relation

[https://victorydntmd.tistory.com/126](https://victorydntmd.tistory.com/126)

[https://jwprogramming.tistory.com/49](https://jwprogramming.tistory.com/49)

[https://goodmilktea.tistory.com/55](https://goodmilktea.tistory.com/55)

Schema(스키마)

데이터베이스의 구조에 대한 전반적인 명세

ER, EER 모델링 차이

![Untitled 1](https://user-images.githubusercontent.com/52225690/129091934-818ccf7e-94be-4445-8bd0-3d3292b40dcd.png)

EER = ER에서 엔티티간 관계 표시해주는거 추가한것

![Untitled 2](https://user-images.githubusercontent.com/52225690/129091943-65029a76-ea31-4da5-aa66-d290fb1f5826.png)

### **index**

- 추가적인 쓰기 작업, 저장공간 활용하여 table 검색속도 향상시켜주는

자료구조

- 데이터와 데이터의 위치 포함한 자료구조
- index안쓰면 전체 탐색하는 Full Scan 써야한다
- 규모가 큰 데이터, insert, update, delete 자주 발생 x
- join, where, order by 에 자주 사용될 때 사용하면 좋다

**장점**

- table 조회, 성능 향상
- 전반적인 시스템 부하 감소

**단점**

- 인덱스 위한 저장공간 추가로 필요
- 인덱스 관리위한 추가 작업 필요
- 잘못 사용하면 오히려 역효과

### **인덱스 구현(어려움..)**

### **해시 테이블(Hash Table)**

(key,value)형태로 빠른 데이터 검색 필요할 때 유용

연관 데이터 조회 시 인덱스 효과 미미

![Untitled 3](https://user-images.githubusercontent.com/52225690/129091951-50eb0966-8ad5-4b70-99f6-2f4ee50d4b52.png)

### **B+Tree**

인덱스를 위해 자식 노드가 2개 이상인 B-Tree 개선시킨 자료구조

리프노드들은 Linked List로 연결되어있다

리프노드만 인덱스, 데이터를 가지고 나머지(인덱스 노드)는 인덱스만 가짐

![Untitled 4](https://user-images.githubusercontent.com/52225690/129091954-b63a3dad-324d-4bbf-96cc-62828a26a12e.png)

==================================================================================================================

**M-way Search Tree(MST)**

- 자식노드 구성할때 작은건 왼쪽, 큰건 오른쪽인 트리
- 1개의 키에 2개의 자식노드 존재
- 한개 노드에 여러개 키 가능 + 자식노드에 여러개 키 가능

**B-Tree**

- M-way tree의 차수가 많아지면 트리 높이 높아져서 비효율적 보완위함
- 규칙존재
    - 루트를 제외한 모든 노드는 ⌈m/2⌉ 만큼의 자식 포인터를 가져야 한다. 차수가 10이면 한 개의 노드가 자식 포인터를 최소 5개 가져야한다.
    - 루트 노드는 최소 2개의 자식 포인터를 가져야 한다.
    - 모든 리프 노드는 똑같은 레벨이어야 한다.
    - creation process는 bottom-up이라고 생각하면 된다.

![Untitled 5](https://user-images.githubusercontent.com/52225690/129091957-2c1ff096-7646-4e2a-9f8e-b4fc3a631414.png)

    **B+Tree**

![Untitled 6](https://user-images.githubusercontent.com/52225690/129091961-cf864c6e-7f03-4793-81de-33a050373853.png)

    [https://velog.io/@seanlion/btree](https://velog.io/@seanlion/btree)

    ### **db구현 고려사항**

    C : 없음?

    R : 페이지 단위 IO

    U : 데이터 업데이트 시 inplace인지 outplace인지 + 페이지 단위 IO

    D : 데이터 삭제 시 hard delete인지 soft delete인지
