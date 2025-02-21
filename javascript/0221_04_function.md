# 함수 (function)

함수는 특정 작업을 수행하는 코드 블록이다.
재사용이 가능하고 코드의 가독성을 높이며, 유지보수를 쉽게 해준다.

## 1. 함수 선언

typeScript에서는 여러받식으로 함수를 선언할 수 있다.

### (1) 함수 선언문(function declaration)

```js
function greet(name: string): string {
  return `Hello, ${name}`;
}

console.log(greet("Alice")); //Hello, Alice
```

- function 키워드를 사용하여 선언
- **호이스팅(hoisting)**이 적용됨(함수를 선언하기 전에 호출가능)

### (2) 함수 표현식(Function Expression)

```js
const greet = function (name: string): string {
  return `Hello, ${name}`;
};

console.log(greet("Bob")); //Hello, Bob
```

- 변수에 익명 함수를 할당
- 호이스팅이 적용되지 않음(선어 전에 호출 불가)

### (3) 화살표함수 (Arrow Function)

```js
const greet = (name: string): string => `Hello, ${name}`;

console.log(greet("Charlie")); //Hello, Charlie
```

- 함수 선언문을 더 간결하게 표현
- 호이스팅이 적용됨
- this 바인딩이 없음

## 2. 함수의 매개변수

함수는 매개변수(parameter)를 받을 수 있고, 다양한 방식으로 정의할 수 있다.

### (1) 기본값 설정(Default Parameter)

```js
function greet(name: string = "Guest"): string {
  return `Hello, ${name}`;
}

console.log(greet()); //Hello, Guest
console.log(greet("Alice")); //Hello, Alice
```

- 매개변수에 값이 없으면 기본값 이 사용됨.

### (2) 선택적 매개변수(Optional Parameter)

```js
function introduce(name: string, age?: number): string {
  return age
    ? `${name} is ${age} years old`
    : `${name} prefers not to say their age`;
}

console.log(introduce("Bob")); //Bob prefers not to say their age
console.log(introduce("Alice", 30)); //Alice is 30 years old
```

- 매개변수 뒤에 `?`를 붙여 선택적으로 사용
- 값이 없으면 `undefined`로 처리

### (3) 나머지 매개변수(Rest Parameter)

```js
function sum(...numbers: number[]): number {
  return nubers.reduce((acc, curr) => acc + curr, 0);

  console.log(sum(1, 2, 3, 4, 5));
}
```

- `...numbers` -> 여러 개의 값을 배열로 받아서 처리

## 3. 함수의 반환값(return type)

### (1) 반환 타입 지정

```js
function add(a: number, b: number): number {
  return a + b;
}
console.log(add(1, 2)); //3
```

- `:number`->반환값이 숫자임을 명시

### (2) 반환값이 없는 함수(void)

```js
function logMessage(message: string): void {
  console.log(message);
}

logMessage("Hello, TypeScript!"); //Hello, TypeScript!
```

- `void` -> 반환값이 없음을 명시

### (3) 함수의 반환값이 여러개인 경우(튜플 사용)

```js
function getUserInfo(): [string, number] {
  return ["Alice", 25];
}

const [name, age] = getUserInfo();
console.log(name); //Alice
console.log(age); //25
```

- 튜플(Tuple)을 사용하여 여러 개의 값을 반환

## 4. 함수의 `this` 문제(일반함수 vs 화살표 함수)

### (1)일반함수의 `this`

```js
const person = {
  name: "Alice",
  sayHello: function () {
    console.log(`Hello, my name is ${this.name}`);
  },
};
person.sayHello(); //Hello, my name is Alice
```

- `this`는 호출한 객체(person)를 참조

### (2) 화살표 함수의 `this`

```js
const person = {
  name: "Bob",
  sayHello: () => {
    console.log(`Hello, my name is ${this.name}`);
  },
};
person.sayHello(); //`Hellos, my name is undefined`
```

- 화살표 함수는 `this`를 부모 스코프에서 가져옴
- 객체에서 `this`를 사용할 때는 일반 함수를 쓰는게 안전함

## 5. 함수의 오버로딩(Function Overloading)

typeScript에서는 같은 이름의 함수를 여러방식으로 사용할 수 있다.

```js
function getInfo(value: string | number): string {
  return typeof value === "number" ? `Age:${value}` : `Name:${value}`;
}
console.log(getInfo(25)); //Age:25
console.log(getInfo("Alice")); //Name:Alice
```

- 함수의 매개변수 타입과 반환값을 다양하게 정의할 수 있음
- 오버로딩은 함수의 이름은 같지만 매개변수의 타입과 개수가 다른 함수를 여러개 선언하는 것

## 정리

| 기능             | 설명                   | 예제                           |
| ---------------- | ---------------------- | ------------------------------ | --------------- |
| 함수 선언문      | `function` 키워드 사용 | function greet(name){}         |
| 함수 표현식      | 변수에 익명 함수 할당  | const greet = function(name){} |
| 화살표 함수      | `=>` 사용              | const greet = (name) => {}     |
| 기본 값 매개면수 | 기본값 제공            | function fn(name = "Guest"){}  |
| 선택적 매개변수  | `?` 사용               | function fn(name?){}           |
| 나머지 매개변수  | `...`사용              | function fn(...args){}         |
| 반환값 지정      | `:type`사용            | function fn():number{}         |
| 오버로딩         | 여러 개 함수 정의      | function fn(value:number       | string):string; |
