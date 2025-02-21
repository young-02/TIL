# 스프레드 연산자

스프레드연산자(...)는 배열, 객체, 함수 인자 등을 확장하는데 사용된다.
디스트럭처링과 함께 사용하면 코드를 더 간결하고 직관적으로 작성할 수 있다.

## 1. 배열에서 스프레드 연산자 사용하기

배열을 펼쳐서 새로운 배열을 만들거나, 배열을 복사할 때 사용한다.

### (1) 배열 복사 (Shallow Copy)

스프레드 연산자를 사용하면 배열을 복사 할수 있다.

```js
const original = [1, 2, 3];
const copy = [...original];

console.log(copy); // [1,2,3]
console.log(copy === original); // false (다른배열)
```

:white_check_mark: original 배열을 복사하여 새로운 배열 copy를 생성
:white_check_mark: `original` !== `copy` -> 새로운 배열이 생성되었다는 의미

### (2) 배열 합치기 (배열 병합)

기존 배열을 펼쳐서 새로운 배열에 포함할 수 있다.

```js
const arr1 = [1, 2];
const arr2 = [3, 4];

const merged = [...arr1, ...arr2];

console.log(merged); // [1,2,3,4]
```

:white_check_mark: arr1과 arr2를 결합하여 새로운 배열 생성!

### (3)새로운 요소 추가하기

기존배열을 유지하면서 새로운 요소를 추가할 수도 있다.

```js
const numbers = [2, 3, 4];
const newNumbers = [1, ...numbers, 5];
console.log(newNumbers); // [1,2,3,4,5]
```

:white_check_mark: 1과5를 기존 배열(numbers)앞뒤에 추가

## 2. 객체에서 스프레드 연산자 사용하기

객체에서도 복사하거나 속성을 추가할 때 유용하다.

### (1) 객체 복사

```js
const person = { name: "Alice", age: 25 };
const copy = { ...person };

console.log(copy); // { name: "Alice", age: 25 }
console.log(person === copy); // false (다른 객체)
```

:white_check_mark: person 객체를 복사하여 새로운 객체 copy를 생성
:white_check_mark: `person` !== `copy` -> 새로운 객체가 생성되었다는 의미

### (2) 객체 속성 추가 & 수정

```js
const user = { name: "Bob", age: 30 };
const updateUser = { ...user, age: 31, city: "Seoul" };

console.log(updateUser); // { name: "Bob", age: 31, city: "Seoul" }
```

:white_check_mark: age 30 -> 31 수정 <br>
:white_check_mark: city 추가

### (3) 객체 병합

```js
const info = { age: 28, country: "USA" };
const details = { name: "Charlie", job: "Engineer" };

const merged = { ...info, ...details };
console.log(merged); // { age: 28, country: "USA", name: "Charlie", job: "Engineer" }
```

:white_check_mark: info와 details 객체를 병합하여 새로운 객체 merged를 생성

## 3. 함수에서 스프레드 연산자 사용하기

### (1)함수 인자로 배열 전달

```js
function sum(a: number, b: number, c: number) {
  return a + b + cl;
}
const numbers = [1, 2, 3];
console.log(sum(...numbers)); //6
```

:white_check_mark: 배열을 개별인자로 분해하여 함수에 전달.

### (2) 여러 개의 함수 인자 받기 (rest와 차이점)

- 스프레드(...):배열을 펼쳐서 개별 요소로 전달
- 래스트(...): 여러개의 인자를 배열로 수집

```js
function printNumbers(...nums: number[]) {
  console.log(nums);
}
printNumbers(1, 2, 3, 4, 5); //[1,2,3,4,5]
```

:white_check_mark: ...nums는 여러 개의 인자를 배열로 수집 (rest parameter)

## 4. 스프레 연산자 주의할 점

### (1) 깊은 복사가 아니라 얕은 복사!

스프레드 연산자는 **얕은 복사(Shallow Copy)** 를 수행한다.
즉, 중첨된 객체는 여전히 원본을 참조한다.

```js
const obj1 = { name: "Alice", details: { age: 25 } };
const obj2 = { ...obj1 };

obj2.details.age = 30;

console.log(obj1.details.age); // 30 (원본 객체도 변경됨!)
```

:white_check_mark:해결 방법: 깊은 복사(Deep Copy)를 원하면 `structuredClone()` 또는
JSON.parse(JSON.stringify())를 사용

```js
const deepCopy = structuredClone(obj1);
deepCopy.details.age = 40;

console.log(obj1.details.age); //30 원본이 변경되지 않음
console.log(deepCopy.details.age); //40
```

## 정리

| 사용처              | 예제                  |
| ------------------- | --------------------- |
| 배열복사            | [...arr]              |
| 배열 합치기         | [...arr1, ...arr2]    |
| 배열에 요소 추가    | [1,...arr,5]          |
| 객체 복사           | {...obj}              |
| 객체 속성 추가/수정 | {...obj,newKey:value} |
| 객체 합치기         | {..obj1, ...obj2}     |
| 함수 인자 전달      | func(...arr)          |
