# Hoisting(호이스팅)

자바스크립트는 실행 전에 코드의 변수 선언과 함수 선언을 메모리에 먼저 할당한다.
그러나 변수의 초기화는 그대로 유지 되므로, 선언만 끌어올려지고 할당은 원래 위치에서 실행된다.

```js
console.log(a); // undefined
var a = 10;
console.log(a); //10
```

var a = 10; 은 내부적으로 아래와 같이 해서된다.

```js
var a; // 선언이 끌어올려짐 (Hoisting 발생)
console.log(a); // undefined(초기화는 원래 위치에서 진행)
a = 10;
console.log(a); //
```

즉, 변수 선언은 끌어올려지지만, 할당은 원래 자리에 남아 있기 때문에 undefined로 출력된다.

함수선언문은 전체가 호이스팅 되기 때문에 함수 호출을 선언 이전에 해도 정상적으로 실행된다.

```js
sayHello(); // 'hello'
function sayHello() {
  console.log("hello");
}
```

함수 표현식은 변수에 익명함수 (또는 화살표함수)를 할당하는 방식이라, 변수는 호이스팅되지만 함수 할당은 그대로 남아 있는다.

```js
sayHi(); // ReferenceError: Cannot access 'sayHi' before initialization

var sayHello = function () {
  console.log("hello");
};
```

아래와 같이 해석된다.

```js
var sayHello;
sayHello(); // ReferenceError: Cannot access 'sayHi' before initialization
sayHello = function () {
  console.log("hello");
};
```

변수 sayHello가 호스팅되었지만, 함수가 할당되기 전이므로 sayHello()를 호출하면 오류가 발생한다.

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

## 결론

자바스크립트에서 호이스팅은 변수와 함수의 선언이 해당 범위의 최상단으로 끌어올려지는 것처럼 동작하는 개념이다. `var`로 선언한 변수는 `undefined`로 초기화 상태에서 호이스팅되지만, `let`과 `const`는 TDZ(일시적 사각지대)에 걸려 초기화 전에는 참조 할 수 없다.
또한 함수 선언문은 호이스팅되지만, 함수 표현식은 변수만 호이스팅되고 함수 할당은 유지된다. 따라서 , `let`과 `const`를 사용하고 변수를 선언한 후에 사용 하는 것이 좋은 코드 스타일이다.
