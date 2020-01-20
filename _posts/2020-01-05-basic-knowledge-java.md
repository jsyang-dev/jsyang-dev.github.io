---
title: 기본 지식 - Java
layout: post
subtitle: 개발자가 알아야 할 지식
tags:
- basicknowledge
- study
- java
author: Jeongsu Yang
comments: 'True'
---

### Java 언어의 장단점

- 장점
  - **운영체제에 독립적이다.**
    - JVM에서 동작하기 때문에, 특정 운영체제에 종속되지 않는다.
  - **객체지향 언어이다.**
    - 객체지향적으로 프로그래밍 하기 위해 여러 언어적 지원을 하고있다. (캡슐화, 상속, 추상화, 다형성 등)
    - 객체지향 패러다임의 특성상 비교적 이해하고 배우기 쉽다.
  - **자동으로 메모리 관리를 해준다.**
    - JVM에서 Garbage Collector라고 불리는 데몬 쓰레드에 의해 GC(Garbage Collection)가 일어난다. GC로 인해 별도의 메모리 관리가 필요 없으며 비지니스 로직에 집중할 수 있다.
  - **오픈소스이다.**
    - 정확히 말하면 OpenJDK가 오픈소스이다. OracleJDK는 사용 목적에 따라서 유료가 될 수 있다.
    - 많은 Java 개발자가 존재하고 생태계가 잘 구축되어있다. 덕분에 오픈소스 라이브러리가 풍부하며 잘 활용한다면 짧은 개발 시간 내에 안정적인 애플리케이션을 쉽게 구현할 수 있다.
  - **멀티스레드를 쉽게 구현할 수 있다.**
    - 자바는 스레드 생성 및 제어와 관련된 라이브러리 API를 제공하고 있기 때문에 실행되는 운영체제에 상관없이 멀티 스레드를 쉽게 구현할 수 있다.
  - **동적 로딩(Dynamic Loading)을 지원한다**
    - 애플리케이션이 실행될 때 모든 객체가 생성되지 않고, 각 객체가 필요한 시점에 클래스를 동적 로딩해서 생성한다. 또한 유지보수 시 해당 클래스만 수정하면 되기 때문에 전체 애플리케이션을 다시 컴파일할 필요가 없다. 따라서 유지보수가 쉽고 빠르다.
- 단점
  - **비교적 속도가 느리다.**
    - 자바는 한 번의 컴파일링으로 실행 가능한 기계어가 만들어지지 않고 JVM에 의해 기계어로 번역되고 실행하는 과정을 거치기 때문에 C나 C++의 컴파일 단계에서 만들어지는 완전한 기계어보다는 속도가 느리다. 그러나 하드웨어의 성능 향상과 바이트 코드를 기계어로 변환해주는 JIT 컴파일러 같은 기술 적용으로 JVM의 기능이 향상되어 속도의 격차가 많이 줄어들었다.
  - **예외처리가 불편하다.**
    - 프로그래머 검사가 필요한 예외가 등장한다면 무조건 프로그래머가 선언을 해줘야 한다.

> -

### OOP의 4가지 특징

1. 추상화
    - 구체적인 사물들의 공통적인 특징을 파악해서 이를 하나의 개념(집합)으로 다루는 것
2. 캡슐화
    - 정보 은닉(information hiding): 필요가 없는 정보는 외부에서 접근하지 못하도록 제한하는 것
3. 일반화 관계
    - 여러 개체들이 가진 공통된 특성을 부각시켜 하나의 개념이나 법칙으로 성립시키는 과정
4. 다형성
    - 서로 다른 클래스의 객체가 같은 메시지를 받았을 때 각자의 방식으로 동작하는 능력

