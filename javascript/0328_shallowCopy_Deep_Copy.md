# 객체의 얕은 복사 와 깊은 복사

## 얕은 복사(Shallow Copy)

얕은 복사는 객체의 1단계까지만 복사 하는 방식이다. <br>
객체의 프로퍼티 값이 기본 자료형(숫자, 문자열 등)이면 값 자체를 복사하지만, 참조 차료형(배열, 객체)등이면 원본 객체의 참조(메모리 주소)만 복사 한다.

```js
const obj1 = { a: 1, b: { c: 2 } };
const obj2 = { ...obj1 }; // 스프레드 연산자를 사용한 얕은 복사

console.log(obj1.b === obj2.b); //true(같은 참조를 가리킴)

obj2.b.c = 100;
console.log(obj1.b.c); // 100 (원본 객체도 영향을 받음)
```

- {...obj1}은 a:1처럼 기본 자료형의 값은 복사하지만, b:{c:2}처럼 객체인 경우 참조(주소)만 복사한다.
- 따라서 obj2.b.c = 100을 하면 obj1.b.c.도 같이 복사 된다.

### 얕은 복사를 수행하는 방법

- 스프레드 연산자(...)
- object.assign()
  ```js
  const obj2 = Object.assign({}, obj1);
  ```
- Array.prototype.slice()

```js
const arr1 = [1, 2, [3, 4]];
const arr2 = arr1.slice();
```

## 깊은 복사(Deep Copy)

깊은 복사는 객체의 모든 중첩 구조까지 완전히 새로운 메모리에 복사하는 방식이다. <br>
내부 객체 까지 새롭게 복사해서 원본과 복사본이 완전히 독립적인 상태가 된다.

```js
const obj1 = { a: 1, b: { c: 2 } };
const obj2 = structuredClone(obj1); //깊은복사;

console.log(obj1.b === obj2.b); //false
obj2.b.c = 100;
console.log(obj1.b.c); //2 원본 객체는 변경되지 않음
```

- structuredClone()은 객체의 모든 중첩된 구조를 새롭게 복사해서 완저히 독립된 객체를 생성하기 때문이다.

### 깊은 복사를 수행하는 방법

1. structuredClone()
2. JSON.parse(JSON.stringify(obj)) 단, 함수나 undefined를 포함한 객체는 복사 불가

```js
const obj2 = JSON.parse(JSON.stringify(obj1));
```

3. lodash의 cloneDeep()사용

```js
import cloneDeep from "lodash/cloneDeep";
const obj2 = cloneDeep(obj1);
```

## 정리

| 비교항목            | 얕은복사                | 깊은복사                         |
| ------------------- | ----------------------- | -------------------------------- |
| 복사 방식           | 1단계까지만 복사        | 모든 중첩된 객체까지 복사        |
| 내부 객체의 참조    | 원본과 동일한 참조 유지 | 원본과 완전히 독립               |
| 성능                | 빠름                    | 느림(데이터가 많을수록 성능저하) |
| 원본 객체 변경 영향 | 있음                    | 없음                             |
| 사용예              | 단순한 객체 상태관리    | 복잡한 중첩 구조 객체            |

## 얕은복사를 써도 괜찮은 경우

- 단순한 객체(1단계만 있음)를 복사할때
- 원본과 복사본이 같은 내부 객체를 공유해도 괜찮을때
- 성능이 중요한 경우 (복사할 데이터가 많으면 깊은 복사는 속도가 느릴 수 있음)

## 깊은 복사를 써야 하는 경우

- 중첩된 객체가 포함된 데이터를 완전히 분리해야 할 때
- 원본 객체가 변경되어도 복사본이 영향을 받으면 안 될 때
- 상태관리를 할 때 (React,Redux 같은 곳에서 중요)
