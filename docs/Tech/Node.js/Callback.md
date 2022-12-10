---
layout: default
title: Callback 함수
parent: Node.js
grand_parent: Tech
description: "Callback function"
permalink: /tech/node-js/callback
---

# 콜백함수란?
콜백 함수는 다른 코드(함수 또는 메서드)에게 인자로 넘겨줌으로써 그 제어권도 함께 위임한 함수이다. 
콜백 함수의 제어권을 넘겨받은 코드는 콜백 함수 호출 시점에 대한 제어권을 가진다.

### 콜백지옥이란? 
콜백 함수를 익명 함수로 전달하는 과정이 반복되어 코드의 들여쓰기 수준이 감당하기 힘들 정도로 깊어지는 현상

콜백 지옥을 벗어나기 위한 방법
-  Promise 사용: resolve나 reject가 실행되기 전까지는 다음(then) 또는 오류구문(catch)로 넘어가지 않는다
-  Generator 사용: Generator를 사용하면 Iterator가 반환되는데 Iterator는 next라는 메서드를 가지고 있어서, 이 next 메서드를 호출하면 generator 함수 내부에서 가장 먼저 등장하는 yield 함수 실행을 멈춤
- async/await 사용: 비동기 작업을 수행하고자 하는 함수 앞에 async를 표기하고, 함수 내부에서 실질적인 비동기 작업이 필요한 위치마다 await 표기 하는 것만으로도 뒤의 내용 자동 promise 전환 
