# 동기(Synchronous)와 비동기(Asynchronous)프로그래밍

자바스크립트는 기본적으로 단일 스레드(Single-thread)기반으로 동작하는 언어
한 번에 한줄의 코드만 실행할 수 있어, 모든 작업을 동기적으로 실행하면 웹사이트가 느려지거나 멈출 수 있기 때문에,이를 해결하기 위해 비동기 프로그래밍이 사용된다.

## 1. 동기 프로그래밍(Synchronous programming)

동기 프로그래밍에서는 코드가 위에서 아래로 차례대로 실행된다.
하나의 작업이 끝나야 다음 작업이 실행되기 때문에 실행 순서를 예측하기 쉽다는 장점이 있다.
하지만 시간이 오래 걸리는 작업이 있을 경우 프로그램이 멈춘 것처럼 보일 수 있다는 단점이 있다.

```js
console.log("A 작업 시작");
console.log("B 작업 실행");
console.log("C 작업 실행");

// A 작업 시작
// B 작업 실행
// C 작업 실행
```

코드가 순서대로 실행된다.

### 동기 작업이 오래 걸릴 경우 문제 발생

```js
console.log("A 작업 시작");

function longTask() {
  for (let i = 0; i < 1e9; i++) {}
  console.log("긴 작업 완료");
}

longTask();
console.log("B 작업 실행");

// A 작업 시작
// 긴 작업 완료
// B 작업 실행
```

longTask()가 실행되는 동안 다른 작업이 블로킹되어 B작업이 늦게 실행됨

## 2. 비동기 프로그래밍(Asynchronous programming)

비동기 방식에서는 하나의 작업이 끝날 때까지 기다리지 않고, 다음 작업을 실행한다.
작업이 지연되더라도 프로그램이 멈추지 않고 실행될 수 있다.

```js
console.log("A 작업 시작");

setTimeout(() => {
  console.log("B 작업 3초후에 실행");
}, 3000);
console.log("C 작업 실행");
// A 작업 시작
// C 작업 실행
// B 작업 3초후에 실행
```

`setTimeout`을 사용하면 B작업이 예약된 상태에서 C작업이 먼저 실행된다.

## 3. 비동기 프로그래밍을 다루는 방법

- 콜백(Callback)
- 프로미스(Promise)
- async/await

### (1) 콜백함수(Callback)

특정작업이 끝난 후 실행되는 함수
여러개의 비동기 작업을 콜백으로 처리하면 코드가 너무 복잡해지는 콜백헬(Callback Hell) 문제가 생길 수 있다.

```js
function fetchData(callback) {
  setTimeout(() => {
    console.log("데이터가져오기");
    callback();
  }, 2000);
}

fetchData(() => {
  console.log("콜백실행:데이터 처리 완료");
});

//2초후 데이터 가져오기
// 콜백실행:데이터 처리 완료
```

fetchData 작업이 끝난후 callback()이 실행된다

### (2) 프로미스(Promise)

`Promise`는 비동기 작업의 성공(resolve)와 실패(reject)를 처리하는 객체이다.
콜백보다 가독성이 좋고, 체이닝(then,catch)을 이용해 순차적으로 실행이 가능하다.

```js
function fetchData() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve("데이터 가져오기 성공");
    }, 2000);
  });
}

fetchData()
  .then((data) => {
    console.log(data);
  })
  .catch((error) => {
    console.log("오류발생", error);
  });

//2초후 데이터 가져오기 성공
```

### (3) async/await

async/await는 Promise를 더 쉽게 사용할 수 있도록 도와주는 문법이다.
비동기 코드도 동기 코드처럼 작성할 수 있어서 가독성이 좋다.

```js
function fetchData() {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve("데이터 가져오기 성공");
    }, 2000);
  });
}

async function getData() {
  const result = await fetchData();
  console.log(result);
}

getData();

//2초후 데이터 가져오기 성공
```

## 4. 비동기 프로그래밍 사용

### (1)네트워크 요청(API호출)

웹에서 데이터를 가져오는 경우, 서버 응답을 기다리는 동안 다른작업을 해야 하기 때문에 비동기 처리가 필수이다.

```js
async function getUserData() {
  const response = await fetch("https://jsonplaceholder.typicode.com/users");
  const data = await response.json();
  console.log(data);
}

getUserData();
```

### (2) 타이머(setTimeout, setInterval)

```js
function timer() {
  console.log("타이머 실행");
}

setTimeout(timer, 2000);

//2초후 타이머 실행
```

### (3) 이벤트 핸들링

사용자의 클릭, 키 입력 등의 이벤트는 언제 발생할지 모르기 때문에 비동기 적으로 처리된다.

```js
document.addEventListener("click", () => {
  console.log("클릭 이벤트 발생");
});
```

### 정리

||동기(synchronous)|비동기(Asynchronous)|
|실행방식|순차적으로 실행됨|다른작업과 동시에 실행가능|
|작업차단여부|하나의 작업이끝날때 까지 기다린 다음 작업 대기|대기하지 않고 다음 작업 실행|
|예제|일반적인 코드 실행 |네트워크요청, 이벤트 핸들링 setTimeout등|
|문제점| 시간이 오래 걸리는 작업이 있으면 프로그램이 멈출 수 있음
| 콜백헬(Callback Hell) 문제 발생 가능|