> - [https://gmlwjd9405.github.io/2018/07/05/oop-features.html](https://gmlwjd9405.github.io/2018/07/05/oop-features.html)

### OOP의 5대 원칙 (SOLID)

- **S**: 단일 책임 원칙(SRP, Single Responsibility Principle)
  - 객체는 단 하나의 책임만 가져야 한다.
- **O**: 개방-폐쇄 원칙(OCP, Open Closed Principle)
  - 기존의 코드를 변경하지 않으면서 기능을 추가할 수 있도록 설계가 되어야 한다.
- **L**: 리스코프 치환 원칙(LSP, Liskov Substitution Principle)
  - 일반화 관계에 대한 이야기며, 자식 클래스는 최소한 자신의 부모 클래스에서 가능한 행위는 수행할 수 있어야 한다.
- **I**: 의존 역전 원칙(DIP, Dependency Inversion Principle)
  - 의존 관계를 맺을 때 변화하기 쉬운 것 또는 자주 변화하는 것보다는 변화하기 어려운 것, 거의 변화가 없는 것에 의존하라는 것이다.
- **D**: 인터페이스 분리 원칙(ISP, Interface Segregation Principle)
  - 인터페이스를 클라이언트에 특화되도록 분리시키라는 설계 원칙이다.

> - [https://gmlwjd9405.github.io/2018/07/05/oop-solid.html](https://gmlwjd9405.github.io/2018/07/05/oop-solid.html)

### 객체지향 프로그래밍과 절차지향 프로그래밍의 차이점

- 절차지향 프로그래밍
  - 실행하고자 하는 절차를 정하고, 이 절차대로 프로그래밍하는 방법
  - 목적을 달성하기 위한 일의 흐름에 중점을 둔다.
- 객체지향 프로그래밍
  - 실세상의 물체를 객체로 표현하고, 이들 사이의 관계, 상호 작용을 프로그램으로 나타낸다.
  - 객체를 추출하고 객체들의 관계를 결정하고 이들의 상호 작용에 필요한 함수(메서드)와 변수(필드)를 설계 및 구현하다.
  - 객체 지향의 행심은 연관되어 있는 변수와 메서드를 하나의 그룹으로 묶어서 그룹핑하는 것이다.
  - 사람의 사고와 가장 비슷하게 프로그래밍을 하기 위해서 생성된 기법
  - 하나의 클래스를 바탕으로 서로 다른 상태를 가진 인스턴스를 만들면 서로 다른 행동을 하게 된다. 즉, 하나의 클래스가 여러 개의 인스턴스가 될 수 있다는 점이 객체 지향이 제공하는 가장 기본적인 재활용성이라고 할 수 있다.

> -

### JVM의 구조

- JRE는 JVM과 Java API로 구성되어 있다.
- 자바 바이트코드는 JRE 위에서 동작하며, JRE는 JVM과 Java API로 구성되어 있다.
- 그 중 JVM은 자바 어플리케이션을 클래스 로더를 통해 읽어서 바이트코드를 해석하고 자바 API와 함께 실행하는 가장 중요한 역할을 담당하고 있다.
- 자바의 코드가 수행되는 과정은 Java Source(.java 파일)가 javac에 의해 Java Byte Code(.class 파일)로 변경되고 JVM의 클래스 로더가 컴파일된 자바 바이트코드를 런타임 데이터 영역에 로드하고 실행 엔진이 자바 바이트 코드를 수행하는 과정으로 이루어진다.
![java-jvm](/assets/post/basicknowledge/java-jvm.png)
- 클래스 로더(Class Loader)
  - 자바는 컴파일타임이 아니라 런타임에 클래스를 처음으로 참조할 때 해당 클래스를 로드하고 링크하는 특징이 있다. 이 동적 로드를 담당하는 부분이 JVM의 클래스 로더이다.
- 런타임 데이터 영역(Runtime Data Areas)
  - VM이라는 프로그램이 운영체제 위에서 실행되면서 할당받는 메모리 영역이다. 아래의 6가지 영역으로 나눌 수 있다.
    - 스레드 별 하나씩 생성되는 영역
      - PC Register: 스레드가 시작 될 때 생성, 현재 수행중인 JVM의 명령의 주소를 가진다.
      - JVM Stack: 스레드 시작 시 생성, 스택 프레임을 저장하는 스택
      - Native Method Stack: 자바 외의 언어로 작성된 네이티브 코드를 위한 스택
    - 모든 스레드가 공유하는 영역
      - Heap Area: 인스턴스 또는 객체를 저장하는 공간으로 가비지 컬렉션 대상
      - Method Area: 메서드 영역은 모든 스레드가 공유하는 영역으로 JVM이 시작될 때 생성됨
      - Java Garbage Collection: 각 클래스와 인터페이스의 상수뿐만 아니라, 메서드와 필드에 대한 모든 레퍼런스까지 담고 있는 테이블

> - [https://jeong-pro.tistory.com/148](https://jeong-pro.tistory.com/148)

### Java Collection Framework

![java-collection](/assets/post/basicknowledge/java-collection.png)
![java-map](/assets/post/basicknowledge/java-map.png)

- Set은 중복을 허용하지 않음, List는 중복 가능
- HashSet은 입력 순서 보장하지 않음, LinkedHashSet은 입력 순서 보장
- Vector는 동기화 지원, ArrayList는 지원하지 않음
- HashMap은 내부 hashing된 값에 따라 키 순서가 정해지므로 key는 특정 순서 없이 나옴
- TreeMap은 내부적으로 RedBlack Tree로 저장됨, 키값에 대한 Compartor 구현으로 정렬 순서를 바꿀수 있음, 정렬된 순서로 key 값이 나옴
- LinkedHashMap은 내부적으로 LinkedList, 입력 순서대로 key 값이 나옴

> -

### java의 non-static 멤버와 static 멤버의 차이

- non-static 멤버
  - 공간적 특성: **멤버는 객체마다 별도로 존재한다.**
    - ***인스턴스 멤버*** 라고 부른다.
  - 시간적 특성: **객체 생성 시에 멤버가 생성된다.**
    - 객체가 생길 때 멤버도 생성된다.
    - 객체 생성 후 멤버 사용이 가능하다.
    - 객체가 사라지면 멤버도 사라진다.
  - 공유의 특성: **공유되지 않는다.**
    - 멤버는 객체 내에 각각의 공간을 유지한다.
- static 멤버
  - 공간적 특성: **멤버는 클래스당 하나가 생성된다.**
    - 멤버는 객체 내부가 아닌 별도의 공간에 생성된다.
    - ***클래스 멤버*** 라고 부른다.
  - 시간적 특성: **클래스 로딩 시에 멤버가 생성된다.**
    - 객체가 생기기 전에 이미 생성된다.
    - 객체가 생기기 전에도 사용이 가능하다. (즉, 객체를 생성하지 않고도 사용할 수 있다.)
    - 객체가 사라져도 멤버는 사라지지 않는다.
    - 멤버는 프로그램이 종료될 때 사라진다.
  - 공유의 특성: **동일한 클래스의 모든 객체들에 의해 공유된다.**

> - [https://gmlwjd9405.github.io/2018/08/04/java-static.html](https://gmlwjd9405.github.io/2018/08/04/java-static.html)

### String, StringBuilder, StringBuffer 차이점

- String
  - String 클래스는 Immutable 객체이기 때문에 + 등 concat 연산 시 원본을 변경하지 않고 새로운 String 인스턴스를 생성해야 하는 단점이 존재한다. 하지만 JDK 1.5 이후부터는 컴파일 타임에 StringBuilder로 변경한다고 한다.
- StringBuilder
  - String에서 + 등으로 문자열 등을 concat하는 연산이 많은 경우 사용하는것이 좋다. 기존 String 문자들을 concat하는 경우 매번 새로운 String 인스턴스를 사용하기 때문에 성능상의 이슈 존재(JDK 1.5버전 부터는 내부적으로 StringBuilder를 이용하도록 변경되긴 했다.)
- StringBuffer
  - StringBuffer는 Builder와 비교해서 thread-safe하다. (멀티 스레드 환경에서 동기화의 지원 여부가 다름.) 내부적으로 append 등 모든 메소드에 대해 synchronized 키워드가 붙어있다.

> -

### Comparable, Comparator 차이점

- 정렬을 위해서 사용하는 인터페이스
- Comparable: 정렬 기준을 설정할 클래스가 직접 상속해 compareTo 메소드를 오버라이딩 해야 함
- Comparator: 직접 구현해서 Arrays.sort 같은 정렬 메소드에 인자로 넘겨 정렬 기준을 직접 설정해 줄 수 있음 (기본 Arrays.sort는 오름차순이지만, 위처럼 Comparator를 구현해서 파라미터로 넘겨주면 내림차순으로 정렬이 가능)

> -

### LinkedList와 ArrayList의 차이점

- LinkedList: 삽입, 삭제가 자주 일어나는 경우 유리한 구조
- ArrayList: 검색에 유리한 구조, 내부적으로 데이터를 배열에서 관리하며 데이터의 추가, 삭제를 위해 임시 배열을 생성해 데이터를 복사 하는 방법을 사용 하고 있기 때문에 삽입 삭제시 많은 복사가 일어남

> -

### Overload, Override 차이점

- Overload
  - 두 메서드가 같은 이름을 갖고 있으나 인자의 수나 자료형이 다른 경우
- Override
  - 상위 클래스의 메서드와 이름과 용례(signature)가 같은 함수를 하위 클래스에 재정의하는 것
  - 상속 관계에 있는 클래스 간에 같은 이름의 메서드를 정의

> - [https://gmlwjd9405.github.io/2018/08/09/java-overloading-vs-overriding.html](https://gmlwjd9405.github.io/2018/08/09/java-overloading-vs-overriding.html)

### Abstract Class, Interface 차이점

> -

### Java의 접근 제어자

> -

### JPA 란

> -

### 테스트 코드 작성 이유

> -

### 객체의 동일성, 동등성 차이점

> -

### 프로세스와 스레드의 차이

> -
