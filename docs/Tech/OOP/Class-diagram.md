---
layout: default
title: 클래스 다이어그램
parent: OOP
grand_parent: Tech
description: "Class Diagram"
permalink: /tech/oop/class-diagram
---

# 클래스 다이어그램
UML에서 Static Structure Diagram으로 '시스템 클래스와, 속성, 메소드, 관계'등을 보여줌으로써 시스템의 구조를 묘사한다. 
Object Oriented Modeling의 주요 구성요소로써 애플리케이션 구조의 컨셉적인 모델링에 사용되며, 클래스 다이어그램은 데이터 모델링에도 사용될 수 있다. 
다이어그램에서 클래스는 '박스'로 표현되며 3가지 컴포넌트를 포함한다.

- Top Component: 클래스 이름, 굵은글씨로 중앙 정렬 되어있어야 하며 대문자로 시작해야 한다. 
- Middle Component: 클래스의 속성을 의미하며 왼쪽 정렬하고, 소문자로 시작한다. 
- Bottom Component: 클래스의 Operation(메소드?)를 의미하며 왼쪽 정렬하고, 소문자로 시작한다. 

여러개의 클래스들이 식별되고 그룹회되며 클래스다이어그램은 클래스간의 정적인 관계를 결정하는데 도움을 준다. 

## 1. Member
### 1-1. Visibility
- +: public
- -: private
- #: protected
- ~: package

### 1-2. Scope
- Instance Members: 인스턴스마다 속성값이 다르며, 메소드 호출이 인스턴스 상태에 영향을 미칠 수 있다. 
- Class Members: 모든 인스턴스마다 속성값이 같으며 Method 호출이 클래스 상태변화에 영향을 미치지 않는다. 

## 2. Relationship
### 2-1. 인스턴스 레벨 관계
- Dependency
- Association
- Aggregation
- Composition

### 2-2. 클래스 레벨 관계

