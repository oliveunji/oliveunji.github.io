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

참고한 블로그: [https://yceffort.kr/2022/05/npm-vs-yarn-vs-pnpm](https://yceffort.kr/2022/05/npm-vs-yarn-vs-pnpm)

### 5. event-driven 아키텍쳐란?
Event-driven 아키텍쳐는 이벤트를 생성하는 이벤트 생성자(event producer)와 이를 구독하는 이벤트 소비자(event consumer)로 구성된다.  

![image](https://user-images.githubusercontent.com/39396725/199005328-5ba0c4f7-c36e-4997-a88a-c4f73b62468d.png)

이벤트는 실시간으로 전달되며 이벤트 소비자들은 이벤트가 일어나면 즉각 반응할 수 있다. 또한 이벤트 생성자는 소비자로부터 분리될 수 있고, 각 소비자들 또한 서로를 모른다. 
이벤트 기반 아키텍쳐는 pub/sub 모델과 event stream 모델로 분리된다. 

#### 이 아키텍쳐는 다음과 같은 경우에 사용된다. 
- 여러개의 하부 시스템이 같은 이벤트 처리해야 할때
- 실시간 프로세싱 경우
- 복잡한 이벤트 프로세싱 (ex 패턴 매칭 등)의 경우
- IoT와 같은 많은 양의 데이터가 들어오는 경우

#### 장점
- Producer와 Consumer가 decouple됨
- point-to-point 통합이 필요없음. (즉 새로운 consumer 추가가 용이)
- consumer는 이벤트 받자마자 응답 가능
- 확장이 용의, 분산이 쉬움
- subsyste은 이벤트 스트림에 대해 독립적인 view 가질 수 있음

#### 어려운점
- 이벤트 deliver 보장
- 이벤트가 순서대로 처리됨을 보장하거나, 딱 한번만 처리된 것을 보장하는 것이 어려움 

참조한 링크: [https://learn.microsoft.com/en-us/azure/architecture/guide/architecture-styles/event-driven](https://learn.microsoft.com/en-us/azure/architecture/guide/architecture-styles/event-driven)

### 6. Promise에 대해 설명
Promise란 JavaScript 비동기 처리에 사용되는 객체이다. 
Promise는 다음과 같이 3가지 상태를 가진다. 
- Pending(대기) : 비동기 처리 로직이 아직 완료되지 않은 상태
- Fulfilled(이행) : 비동기 처리가 완료되어 프로미스가 결과 값을 반환해준 상태
- Rejected(실패) : 비동기 처리가 실패하거나 오류가 발생한 상태


```js
function getData() {
  return new Promise(function(resolve, reject) {
    $.get('url 주소/products/1', function(response) {
      if (response) {
        resolve(response);
      }
      reject(new Error("Request is failed"));
    });
  });
}

// 위 $.get() 호출 결과에 따라 'response' 또는 'Error' 출력
getData().then(function(data) {
  console.log(data); // response 값 출력
}).catch(function(err) {
  console.error(err); // Error 출력
});
```

#### Async/Await 과 Promise의 차이?
Async/Await은 Promise의 Syntatic Sugar일 뿐이다. Async/Await으로 작성하면 비동기 요청을 동기? 처럼 보이게 작성할 수 있어서 코드에 대한 가독성이 좋아져서 코드 이해가 쉬워진다.  

참고한 링크
- [https://joshua1988.github.io/web-development/javascript/promise-for-beginners/](https://joshua1988.github.io/web-development/javascript/promise-for-beginners/)
- [https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Promises#async_and_await](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Promises#async_and_await)

7. node.js의 장단점
8. 콜백지옥 해결방안에 대해 설명
9. Single Threaded Async란?
10. 비동기 처리 Promise와 async/await의 차이?
11. REST API 에 대해 설명
### 12. OOP란?
객체지향 프로그래밍(Object Oriented Programming) 이란 컴퓨터 프로그래밍 패러다임중 하나로 프로그램을 명령어의 목록으로 보는 시각에서 벗어나 객체들의 모임으로 파악한다. 각각의 객체는 메세지를 주고받고 데이터를 처리할 수 있다. 

객체지향 프로그래밍은 프로그램을 유연하고 변경이 쉽게 만들기 때문에 대규모 소프트웨어 개발에 많이 사용된다. 
객체 지향 프로그래밍의 특징은 기본적으로 자료추상화, 상속, 다형개념, 동적 바인딩등이 있으며 다중상속등의 특징이 존재한다. 
소프트웨어 공학의 관점에서 좋은 SW를 만들기 위해 강한 응집력과 약한 결합력을 지향해야 하는데 OOP는 이를 가능하게 한다. 

13. GET, POST 차이
### 14. Node.js가 무엇인가요?
확장성있는 네트워크 애플리케이션 개발에 사용되는 소프트웨어 플랫폼이다. JavaScript 언어를 사용하며, 논블로킹 I/O와 단일 이벤트 스레드 루프를 통한 높은 처리 성능을 가지고 있다. (싱글스레드 논블로킹 모델) 
하나의 스레드지만 비동기 입출력을 통해 각각의 요청들을 서로 블로킹 하지 않는다. 

15. Node.js 사용해야 하는 이유
16. Node.js의 동작원리
17. I/O 논블로킹이란?
18. 웹 서버가 무엇인가요?
### 19. Arrow Function 이란 무엇인지 설명해주실 수 있을까요?
함수형 표현의 간결한 표현법. 다만 몇가지 차이점을 가진다. 
- this, arguments, super과 같은 own bindings를 가지지 않는다. 
- constructor로 사용될 수 없다. 
- yield를 사용할 수 없다. 
20. 38. ‘==’와 ‘===’ 연산자의 차이는 무엇인지 설명해주실 수 있을까요?
21. 깊은 복사와 얕은 복사의 차이는 무엇이고 JS에서 각각을 구현하는 방법은 어떻게 되
는지 설명해주실 수 있을까요?
22. JS의 passed by value 와 passed by reference 에 대해 아는 만큼 설명해주실 수 있을
까요?
23. 고차 함수란 무엇인지 설명해주실 수 있을까요?
24. 다음 함수의 결과의 예측과 근거를 설명해주실 수 있을까요?
```js
var obj1 = { address : "Seoul, Korea", getAddress: function(){
console.log(this.address); } } var getAddress = obj1.getAddress; var obj2
= { name:"Minji", getAddress }; obj2.getAddress();
```
25. Express란 무엇이고 왜 필요하며 대안은 무엇이 있는지 설명해주실 수 있을까요?
26. npm 이란 무엇인지 설명해주실 수 있을까요?
27. 웹 서버란 무엇인지 NGiNX와 Apache를 비교하여 설명해주실 수 있을까요?
28. JWT란 무엇인지 설명해주실 수 있을까요?
### 29. 트랜스파일러와 번들러에 대해 설명해주실 수 있을까요? 
#### 모듈 번들러
여러 개로 나뉘어져 있는 JS파일을 하나의 “Javascript Bundle”파일로 만들어준다. (의존성 처리)
모듈 번들러가 없으면 수동으로 파일을 결합하거나 수많은 <script>태그를 사용하여 자바 스크립트를 HTML로 로드해야 한다.

:heavy_check_mark: 번들러 없을때 단점
- 필요한 코드와 적절한 로드 순서를 추적해야한다.
- <script>태그가 여러 개인 경우 서버 호출이 많아져 성능이 저하된다.
- 수많은 수작업이 필요하다.

번들러를 이용하여 결합, 축소 (코드를 더 작고 효율적으로), 코드 분할 (초기 로드시간을 축소) 및 Javascript를 로드하는 프로세스를 자동화한다. 번들러로는 Webpack, Parcel, Rollup 등이 있다.
  
#### 트랜스파일러
트랜스파일링(Transpiling)이란 어떤 특정 언어로 작성된 소스 코드를 다른 언어의 소스 코드로 변환하는 것을 말한다.
이를 해주는 것이 트랜스파일러(Transpiler)이다. 트랜스파일러가 필요한 이유는 지원하지 않는 언어를 지원하는 다른 언어로 변환하기 위해서 이다.

:heavy_check_mark: 트랜스파일러의 기능
- ES6+의 기능을 ES5 코드로 변환
- 리액트의 JSX를 자바스크립트 코드로 변환
- 타입스크립트를 자바스크립트로 변환
- sass를 CSS로 변환 등등..

ES6+나 JSX를 변환시키는 트랜스파일러로는 바벨(Babel)이 있으며 타입스크립트를 변환시키는 도구로는 타입스크립트 트랜스파일러가 있다. 보통 모듈 번들러에 트랜스파일러를 추가해서 사용하는 방식을 사용한다.
