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

