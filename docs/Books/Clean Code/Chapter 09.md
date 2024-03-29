---
layout: default
title: Chapter 09
parent: Clean Code
grand_parent: Books
description: "Chapter 09"
permalink: /books/clean-code/chapter-09
---

# 9. 단위 테스트
테스트를 추가하려고 급하게 서두르는 와중에 프로그래머들이 제대로 된 테스트케이스를 작성해야 한다는 미묘한 사실을 놓쳐버렸다.

## TDD 법칙 세가지
1. 실패하는 단위 테스트를 작성할때까지 실제 코드를 작성하지 않는다
2. 컴파일을 실패하지 않으면서 실행이 실패하는 정도로만 단위 테스트를 작성한다
3. 실패하는 테스트를 통과할 정도만 실제 코드를 작성한다.

## 꺠끗한 테스트 코드 유지하기
지저분한 테스트코드를 내놓으나 테스트를 안하나, 오십보 백보, 아니 오이려 더 못함.
테스트 코드는 실제 코드 못지않게 중요하며 꺠끗하게 짜야한다.

### 테스트는 유연성, 유지보수성, 재사용성을 제공한다.
코드에 유연성, 유지보수성, 재사용성을 제공하는 버팀목이 바로 단위테스트이다.
테스트케이스가 없으면 개발자는 변경을 주저한다.
실제 코드를 점검하는 자동화된 단위 테스트 슈트는 설계와 아키텍처를 최대한 깨끗하게 보존하는 열쇠다. 

## 꺠끗한 테스트 코드
깨끗한 테스트코드를 만드려면 가독성이 필요하고 -> 명료성, 단순성, 풍부한 표현력이 필요하다.

## 테스트당 ASSERT 하나
TEMPLATE METHOD 패턴을 사용하면 중복을 제거할 수 있다. 
어쩌면 테스트 함수마다 한 개념만 테스트하라는 규칙이 더 나을수도 있다.

## F.I.R.S.T
- Fast: 테스트는 빨라야한다
- Independent: 테스트는 서로 의존하면 안되며, 각 테스트는 독립적으로 어떤 순서로 실행해도 괜찮아야 한다
- Repeatable: 테스트는 어떤 환경에서도 반복 가능해야 한다
- Self-validationg: 테스트는 부울 값으로 결과를 내야한다
- Timely: 테스트는 적시에 작성해야 한다. 단위 테스트는 테스트하려는 실제 코드를 구현하기 직전에 구현한다.

## 결론
테스트 코드는 실제 코드의 유연성, 유지보수성, 재사용성을 보존하고 강화한다. 
표현력을 높이고 간결하게 정리하자. DSL을 만들자 

## 북틸
- https://nomadcoders.co/community/thread/9299
- https://dongpark.notion.site/9-23815f9364134cc9b40c52c6dc2328c0

#노개북 #노마드코더 #개발자북클럽
