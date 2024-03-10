## Chapter 1 깨끗한 코드
### 코드는 항상 존재하리라. 코더도 항상 존재할까?
코드는 상세하고 정밀한 요구사항 명세라는 점에서 코드는 시대의 변화와 무관하게 존재할 것이다. \
하지만 코더(프로그래머)는 어떨까? 생성형 인공지능이 "정밀한 요구사항"을 작성해내는 역량에 달려있다.

### 코드가 그 문제를 풀기위한 언어처럼 보인다면 '아름다운 언어'다.
흔히들 문제를 풀기 적합하지 않다며 언어를 탓하곤 한다. \
하지만 언어를 단순하게, 프로그램을 단순하게 만드는 역할은 프로그래머다. 언어를 광신하거나 탓하지 말자.

---

## Chapter 2 의미 있는 이름
### 이름에 의도를 명확히 하라
항상 고민인 지점은 의도를 명확히 하다보니 명칭이 길어진다는 점이다. \
명칭이 길어지면서 code formatting 조건에 따라 indent 나 line break 가 발생할 수도 있다. \ 

### 불용어: 특정한 의미를 가지지 않는 단어
뜨끔한 명칭이 있다. 바로 Info와 Data. \
ORM이 감싸 Entity 객체가 서비스 로직에 들어가기 전 조금 수정된 객체나, DTO와 Entity 사이의 객체를 Info 또는 Data로 칭한 경험이 많다. \
개선하자면 `${Entity}Before/After${Service/DTO}`정도가 떠오른다. 'Before' 'After' 키워드 대신에 'Transformed', 'Resource' 키워드도 좋아보인다. \
만약 두 Layer 사이를 새로운 Layer로 구분한다면 명명이 더 쉬울 것이다. 

### 네이밍 인코딩: 인터페이스
저자는 이 객체가 인터페이스임을 드러내지 않고 싶어한다. \
그 이유가 무엇일까? 실제로 구체 클래스가 인터페이스 클래스를 implement 하는 순간 해당 클래스의 역할은 클래스의 행동을 강제하는 것일 뿐 그것이 인터페이스인지를 네이밍까지 해서 알려줄 필요가 없다. \
이것은 추상화 원칙을 위반하는 것이다. \


### 생성자 네이밍 센스
생성자를 오버로딩하는 경우, 생성자가 필요한 파라미터를 정적 메서드를 활용하여 명확히 드러내는 것이 좋다.
```java
Money money = Money.FromAmount(10000);
// upper is better than below
Money money = new Money(10000);
```
근데 이거 Builder 패턴 쓰면 더 좋지 않나?

---

## Chapter 3
### 함수가 하나의 행동을 한다는 것
함수 내부의 로직이 일관된 추상화 레벨에서 돌아가야 한다는 것.
### 인수
인수는 최대 2개까지. 가장 좋은 구성은 0개. \
Javascript 와 Java 의 가장 큰 차이가 여기인 듯. 
javascript의 함수는 일급 객체, 함수가 내부 함수의 인수로도 들어가서 currying이 구현됨 => 함수형 프로그래밍
초심자 입장에서는 함수가 만능 열쇠처럼 느껴짐. 
출력 인수를 사용하는 것도 어색하지 않음. Array.map 등 프로토타입 메서들는 function(this) 형태로 출력 인수를 사용함. 
java에서 operation은 각 객체의 method() 짓. 객체에 질려하는 이유가 여기에 있을 수도.
### 시간적인 결합 Temporal Coupling
두 함수(행동)이 순서에 맞게 일어나야 하는 관계에 있는 것을 의미. \
따라서 캡슐화, builder 패턴, exception 등을 활용하여 시간적인 결합을 제거하는 것이 좋다. \

https://betterprogramming.pub/temporal-coupling-in-code-e74899f7a48f