# 배열(Array)

배열은 여러 개의 값을 순서대로 저장하는 데이터 구조 이다.
javascript에서 가장 많이 쓰이는 데이터 구조 중 하나이며, 다양한 기능과 메서드를 제공한다.

## 1. 배열(Array)라?

하나의 변수에 여러 개의 값을 저장할 수 있는 데이터 구조.
배열은 객체(Object)의 특별한 형태로 동작한다.

```js
const fruits = ["apple", "banana", "cherry"];
console.log(fruits[0]); // apple
console.log(fruits.length); // 3
```

- 배열의 각 항목은 인텍스(Index)를 통해 접근 가능
- 0부터 시작하는 숫자 인텍스를 가짐
- .length 속성을 이용해 배열 길이를 확인할 수 있음.

## 2. 배열의 특징

- 순서가 있는 데이터 구조
- 값을 중복해서 저장 가능
- 인덱스를 통해 빠르게 접근 가능
- 크기가 고정되지 않고 동적으로 변경가능

javascript에서 배열은 **동적 배열(Dynamic Array)**형태로 동작한다.
**크기를 미리 지정하지 않아도 되고, 값이 투가 되면 자동으로 크기가 늘어난다.**

## 3. 배열 생성 방법

### 1) 배열 리터럴 방식 ([] - 대괄호를 사용해 배열 선언)

```js
const numbers = [1, 2, 3, 4, 5];
```

### 2) Array 생성자 함수(new Array())

하나의 **숫자 값을 넣으면 해당 길이만큼의 빈 배열을 생성**하므로 주의 해야 한다.

```js
const arr1 = new Array(5); //길이가 5인 빈 배열
console.log(arr1); //[empty × 5]
const fruits = new Array("apple", "banana", "cherry"); // 여러 개 값 전달 시 정상적인 배열 생성
console.log(fruits); //["apple", "banana", "cherry"]
```

### 3) Array.of()

new Array()의 단점을 해결하기 위해서 나왔다.
배열을 생성할 때 값이 하나만 있어도 정상적으로 배열을 만들수 있다.

```js
const arr = Array.of(5);
console.log(arr); //[5]
```

### 4) Array.from()

Array.from()은 유사 배열 객체(array-like object)나 이터러블 객체(Set,Map)를 배열로 변환할때 사용한다.

```js
console.log(Array.from("hello")); //["h","e","l","l","o"]
console.log(Array.from({ length: 3, 0: "a", 1: "b", 2: "c" })); //["a","b","c"]
```

-> 유용한기능:{length:n}객체를 이용하면 쉽게 n길이의 배열을 만들수 있다.

## 4. 배열의 요소다루기(CRUD)

배열에서는 요소를 추가(Create), 읽기(Read), 수정(Update), 삭제(Delete)할 수 있다.

### 1) 요소추가 (Create)

**(1) push()- 배열 끝에 추가**

```js
const fruits = ["apple", "banana"];
fruits.push("cherry");
console.log(fruits); //['apple','banana','cherry']
```

**(2) unshift()- 배열 앞에 추가**

```js
fruits.unshift("mango");
console.log(fruits); //['mango','apple','banana','cherry']
```

### 2) 배열 요소 읽기(Read)

배열 요소는 인덱스(Index)를 이용해 접근할 수 있다.

```js
console.log(fruits[0]); //'mango'
console.log(fruits[fruits.length - 1]); //'cherry'
```

### 3) 배열 요소 수정(Update)

특정 인덱스의 값을 변경하면 된다.

```js
fruits[1] = "grape";
console.log(fruits); //['mango','grape',banana','cherry']
```

### 4) 배열 요소 삭제(Delete)

**(1) pop()- 배열 끝에서 삭제**

```js
fruits.pop();
console.log(fruits); //['mango','grape','banana']
```

**(2) shift()- 배열 앞에서 삭제**

```js
fruits.shift();
console.log(fruits); //['grape','banana']
```

**(3) splice() - 특정 인덱스 요소 삭제 및 추가**

```js
fruits.splice(1, 1); // 인덱스 1부터 1개 제거
console.log(fruits); //['grape',]
```

splice(startIndex,deleteCount,newItem1,newItem2...)

## 5. 배열 메서드 (활용법)

## 1) map() - 배열 변환(새로운 배열 생성)

```js
const numbers = 1,2,3
const objects = numbers.map((num)=>({number:num}))
console.log(objects) //[{number:1},{number:2},{number:3}]
```

## 2) filter() - 조건에 맞는 요소만 추출

```js
const numbers = [1, 2, 3, 4, 5];
const evenNumbers = numbers.filter((num) => num % 2 === 0);
console.log(evenNumbers); //[2,4]
```

## 3) reduce() - 누적 값 계산

```js
const number = [1, 2, 3, 4, 5];
const sum = numbers.reduce((acc, num) => acc + num, 0);
console.log(sum); //15
```

## 4) find() 조건에 맞는 첫 번째 요소 찾기

```js
const users = [
  { id: 1, name: "Alice" },
  { id: 2, name: "Bob" },
];
const user = users.find((user) => user.id === 2);
console.log(user); //{id:2,name:'Bob'}
```

## 5) some() & every() - 조건검사

```js
const numbers = [1, 2, 3, 4, 5];
console.log(numbers.some((num) => num > 2)); //true (하나라도 만족하면 true)
console.log(numbers.every((num) => num > 3)); //false (모두 만족하면 true)
```

## 6) sort() - 배열 정렬

```js
const arr = [3, 1, 4, 2];
arr.sort((a, b) => a - b);
console.log(arr); //[1,2,3,4]
```
