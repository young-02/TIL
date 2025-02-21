# Hoisting(호이스팅)

호이스팅은 **자바스크립트 엔진이 실행하기 전에 변수와 함수 선언을 메모리에 먼저 올려놓는 과정**이다. <br>
즉 코드에서 변수를 선언하기 전에 사용할 수 있는 이유가 호이스팅 덕분이다.

## 1. 변수의 호이스팅

### (1) `var`의 호이스팅

```js
console.log(name); //undefined
var name = "Alice";
console.log(name); //Alice
```

- var name;이 코드 실행 전에 먼저 선언됨.
- 초기화(='Alice')는 그대로 남아 있음
- 그래서 console.log(name)를 실행하면 undefined가 출력됨.
  :white_check_mark: `var`는 선언만 호이스팅되고, 할당은 호이스팅되지 않는다..

### (2) `let`과 `const` 의 호이스팅

```js
console.log(name); // ReferenceError: Cannot access 'name' before initialization
let name = "Alice";
console.log(name); //Alice
```

- let과 const도 호이스팅 되지만 초기화 전에 접근 할수 없음
- Temporal Dead Zone(TDZ, 일시적 사각지대) 때문에 선언 전에 접근하면 오류 발생

```js
console.log(city); // ReferenceError: Cannot access 'city' before initialization
const city = "Seoul";
```

- 위 코드는 선언과 초기화가 분리되어 있음.
- 선언은 호이스팅되지만, 초기화는 호이스팅되지 않음.
- 따라서 선언 전에 참조하면 오류 발생.

## 2.함수의 호이스팅

### (1) 함수 선언문(function declaration)

```js
sayHello(); // 'hello'
function sayHello() {
  console.log("hello");
}
```

- 함수 선언문은 전체 코드 실행 전에 메모리에 올라간다.
- 선언 전에 호풀해도 정상적으로 실행된다.

### (2)함수 표현식(Function Expression)

```js
sayHi(); // ReferenceError: Cannot access 'sayHi' before initialization

const sayHi = function () {
  console.log("hi");
};
sayHi(); // 'hi'
```

- 함수 표현식은 변수 처럼 동작
- const sayHi 는 TDZ 때문에 선언 전에 접근이 불가능하다.

## 정리

| 선언 방식   | 호이스팅 여부           | 선언전 사용 가능 |
| ----------- | ----------------------- | ---------------- |
| var         | 선언만 호이스팅         | 값은 `undefined` |
| let         | 선언만 호이스팅         | TDZ로 오류 발생  |
| const       | 선언만 호이스팅         | TDZ로 오류 발생  |
| 함수 선언문 | 선언+정의 모두 호이스팅 | 정상 실행        |
| 함수 표현식 | 번수처럼 동작(TDZ)      | 오류 발생        |

- `var`는 선언만 호이스팅되고 undefined로 초기화된다
- `let`과 `const`는 선언되지만 초기화 전 접근불가(TDZ)
- 함수 선언문은 호이스팅되어 선언 전에 호출 가능!
- 함수 표현식은 변수처럼 동작하여 선언 전에 호출 불가!
-
