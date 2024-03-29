---
layout: default
title: Chapter 07
parent: Designing Data-Intensive Applications
grand_parent: Books
description: "Chapter 07"
permalink: /books/designing-data-intensive-applications/chapter-07
---

# Chapter 07. 트랜잭션
트랜잭션이란 애플리케이션에서 몇 개의 읽기와 쓰기를 하나의 논리적인 단위로 묶는 방법으로 내결함성 갖춘 시스템을 구현하기 위한 방법으로 널리 채택되어 옴
한 트랜잭션 내의 모든 읽기와 쓰기는 한 연산으로 실행되며 전체가 성공하거나, 실패한다 -> 이는 애플리케이션에서 오류 처리를 단순화할 수 있다
트랜잭션은 자연 법칙이 아니며 프로그래밍 모델을 단순화하려는 목적으로 만든것으로, 애플리케이션에서 어느정도 잠재적 오류 시나리오나 동시성 문제를 무시할 수 있도록 해준다. => **안정성보장**

문제가 생길 수 있는 여러 예를 조사하고, 이런 문제를 방지하기 위해 사용하는 알고리즘을 살펴본다. 
또한 다양한 경쟁조건과, **커밋 후 읽기, 스냅숏 격리, 직렬성** 등을 어떻게 구현하는지 살펴본다.

## 애매 모호한 트랜잭션 개념
NoSQL 와 같은 요즘 등장한 DB 중 다수는 트랜잭션을 완전히 포기하거나, 훨씬 약한 보장을 의미하는 단어로 재정의했다. 

### ACID의 의미
A(Atomicity) 원자성, C(Consistency) 일관성, I(Isolation) 격리성, D(Durability) 지속성 
현실에서는 DB 마다 ACID 구현이 제각각이다. ACID 표준을 따르지 않는 시스템은 때로 BASE 라고 불린다.

#### 원자성
원자적 - 더 작은 부분으로 쪼갤 수 없는 무언가
ACID의 맥락에서 보면, 원자성은 여러 쓰기 작업이 하나의 원자적인 트랜잭션으로 묶여 있는데 결함때문에 완료될 수 없다면 어보트 되는 것.

#### 일관성
ACID 맥락에서의 일관성은 - 데이터에 관한 어떤 선언은 불변식 이다? 
하지만 일관성 아이디어는 애플리케이션의 불변식 개념에 의존하고, 일관성을 유지하도록 트랜잭션을 올바르게 정의하는건 애플리케이션 책임이다. (DBMS가 보장할 수 있는게 아님)

#### 격리성
ACID 맥락에서의 격리성은 동시에 실행되는 트랜잭션은 서로 격리된다는 것을 의미한다. 고전적인 DB 교과서에서는 격리성을 직렬성이라고 한다. 
여러 트랜잭션이 동시에 실행되었을때에도 결과가 트랜잭션이 순차적으로 (하나씩 차례대로) 실행됬을때의 결과가 같다. 
하지만 직렬성 격리는 성능 손해를 동반함으로 현실에서는 거의 사용하지 않고, 실제로는 직렬성보다 보장이 약한 스냅숏 격리를 구현한다. 

#### 지속성
지속성은 트랜잭션이 성공적으로 커밋됬다면, 트랜잭션에서 기록한 모든 데이터는 손실되지 않는다는 보장이다. 하지만 완벽한 지속성은 존재하지 않는다. 

### 단일 객체와 다중 객체 연산
클라이언트가 한 트랜잭션 내에서 여러번의 쓰기를 하면 DBMS가 어떻게 해야하는지? 

### 단일 객체 쓰기
보통 저장소 엔진들은 거의 보편적으로 한 노드에 존재하는 단일 객체 수준에서 원자성과 격리성을 제공하는 것을 목표로 한다 

### 오류와 어보트 처리
어보트된 트랜잭션을 재시도 하는 것은 간단하고 효과적이 지만 완벽하지는 않다.

### 완화된 격리수준
동시성문제는 트랜잭션이 다른 트랜잭션에서 동시에 변경한 데이터를 읽거나 두 트랜잭션이 동시에 같은 데이터를 변경하려고 할 때만 나타난다. 
운이없을때만 촉발되기 때문에 테스트하기 어렵고 재현하기도 어렵ㄴ다 
DBMS는 오랫동안 트랜잭션 격리를 제공함으로써 동시성 문제를 감추려 했다. 하지만 직렬성 격리는 성능 비용이 있다.
따라서  완화된 격리수준을 사용하는 시스템들이 많다. 

### 커밋 후 읽기
#### 더티 읽기 - 읽을때 커밋된 데이터만 보게 된다 (더티 읽기가 없음)
다른 트랜잭션에서 커밋되지 않은 데이터 보는게 더티읽기 이다. 
-> 구현 방법
1. 로우 수준 잠금을 사용한다
: 특정 객체 변경하고 싶은 경우 객체에 대한 잠금 획득하고 진행해야 함 (읽기 잠금)
-> 하지만 이 방법은 현실적이지 않음. 응답시간에 해를 끼침. 그래서 대부분 DBMS는 과거의 커밋된 값과 새로 쓴값 모두 기억해서, 트랜잭션 실행중인 동안 과거값 읽도록 한다.
-> 하지만 비반복 읽기나 읽기 스큐의 경우에 대해서는 완전히 보장하지 못한다.

2. 스냅숏 격리
위의 버그에 대한 흔한 해결책으로 각 트랜잭션은 DB의 일관된 스냅숏으로부터 읽는다. 이 경우는 실행하는데 오래 걸리며 읽기만 실행하는 질의에 요긴하다.

3. 일관된 스냅숏을 보는 가시성 규칙
   객체를 읽을떄 트랜잭션 ID를 사용해 어떤건 볼 수 있고 어떤건 못보는지 결정함 

#### 더티 쓰기 - 커밋된 데이터만 덮어쓴다 (더티 쓰기 없음)
커밋되지 않은 먼저 쓴 내용을 나중에 실행된 쓰기 작업이 덮어 쓰는 경우 더티 쓰기라 부른다. 
1. 스냅 숏 격리
읽는쪽에서 쓰는쪽을 결코 차단하지 않고, 쓰는쪽에서 읽는쪽을 결코 차단하지 않는다.
이를 구현하기 위해 DBMS는 객체마다 커밋된 버전 여러개를 유지할 수 있어야 한다. (MVCC 다중 버전 동시성 제어 라고도 함)

