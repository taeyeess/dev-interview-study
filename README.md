<div align=center>

![](/assets/images/logo/pinterest_profile_image.png)

</div>

<div align=center>

</div>

---


## :memo: Table of Contents

- [Introduction](#introduction)
- [Part 1. CS](#part-1-cs기초)
    - [개발상식](https://github.com/dev-interview-study/tree/main/CS_Fundamentals/Development)
    - [자료구조](https://github.com/dev-interview-study/tree/main/CS_Fundamentals/DataStructure)
    - [네트워크](https://github.com/dev-interview-study/tree/main/CS_Fundamentals/Network)
    - [운영체제](https://github.com/dev-interview-study/tree/main/CS_Fundamentals/OS)
    - [데이터베이스](https://github.com/dev-interview-study/tree/main/CS_Fundamentals/Database)
    - [디자인패턴](https://github.com/dev-interview-study/tree/main/CS_Fundamentals/DesignPattern)
    - [알고리즘](https://github.com/dev-interview-study/tree/main/CS_Fundamentals/Algorithm)
- [Part 2. Language](#part-2-language)
    - [Java](https://github.com/dev-interview-study/tree/main/Language/Java)
    - [JavaScript](https://github.com/dev-interview-study/tree/main/Language/JavaScript)
- [Part 3. Framework](#part-3-framework)
    - [React](https://github.com/dev-interview-study/tree/main/Framework/React)
    - [Spring](https://github.com/dev-interview-study/tree/main/Framework/Spring)
- [Part 4. Position](#part-4-position)
    - [Frontend](https://github.com/dev-interview-study/tree/main/Position/Frontent)
    - [Backend](https://github.com/dev-interview-study/tree/main/Position/Backend)
- [Reference](#reference)
    - [TBD]
- [Git 활용](#Git-활용)
    - [TBD]


# Introduction
예비 개발자 취업 및 현업자 이직준비에 필요한 기술면접 스터디입니다. 
Contributor들이 각자 주제에 대한 공부를 진행하고, 정리한 자료를 공유하여 다른 멤버들과 함께 성장하기를 목표로 합니다. 주제 외 도움될만한 자료 및 레퍼런스를 올리는 것도 환영합니다.
해당 Repository에서 학습을 하다가 추가로 궁금한 부분은 `Issue`를 통해 질문해주세요:)

---

# Part 1.  CS기초

## :books: 개발상식 [링크](https://github.com/93jpark/dev-interview-study/tree/main/CS_Fundamentals/Development)

- 좋은 코드란 무엇인가?
- 객체 지향 프로그래밍이란 무엇인가?
- RESTful API
- Test-Driven-Development
- 함수형 프로그래밍
- MVC 패턴
- Git & GitHub

## 🧬 자료구조 [링크](https://github.com/93jpark/dev-interview-study/tree/main/CS_Fundamentals/DataStructure)

- Array vs LinkedList
- Stack and Queue
- Tree
    - Binary Tree
    - Full Binary Tree
    - Complete Binary Tree
    - BST (Binary Search Tree)
- Binary Heap
- Red-Black Tree
    - 정의, 특징
    - 삽입, 삭제
- Hash Table
    - Hash Function
    - Resolve Collision
        - Open Addressing
        - Separate Chaining
    - Resize
- Graph
    - Graph 용어 정리
    - Graph 구현, 탐색
    - Minimum Spanning Tree
- 시/공간 복잡도

## 🌍 네트워크 [링크](https://github.com/93jpark/dev-interview-study/tree/main/CS_Fundamentals/Network)

- OSI 7계층
- GET, POST 방식의 차이점
- TCP 3-way-handshake & 4-way handshake
- TCP 와 UDP 의 차이점
- HTTP 와 HTTPS 의 차이점
    - HTTP 의 문제점들
- DNS round robin 방식
- 웹 통신의 큰 흐름
- 공개키 암호, 대칭키 암호
- HTTP 동작과정과 HTTP method, 상태코드
- Stateful vs Stateless 서비스
- 로드 밸런싱
- Naver를 치면 일어나는 과정

## :computer: 운영체제 [링크](https://github.com/93jpark/dev-interview-study/tree/main/CS_Fundamentals/OS)


- 컴퓨터 시스템의 동작 원리
- 프로세스와 스레드의 차이
- 스케줄러의 종류
    - 장기 스케줄러
    - 단기 스케줄러
    - 중기 스케줄러
- Context Switching
- Interrupt
- System Call
- Dead Lock
- CPU 스케줄러
    - FCFS
    - SJF
    - SRT
    - Priority scheduling
    - RR
- 동기와 비동기의 차이
- 멀티스레드
    - 장점과 단점
- 프로세스 동기화
    - Critical Section
    - 해결책
- 메모리 관리 전략
    - 메모리 관리 배경
    - Paging
    - Segmentation
- 가상 메모리
    - 배경
    - 가상 메모리가 하는 일
    - Demand Paging (요구 페이징)
    - 페이지 교체 알고리즘
- 캐시의 지역성
    - Locality
    - Caching line

## 🗂 데이터베이스 [링크](https://github.com/93jpark/dev-interview-study/tree/main/CS_Fundamentals/Database)

- 데이터베이스
    - 데이터베이스를 사용하는 이유
    - 데이터베이스 성능
    - 데이터베이스 기본 용어
- Index
    - Index 란 무엇인가
    - Index 의 자료구조
    - Primary index vs Secondary index
    - Composite index
    - Index 의 성능과 고려해야할 사항
- 정규화에 대해서
    - 정규화 탄생 배경
    - 정규화란 무엇인가
    - 정규화의 종류
    - 정규화의 장단점
- Transaction
    - 트랜잭션(Transaction)이란 무엇인가?
    - 트랜잭션과 Lock
    - 트랜잭션의 특성
    - 트랜잭션의 상태
    - 트랜잭션을 사용할 때 주의할 점
    - 트랜잭션 격리수준
- Statement vs PreparedStatement
- NoSQL
    - 정의
    - CAP 이론
        - 일관성
        - 가용성
        - 네트워크 분할 허용성
    - 저장방식에 따른 분류
        - Key-Value Model
        - Document Model
        - Column Model
- Optimizer
- Replication
- Partitioning
- Sharding
- Object-Relational Mapping (ORM)

## 📤 디자인패턴 [링크](https://github.com/93jpark/dev-interview-study/tree/main/CS_Fundamentals/DesignPattern)

- 생성 패턴 (5개)
    - 싱글톤 (Singleton)
    - 팩토리 메소드 (Factory Method)
    - 추상 팩토리 (Abstract Factory)
    - 빌더 (Builder)
    - 프로토타입 (Prototype)

- 구조 패턴 (7개)
    - 어댑터 (Adapter)
    - 브릿지 (Bridge)
    - 컴포짓 (Composite)
    - 데코레이터 (Decorator)
    - 퍼사드 (Facade)
    - 플라이웨이트 (Flyweight)
    - 프록시 (Proxy)

- 행동 패턴 (11개)
    - 책임 연쇄 (Chain-of-Responsibility)
    - 커맨드 (Command)
    - 인터프리터 (Interpreter)
    - 이터레이터 (Iterator)
    - 중재자 (Mediator)
    - 메멘토 (Memento)
    - 옵저버 (Observer)
    - 상태 (State)
    - 전략 (Strategy)
    - 템플릿 메소드 (Template Method)

## 🧩 알고리즘 [링크](https://github.com/93jpark/dev-interview-study/tree/main/CS_Fundamentals/Algorithm)

- 선택 정렬
- 거품 정렬
- 병합 정렬
- 삽입 정렬
- 퀵 정렬
- 힙 정렬
- 투포인터 알고리즘
- 순열(Permutation)
- BFS & DFS
- 이분탐색
- 최대공약수와 최소공배수
- LRU Cache
- Greedy Algorithm
- Dijkstra Algorithm

# Part 2. Language

## Java [링크](https://github.com/93jpark/dev-interview-study/tree/main/CS_Fundamentals/Language/Java)


#### :warning: *TBD*

## JavaScript [링크](https://github.com/93jpark/dev-interview-study/tree/main/CS_Fundamentals/Language/Java)


#### :warning: *TBD*


# Part 3. Framework

## 🌼 Spring [링크](https://github.com/93jpark/dev-interview-study/tree/main/Framework/Spring)

- 스프링 프레임워크란
- Spring, Spring MVC, Spring Boot의 차이
- Bean이란
- Container란
- IOC(Inversion of Control, 제어의 역전)란
- MVC 패턴이란
- DI(Dependency Injection, 의존성 주ㅋ입)란
- AOP(Aspect Oriented Programming)란
- POJO
- DAO와 DTO의 차이
- Spring JDBC를 이용한 데이터 접근
- Filter와 Interceptor 차이

## ☢️ React [링크](https://github.com/93jpark/dev-interview-study/tree/main/Framework/React)

#### :warning: *TBD*


# Part 4. Position

## Front-end [링크](https://github.com/93jpark/dev-interview-study/tree/main/Position/Frontend)
#### :warning: *TBD*

## Back-end [링크](https://github.com/93jpark/dev-interview-study/tree/main/Position/Backend)
#### :warning: *TBD*


# Reference

#### :warning: *TBD*

# Git 활용

- Git 가이드 for 스터디 참여 [링크](https://github.com/93jpark/dev-interview-study/tree/main/Git)

