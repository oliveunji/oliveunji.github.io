---
layout: default
title: Getting Started
parent: TypeScript
grand_parent: Tech
description: "Getting_Started"
permalink: /tech/typescript/getting-started
---

TypeScript에서 컴파일에 실패한 코드는 js 생성하지 못하게 하는 옵션 + 변화가 있을때 계속 재컴파일 하는 옵션
```ts
tsc --noEmitOnError test.ts --watch
```

### Type Inference
개발자가 변수의 타입을 명시하지 않아도 컴파일러가 추측? 해서 타입을 지정해주는 것. 
### Type Annotation이 필요한 경우?
함수를 생성할때..

TypeScript는 Static Type System이고 JavaScript는 Dynamic Type System이다. 

### TypeScript Optional Chaining
해당 변수가 값이 존재할때만 접근하게끔 하는것
```ts
course?.textFields?.title 
```

### TypeScript Null Coalescing 
```ts
const title = course?.textFields?.title : "No title found"
```

### noImplictAny 옵션
```ts
tsc --noImplicitAny 06-any-type.ts
```

### Union TYpes
```ts
let uniqueIdentifier: number | string
uniqueIdentifier = "e7b59f38-60d6-11ed-9b6a-0242ac120002"

const keys: (number | string)[] = [1000, ""]

let courseId: number | null = 1000; 
// optional 값인 경우 
```

사실 기본적으로 typescript 변수들은 Nullable 이다. strict 하게 null체크를 하고 싶으면 다음의 옵션을 사용하면 된다. 
```ts
tsc --strictNUllChecks test.ts
```

### Not Null Assertion Operator 하는 방법 (컴파일타임에 에러 무시) 
```ts
let courseId : number | null;
courseId!.toString();
```

### Type Aliases
```ts
type CourseStatus = "draft" | "published" | "unpublished" | "archived";
let courseStatus : CourseStatus = "draft" 
```

### TypeScript Interfaces
같은 형태의 타입의 값을 여러번 생성하고 싶을떄 사용
```ts
interface Course {
    title: string;
    readonly substitle: string;
    lessonsCount?: number;

const course: Course{
    title: "bootcamp",
    subtitle: "learn fundamentals",
    lessonsCount: 10 
};

course.title = "hello world"
```

### TypeScript Aliases vs Interfaces
Interfaces를 사용하는 것을 추천. 
대게 aliases를 사용하는 경우는 간단하게 union fixed type? 정할떄? 사용??
Interfaces는 extend가 가능하다. 

### TypeScript Type Assertions
```ts
const input = document. getElementById("input-field) as HTMLInputElement;

```

### 익명함수와 일반 function의 차이
다음의 함수의 결과물은
<img width="659" alt="image" src="https://user-images.githubusercontent.com/39396725/201500547-c4a62b2f-1d11-4992-ac43-2c82334c2cde.png">
Unkwon이 출력되지 않는다. 왜냐면 익명함수는 따로 private context를 생성하지 않기 때문.
<img width="677" alt="image" src="https://user-images.githubusercontent.com/39396725/201500571-24b05dea-22ef-4ec2-92cd-02f9de8020ce.png">
Unkwon이 출력된다. function 때문에 it's own private context를 생성하기 때문. 

### Deep Copy vs Shallow Copy
<img width="428" alt="image" src="https://user-images.githubusercontent.com/39396725/201500798-b5ac3e6d-4988-4188-9b71-b7297e09f513.png">
다음 코드의 결과물은 newCourse의 lessonCount가 영향받지 않았을것이다. (Deep Copy 되었기 때문) 

<img width="854" alt="image" src="https://user-images.githubusercontent.com/39396725/201500855-eadc2a07-7df5-4d36-8698-25f59b655883.png"> 
이 경우는 Shallow copy이기 때문에 lessonCount가 100으로 바뀐다.

위의 결과물은 다음의 결과물과 동일하다. (Spread operator 사용)
<img width="619" alt="image" src="https://user-images.githubusercontent.com/39396725/201500895-fb9ae2a9-ba97-4fb2-953d-18d7801a26e0.png">

Deep Copy를 편하게 하고 싶으면 clone-deep과 같은 package를 사용하면 된다. 

### TypeScript 디버그 방법
<img width="922" alt="image" src="https://user-images.githubusercontent.com/39396725/201502470-e6c9aaf9-314f-4bbc-ab44-a11202f79330.png">
Source Map 사용하면 ts 파일로 디버깅 가능하다. (--sourceMap)

