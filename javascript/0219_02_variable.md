# 변수(variable)

변수는 **값을 저장할 수 있는 공간**
javascript에서 변수를 사용하면 **데이터를 저장하고 재사용** 할 수 있다.

## 1. 변수 선언방식(var, let , const)

| 키워드 | 재할당 가능 여부 | 재선언 가능 여부 | 스코프      | 호이스팅                        |
| ------ | ---------------- | ---------------- | ----------- | ------------------------------- |
| var    | 가능             | 가능             | 함수 스코프 | 호이스팅o(초기화는 안됨)        |
| let    | 가능             | 불가능           | 블록 스코프 | 호이스팅 o(초기화x,TDZ영향받음) |
| const  | 불가능           | 불가능           | 블록스코프  | 호이스팅o(초기화x,TDZ영향받음)  |

## 2.var(권장되지 않음)

예전부터 사용되던 변수 선언 방식,
스코프문제와 호이스팅 문제 때문에 잘 사용되지 않는다.

```js
var name = "Alice";
console.log(name); //Alice

var name = "Bob"; //같은 변수명으로 재선언 가능(예기치 않은 오류 발생 가능)
console.log(name); //Bob
```

### var 문제점

1. 재선언 가능 -> 같은 변수를 여러 번 선언할 수 있어 혼란이 생길수 있음.
2. 함수 스코프 -> {}(블록) 내부에서 선언해도 바깥에서 접근 가능
3. 호이스팅 문제 -> 변수가 위로끌어올려지지만 초기화 되지 않음.

```js
console.log(age); //undefined
var age = 30;
console.log(age); //30
```

:white_check_mark: 호이스팅(Hoisting): 변수가 선언된 위치와 상관없이 최상단으로 끌어올려지느는 현상. 하지만 var는 초기화되지 않고 undefined로 출력됨

## 3. let

변수의 재할당이 가능하지만 재선언은 불가능하다.

```js
let city = "Seoul";
console.log(city); //Seoul

city = "Busan"; // 재할당 가능
console.log(city); //Busan

//let city = "Incheon"//재선언 불가능(에러 발생)
```

### let의 장점

- 블록 스코프를 가짐-> {} 내부에서 선언한 변수는 바깥에서 접근할 수 없음.
- 호이스팅되지만 초기화되지 않음 -> Temporal Dead Zone(TDZ)의 영향을 받음.

```js
console.log(score); //ReferenceError(TDZ 발생)
let score = 100;
console.log(score); //100
```

:white_check_mark: TDZ(Temporal Dead Zone,일시적 사각지대): let과 const 는 선언 전에 접근할 수 없다.
그래서 ReferenceError 발생

## 4. const

한 번 값이 할당되면 변결할 수 없는 상수(constant)를 선언할 때 사용

```js
const country = "Korea";
console.log(country); //Korea

country = "USA"; // 재할당 불가능(에러발생)
```

:white_check_mark: `const`는 반드시 선언과 동시에 초기화해야 함.

```js
const price; // SyntaxError 발생
price = 1000;
```

### const 장점

- 블록 스코프를 가짐
- 호이스팅되지만 초기화되지 않음(TDZ영향을 받음)
- 값 변경 방지 -> 예기치 않은 값 변경을 막아 안정성을 높임

### const의 예외(객체,배열은 변경 가능)

- const 로 선언해도 객체나 배열 내부의 값은 변경할 수 있음.

```js
const person = { name: "Alice", age: 25 };
person.age = 30; // 객체 속성 변경 가능
console.log(person.age); //30
```

- 객체 자체를 변경하는 건 불가능

```js
person = { name: "Bob", age: 40 }; // typeError(객체 재할당 불가능)
```

## 5. var, let , const 언제 사용?

- 변경할 필요 없는 값 -> const
- 변경될 가능성이 있는 값 -> let
- var는 사용하지 않는 것이 좋음

## 6. 변수 네이밍 규칙

- 알파벳, 숫자, 언더스코어(\_), 달러($) 사용 가능
- 숫자로 시작할 수 없음
- 예약어 사용 불가
- 대소문자 구분
- 카멜케이스, 스네이크케이스, 파스칼케이스 사용 가능

### 올바른 변수명

```js
let userName = "Alice";
let $price = 1000;
let _counter = 10;
```

### 잘못된 변수명

```js
let 1stPlace = "Gold" // 숫자로 시작
let user-name = "Math" //- 하이픈 사용 불가능,
let let = "reserved"// 예약어 사용 불가능
let user age = 25 // 공백 사용 불가능
```
