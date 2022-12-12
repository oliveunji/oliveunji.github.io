---
layout: default
title: 클로저
parent: Node.js
grand_parent: Tech
description: "Closer"
permalink: /tech/node-js/closure
---

# 클로저란? 
여러 함수영 프로그래밍 언어에서 등장하는 보편적 특성으로, MDN 정의는 다음과 같다.
"A closure is the combination of a function and the lexical environment within wich that function was declared."

코드예시 #1
```js
var outer = fuunction() {
  var a = 1
  var inner = function() {
    console.log(++a);
  }
  inner();
}
outer();
```

inner 함수 내부에서는 a를 선언하지 않았기 떄문에 outerEnvironmentReference에 지정된 상위 컨텍스트인 outer의 LexicalEnvironment에 접근해 a 찾아서 출력후, 
outer 실행 컨텍스트 종료시 가비지 컬렉션에 의해 a 삭제된다. 

코드예시 #2
```js
var outer = function (){
  var a = 1
  var inner = function(){
    return a++
  }
  return inner;
}
var outer2 = outer();
console.log(outer2());
console.log(outer2());
```
inner 실행 시점에는 outer 함수 실행 종료된 상황인데도 불구하고 a 가 참조 가능하다. 
그 이유는 outer 함수의 실행이 종료되더라도 inner 함수는 outer2 실행하면 호출 가능해지기 때문에 가비지 컬렉션 대상에서 제외되기 때문이다. 

이를 바탕으로 클로저를 재정의 해보면, **클로저란 어떤 함수 A에서 선언한 변수 a를 참조하는 내부함수 B를 외부로 전달한 경우 A의 실행 컨텍스트가 종료된 이후에도 a 가 사라지지 않는 현상**이다. 

클로저는 객체지향과 함수형 모두를 아우르는 매우 중요한 개념으로 메모리 소모는 클로저의 본질적인 특성일 뿐이며, 관리법 (필요성이 사라진 시점에 더는 메모리 사용하지 않게 해줌) 만 잘 파악해서 사용하면 된다.

## 클로저 활용 사례
1. 콜백 함수 내부에서 외부 데이터 사용하고자 할때
    - 콜백 함수를 내부함수로 선언하여 외부 변수를 직접 참조하는 방법
    - bind로 값을 직접 넘겨줌
    - 콜백 함수를 고차함수로 바꿔서 클로저 적극 활용 
2. 접근 권한 제어 - 함수에서 지역변수와 내부함수 선언하고, 외부에 접근 권한 줄 대상만 return 함
3. 부분 적용함수 (필요한 모든 파라미터 넘어오면 실행)
4. 커링 함수 (lazy loading 관련)



