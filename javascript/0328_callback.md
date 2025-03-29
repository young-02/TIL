# 콜백함수(callback)

콜백 함수는 다른 함수에 인자로 전달되어 나중에 실행되는 함수를 의미한다.<br>
어떤 함수가 실행된 후 특정 시점에서 호출되는 함수를 말한다.

## 콜백함수를 사용하는 이유

### 1. 비동기 작업 처리

- javascript는 기본적으로 단일 스레드로 동작한다. 한번에 하나의 작업만 실행할 수 있다.
- 네트워크 요청, 파일 읽기, 타이머 같은 작업은 실행하는 데 시간이 걸리기 때문에 , 동기적으로 실행하면 프로그램이 멈취 버릴 수도 있다.
- 그래서 비동기 작업이 끝난 후 실행될 함수를 콜백 함수로 전달하여 나중에 실행되도록 하는 것이다.

### 2. 코드의 재사용성과 유연성 증가

- 콜백 함수는 특정 동작을 나중에 실행하도록 추상화할 수 있어서 같은 함수가 다양한 상황에서 재사용 될수 있다.

### 함수형 프로그래밍 스타일 지원

- javascript에서 함수는 일급 객체로 취급하기 때문에, 함수 자체를 인자로 잔달 할수 있다.
- 이를 활용하면 더 간결하고 가독성이 좋은 코드 작성이 가능하다.

## 예제

### 1.기본적인 콜백 함수

```js
function greet(name, callback) {
  const message = `Hello, ${name}`;
  callback(message);
}

function printMessage(message) {
  console.log(message);
}

// greet 함수가 실행된 후  printMessage가 호출됨.
greet("Alice", printMessage);
```

- greet 함수는 name을 받아서 메세지를 만든 후, 콜백함수을 실행 하는 구조이다.
- printMessage 가 callback으로 전달되어 나중에 실행되도록 되어 있다.

### 2.비동기 작업에서 콜백함수 사용

콜백 함수는 주로 비동기 작업에서 많이 사용된다. setTimeout은 일정 시간이 지난 후 실행할 코드를 콜백 함수로 전달한다.

```js
console.log("start");
setTimeout(() => {
  console.log("callback function execution after 2 seconds");
}, 2000);

console.log("End");
```

- setTimeout은 2초 후에 콜백 함수를 실행하지만, 그동안 javascript는 setTimeout아래 코드를 계속 실행한다.
- 따라서 End가 먼저 출력되고, 2초 뒤에 callback function execution after 2 seconds가 출력된다.

### 3. 콜백 지옥(Callback Hell)

콜백 함수를 중첩해서 사용하다 보면 코드가 너무 깊어지는 문제가 발생할 수 있다. 이를 콜백 지옥이라고 한다.

```js
function first(callback) {
  setTimeout(() => {
    console.log("첫번째");
    callback();
  }, 1000);
}

function second(callback) {
  setTimeout(() => {
    console.log("두번째");
    callback();
  }, 1000);
}

function third(callback) {
  setTimeout(() => {
    console.log("세번째");
    callback();
  }, 1000);
}

first(() => {
  second(() => {
    third(() => {
      console.log("모든 작업 완료!");
    });
  });
});

// 1초후에 첫번째
// 1초후에 두번째
// 1초후에 세번째
// 이후 모든 작업 완료!
```

- 콜백 함수가 중첩되면서 코드가 들여쓰기가 깊어지고 가독성이 떨어진다.
- 이를 해결 하기 위해 promise나 async/await를 사용한다.

## 콜백함수 단점 해결 방법

### 1.promise

```js
function first() {
  return new Promise((resolve) => {
    setTimeout(() => {
      console.log("첫번째");
      resolve();
    }, 1000);
  });
}

function second() {
  return new Promise((resolve) => {
    setTimeout(() => {
      console.log("두번째");
      resolve();
    }, 1000);
  });
}

function third() {
  return new Promise((resolve) => {
    setTimeout(() => {
      console.log("세번째");
      resolve();
    }, 1000);
  });
}

first()
  .then(() => second())
  .then(() => third())
  .then(() => console.log("모든 작업 완료!"));
```

- Promise를 사용하면 중첩된 콜백을 피하고, .then()체이닝을 통해 가독성을 높일 수 있다.

### 2. async/await

```js
async function runTask() {
  await first();
  await second();
  await third();
  console.log("모든 작업 완료");
}

runTask();
```

- async/await을 사용하면 코드가 동기적으로 실행되는 것처럼 보이면서도 비동기적으로 동작하기때문에 가독성이 좋아진다.
