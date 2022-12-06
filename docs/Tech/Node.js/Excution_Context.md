---
layout: default
title: Excution Context 
parent: Node.js
grand_parent: Tech
description: "Excution Context in JavaScript"
permalink: /tech/node-js/excution-context
---

# 실행 컨택스트

실행할 코드에 제공할 환경 정보들을 모아놓은 객체로, JS는 어떤 실행 컨텍스카가 활성화되는 시점에 선언된 변수를 위로 끌어올리고(호이스팅), 
외부 환경 정보를 구성하고, this 값을 설정하는 등의 동작 수행 

- variableEnvironment: 현재 컨택스트 내의 식별자들에 대한 정보 + 외부 환경정보, 선언 시점의 LexicalEnvironment의 스냅샷으로 변경 사항은 반영되지 않음
- LexicalEnvironment: 처음에는 VariableEnvironment와 같지만 변경사항이 실시간으로 반영됨
- ThinsBinding: this 식별자가 바라봐야 할 대상 객체 
- environmentRecord: 현재 컨택스와 관련된 코드의 식별자 정보들이 저장됨 (함수에 지정된 매개변수 식별자, 선언된 함수 있는경우 함수 그자체, var로 선언된 변수의 식별자 등), 컨텍스트 내부 전체를 처음부터 훑어가며 순서대로 수집






```js
var a = 1;
function outer(){
  function inner(){
    console.log(a)
    var a = 3
  }
  inner();
  console.log(a)
}
outer()
console.log(a)
```


실행결과
```

```
