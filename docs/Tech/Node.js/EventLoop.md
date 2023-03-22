---
layout: default
title: Event Loop
parent: Node.js
grand_parent: Tech
description: "Event Loop"
permalink: /tech/node-js/event-loop
---

# Node JS란 무엇인가?
<img width="401" alt="image" src="https://user-images.githubusercontent.com/39396725/226844435-0268c86a-53de-46c2-9977-8a2b8be8a55a.png">
JavaScript가 백엔드 역할을 수행할 수 있도록 하게 하는 런타임?
NodeJs는 V8과 libuv를 
V8 - 오픈소스 자바스크립트 엔진, 
libuv - c++ 오픈소스 시스템, Node가 OS의 파일시스템, 네트워킹, 컨커런시 등에 접근할 수 있게 함
Node.js 중간에 끼고 사용하는 이유? 
- JS와 C++를 잇는 가교 역할을 하고, series of wrapper 이다.


Node.js가 wrapper라는 걸 알수있는 코드
<img width="853" alt="image" src="https://user-images.githubusercontent.com/39396725/226847179-d0bdf3e0-9b03-4bb9-8ab4-ea4301718336.png">
여기서 보면 pbkdf2에 대한 실제 구현은 없고 \_pbfdf2를 호출한다

<img width="914" alt="image" src="https://user-images.githubusercontent.com/39396725/226847640-a5185dcc-a266-4cef-a101-ce1ec5c41adb.png">
\_pbfdf2 는 PBKDF2를 호출하는데

<img width="444" alt="image" src="https://user-images.githubusercontent.com/39396725/226847748-317268f3-59af-432e-a325-68e6f990b3b6.png">

<img width="920" alt="image" src="https://user-images.githubusercontent.com/39396725/226847831-9a4b5559-65c2-4362-904d-b02c6dacd099.png">

process.binding()을 통해 c++랑 join 한다 

- V8을 통해서 JS값을 C++ 값으로 바꿔준다
- libuv는 concurrency 등과같은 처리를 하는데 사용이된다. 
- 

# Event Loop
NodeJs로 프로그램을 작성하면 One Thread를 생성해서 EventLoop라는 걸 만들고 코드실행 

이벤트루프가 하는 일 수도코드
```js
// node myfile.js

const pendingTimers = []
const pendingOSTasks = []
const pendingOperations = []

myFile.runContents();

function shouldContinue(){
  // check one: Any pending setTimeout, setInterval, setImmediate?
  // check two: Any pending OS tasks? (listening to port)
  // check three: Any pending long running operations? (like fs module)
  return pendingTimers.length || pendingOSTasks.length || pendingOperations.length  
  
}
// Entire body executes in one 'tick'
while (shouldContinue()) {
  // 1.Node looks at pending Timers and sees if any functions are ready to be called. setTimeout, setInterval
  // 2. Node looks at pending OS tasks
  // 3. Pause execution. Continues whe...
  // - a new pendingOSTask
  // - a new pendingOperation
  // - a timer is about to complete
  
  // 4. Look at pendingTimers
  
  // 5. Handle any 'close' event
}



// exit back to terminal
```

<img width="441" alt="image" src="https://user-images.githubusercontent.com/39396725/226861430-8ebd6395-224c-4773-9d14-d75aab3d105b.png">

예를들어 pbkdf2 같은거 실행해보면 (2개 이상) 거의 동일한 시간에 실행되는걸 알 수 있다. 

몇개의 Standard library call 같은 경우에는, libuv가 expensive한 calculation을 결정해서 eventloop 바깥인, Thread Pool에서 진행된다. 
