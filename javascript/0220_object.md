# 객체

객체(object)는 프로그래밍에서 데이터를 구조화하는 핵심 개념중 하나다.
객체는 **"속성과 동작을 함께 묶은 데이터 구조"** 라고 생각하면된다.

## 1.객체란?

객체는 키(key)와 값(value)의 쌍으로 이루어진 데이터의 모음이다.
javascript에서는 `object` 타입으로 구현된다.

```javascript
const person = {
  name: "Alice",
  age: 25,
  greet: function () {
    console.log(`Hello, my name is ${this.name}`);
  },
};
```

- `name` 과 `age는` 속성(property)이고
- `greet()`는 메서드(method)이다.
  즞 객체는 단순한 데이터의 집합이 아니라, 상태(데이터)와 행동(메서드)을 포함할 수 있는 구조이다.

## 2.객체 특징

### 1) 동적 속성 추가/ 삭제 가능

```javascript
const person = { name: "Alice" };
person.age = 25; // 새로운 속성 추가
delete person.name; //속성 삭제

console.log(person); //{age:25}
```

javascript 객체는 **런타임에 속성을 추가하거나 삭제할 수 있다.**
:rocket: 런타임(RunTime)-> 프로그램이 실제로 실행되는 시간

### 2) 객체 참조 타입

객체는 메모리에서 참조(reference)로 저장된다.
즉, 객체를 변수에 할당하면 **그 값이 아니라 메모리 주소(참조값)을 가리킨다**는 의미이다.

```javascript
const obj1 = { value: 10 };
const obj2 = obj1; // obj2가 obj1을 참조

obj2.value = 20; //obj2를 수정하면 obj1도 변경된다.
console.log(obj1.value); // 20
```

객체를 복사하면 같은 데이터를 공유하기 때문에 **한 곳에서 값을 변경하면 원본도 변함**

:white_check_mark: 객체 복사 방법 (깊은 복사 vs 얕은 복사)
객체를 독립적으로 사용하려면 깊은 복사(deep copy)를 해야한다.

```javascript
const obj1 = { value: 10 };
const obj2 = { ...obj1 }; // 새로운 객체 생성(얕은 복사)

obj2.valule = 20;
console.log(obj1.value); // 10
```

깊은 복사(Deep Copy)는 `JSON.parse(JSON.stringify(obj))` 또는 `structuredClone(obj)` 방법으로 복사한다.

### 3) 객체의 주요 접근 방식

(1)점표기법(.)

```javascript
const person = { name: "Alice", age: 25 };
console.log(person.name); // Alice
```

(2) 대괄호 표기법([])

```javascript
const key = "name";
console.log(person[key]); // Alice
```

## 3. 객체 관련 주요 기능

### (1) Object.keys(), Object.values(), Object.entries()

객체에서 키, 값, [키,값]배열을 얻을 수 있다.

```js
const obj = { a: 1, b: 2, c: 3 };
console.log(Object.keys(obj)); // ['a','b','c']
console.log(Object.values(obj)); //[1,2,3]
console.log(Object.entries(obj)); //[['a',1],['b',2],['c',3]]
```

### (2) Object.assign() (객체병합)

객체를 합칠 때 사용한다.

```js
const obj1 = { a: 1 };
const obj2 = { b: 2 };
const merged = Object.assign({}, obj1, obj2);
```

**전개 연산자(...)**

```js
const merged = { ...obj1, ...obj2 };
```

### (3) 객체 Map으로 변환

객체는 일반적인 키 - 값 저장소지만, `Map`은 보다 **유연한 데이터 구조**이다.

```js
const obj = { name: "Alice", age: 25 };
const map = new Map(Object.entries(obj));

console.log(map.get("name")); // Alice
```

`Map`은 `Object`보다 더 다양한 키 타입을 지원해 (객체, 배열도 가능).

## 4. 객체 생성 방법

### 1. 객체 리터럴({})

```js
const obj = { name: "Alice", age: 25 };
```

### 2. 생성자 함수

```js
function Person(name: string, age: number) {
  this.name = name;
  this.age = age;
}
const p1 = new Person("Alice", 25);
console.log(p1.name); // Alice
```

### 3. class 문법(ES6)

```js
class Person {
  name: string;
  age: number;

  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }

  greet() {
    console.log(`Hello, my name is ${this.name}`);
  }
}

const p1 = new Person("Alice", 25);
p1.greet(); // Hello, my name is Alice
```

class는 객체의 설계도 역할을 하며, 메서드와 속성을 호함할 수 있다.

## 5. 객체 활용 예시

### 1) 객체를 사용한 데이터 관리

```js
const user = {
  id: 1,
  name: "Alice",
  preferences: {
    theme: "dark",
    notifications: true,
  },
};

console.log(user.preferences.theme); //dark
```

### 2) 객체 배열 다루기

```js
const users = [
  { id: 1, name: "Alice" },
  { id: 2, name: "Bob" },
];

const userNames = users.map((user) => user.name);
console.log(userNames); //["Alice", "Bob"]
```

## 정리

- 객체는 키-값 쌍으로 구성된 데이터 구조이다.
- 속성과 메서드를 가질 수 있다.
- 동적으로 속성을 추가/삭제할 수 있다.
- 객체는 참조 타입으로 다뤄지며, 깉은 복사를 해야 독립적인 데이터를 유지 할 수 있다.
- Object.keys(), Object.values(),Object.assign() 같은 유틸 함수가 있다.
- 다양한 객체 생성 방법 ({},class, function , object.create())
- 객체는 데이터 관리, 컴포넌트 상태 관리, 데이터 조작에 유용하게 사용된다.
