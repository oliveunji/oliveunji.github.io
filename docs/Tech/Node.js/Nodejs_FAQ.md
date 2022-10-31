---
layout: default
title: Nodejs_FAQ
parent: Node.js
grand_parent: Tech
description: "Nodejs_FAQ"
permalink: /tech/node-js/node-js-faq
---

## Node.js 50문 50답 
### 1. var, let, const 차이
JavaScript에서 변수선언시 var, let, const를 이용하여 할 수 있으며 (ES6에서 const와 let이 추가됨) 변수선언은 **선언-> 초기화** 단계를 거쳐서 수행된다. 
변수 선언은 런타임에서 되지 않고, 그 이전단계에서 먼저 실행되어, 변수선언을 포함한 모든 선언문이 먼저 실행되는 특징을 가지며, 이를 **호이스팅(hoisting)** 이라한다.
변수는 새로운 값을 재할당 할 수 있지만, const(상수)로 선언된 것은 재할당 할 수 없다. 
var의 경우 전역 레벨로 정의된 이후에는 값을 어디서 바꾸는 바뀐게 전역으로 정의되기 때문에 혼동이 올 수 있다. 
```js
var a = 1

if (true) {
  var a = 5
}

console.log(a) // output: 5
```
var의 문제점
- 변수 중복 선언 - 변수 중복 선언이 가능하며, 예기치 못한 값을 반환할 수 있다
- 블록레벨 스코프 - 함수레벨 스코프로 인해 함수 외부에서 선언한 변수는 모두 전역 변수로 된다
- 변수호이스팅 - 변수 선언문 이전에 변수를 참조하면 언제나 undefined를 반환한다.

let과 const가 개선한 부분 
- 변수중복선언 
    - let 키워드로는 변수 중복 선언이 불가능하지만, 재할당은 가능하다
    - const는 선언과 초기화를 동시에 진행해야 하며, 재선언 불가하고 재할당의 경우 원시값은 불가하지만, 객체는 가능하다. 
        ```js
        // 원시값의 재할당
        const name = 'kmj'
        name = 'howdy' // output: Uncaught TypeError: Assignment to constant variable.

        // 객체의 재할당
        const name = {
          eng: 'kmj',
        }
        name.eng = 'howdy'

        console.log(name) // output: { eng: "howdy" }
        ```
- 블록레벨 스코프
    - let, const 키워드로 선언한 변수는 모두 코드블록을 지역 스코프로 인정하는 블록레벨 스코프를 따른다.
        ```js
        let a = 1

        if (true) {
          let a = 5
        }

        console.log(a) // output: 1
        ```
- 변수 호이스팅 
    - let 키워드로 선언한 변수는 **선언 단계와 초기화 단계가 분리되어 진행** 된다.
    - const 키워드는 **선언 단계와 초기화 단계가 동시에 진행** 된다. 

참고한 블로그: https://www.howdy-mj.me/javascript/var-let-const

### 2. Event Loop란?
JavaScript는 Single Thread 이다. 근데, Event Loop를 사용하면, non-blocking i/o가 가능하다. 
ECMAScript에는 사실 이벤트 루프가 없다. 브라우저나, Node.js에 이벤트 루프가 존재한다. 
JavaScript는 SingleThread 기반의 언어인데 Non blocking i/o와 비동기 통신이 가능한 이유는 event loop가 있어서, 당장 실행할 수 없는 코드는 task queue에 넣어 두었다가
실행가능한 순간이 오면 이때 task queue에서 순차적으로 하나씩 꺼내서 실행한다.
그리하여, 비동기 코드가 존재하거나, setTimer 코드가 존재하면 일단 실행을 건너띄고, 바로바로 처리해야 하는 것들 처리한 이후에 실행된다.
(이러한 이유 떄문에 setTimer에 설정한 몇초뒤 실행 -> 이러한 코드는 설정한 시간 직후에 실행되는 것을 보장하지 않는다. 
<img width="554" alt="image" src="https://user-images.githubusercontent.com/39396725/198592635-60db6794-02fc-486d-81b0-86017588fb53.png">

참고영상: [https://www.youtube.com/watch?v=8aGhZQkoFbQ](https://www.youtube.com/watch?v=8aGhZQkoFbQ)

### 3. Express 의 역할 
Node.js는 JavaScript로 서버사이드 애플리케이션 개발을 가능하게 하는 런타임 환경이다. 즉, 컴퓨터에서 파일을 읽어올수도 있고, 어떤 요청이 들어오면 연산할 수도 있다.
근데 Node.js 자체가 웹서버를 만들기 위해 특화되서 작성된 언어는 아니기 때문에, Node.js로만 웹서버 만들려면 만들수는 있겠지만 번거롭다.
Express는 Node.js 개발자들에게 가장 유명한 **웹 프레임워크** 이며 다음과 같은 기능을 제공한다. 
- HTTP 통신 요청(Request; GET, POST, DELETE 등)에 대한 핸들러를 만든다.
- 템플릿에 데이터를 넣어 응답(response)을 만들기 위해 view의 렌더링 엔진과 결합(integrate)한다.
- 접속을 위한 포트나 응답 렌더링을 위한 템플릿 위치같은 공통 웹 어플리케이션 세팅을 한다.
- 핸들링 파이프라인(reqest handling pipeline) 중 필요한 곳에 추가적인 미들웨어 처리 요청을 추가한다.

### 4. npm과 yarn 각각에 대한 설명
Npm은 node package manager의 약자로, node에서 사용하는 각종 라이브러리들을 편리하게 다운받고 버전관리, 의존성 관리등을 도와주는 도구이다.
근데 어느날 혜성같이 등장한 yarn! 어떤 부분을 보충하기 위해 등장했을까?
2016년, 페이스북은 구굴과 몇몇 다른 개발자들과 함께 npm이 가지고 있었던 일관성, 보안, 성능 문제들을 해결하기 위해 새로운 패키지 매니저를 만드려는 시도중이란 발표를 했다 -> 그것이 바로 yarn (classic)

그 이후로도 npm 및 yarn classic의 근본적인 문제를 해결하기 위해 (flat하게 node modules를 관리하는 것, 성능 및 디스크 관리의 효율성) 때문에 yarn berry와 pnpm이 등장하였다.

하지만 가장 범용적으로 쓰이고, 많은 개발 문서에 안내되어있는 package manager는 여전히 npm 이니 이제 막 node.js를 시작하는 개발자라면 npm 을 사용하는것이 나쁘지 않은 선택지라고 본다. 

5. event-driven programming이란?
6. Promise에 대해 설명
7. node.js의 장단점
8. 콜백지옥 해결방안에 대해 설명
9. Single Threaded Async란?
10. 비동기 처리 Promise와 async/await의 차이?
11. REST API 에 대해 설명
12. OOP란?
13. GET, POST 차이
14. Node.js가 무엇인가요?
15. Node.js 사용해야 하는 이유
16. Node.js의 동작원리
17. I/O 논블로킹이란?
18. 웹 서버가 무엇인가요?
19. 
