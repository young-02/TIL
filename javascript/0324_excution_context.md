# Execution Context

실행컨텍스트(Execution Context)는 자바스크립트 코드가 실행될 때 생성되는 환경을 의미한다.
자바스크립트 엔진은 실행 컨텍스트를 이용해 변수, 함수, 객체의 스코프와 실행 순서를 관리한다.

## 실행컨텍스트란?

자바스크립트는 단일 스레드 기반의 동기적 언어이다. 한번에 하나의 작업만 처리할 수 있고, 코드가 위에서 아래로 순차적으로 실행된다. <br>
그런데 함수가 호풀될 때마다 실행되는 환경이 다를 수 있다.
그래서 각 코드가 실행될 때 필요한 (변수, 함수, this등)를 저장하는 공간이 필요하다. 이 역할을 하는 것이 실행컨텍스트이다.

1. 변수와 함수 선언을 저장하고 관리
2. 스코프와 클로저 정보 저장
3. this바인딩 관리
4. 실행 순서 관리(스택구조사용)

## 실행 컨텍스트의 구조

1. Variable Environment(변수 환경)
   - var 와 function 선언문을 저장하는 공간
   - let, const는 별도로 관리됨(TDZ발생)
   - 함수 실행이 끝나면 삭제됨
2. Lexical Environment(렉시컬 환경)
   - let, const 변수를 저장하는 공간
   - 상위 실행 컨텍스트 정보를 포함 -> 스코프 체인을 통해 참조 가능
   - 클로저와 관련이 깊음
3. This Binding(this 값 저장)
   - 현재 실행 컨텍스트에서 this가 가리키는 값 결정
   - 함수 호출 방식에 따라 this값이 달라짐

## 실행 컨텍스트의 종류

1. 전역 실행 컨텍스트(Global Execution Context)
   - 자바스크립트 코드 실행 시 가장 먼저 생성되는 컨텍스트
   - 전역 변수, 전역 함수 등을 포함
   - 브라우저에서는 window 객체가 this가 됨
2. 함수 실행 컨텍스트(Function Execution Context)
   - 함수가 호풀될 때마다 생성됨
   - 함수 내부 변수, 함수 선언 등을 저장
   - 함수 실행이 끝나면 제거됨
3. Eval 실행 컨텍스트(Eval Execution Context)
   - Eval() 함수가 실행될 때 별도의 컨텍스트가 생성됨
   - 보안 및 성능 이유 때문에 거의 사용하지 않음

## 실행 컨텍스트 생성과정

### 1.생성 단계

코드가 실행되기 전에 먼저 실행 컨텍스트가 생성되면서 다음 작업이 진행된다.

1. 변수, 함수 선언 저장(Hoisting)
   - var 변수는 초기값 undefined로 할당
   - function 선언문은 메모리에 미리 저장
   - let, const 변수는 초기화 되지 않음(TDZ, 일시적 사각지대 존재)
2. Lexical Environment 구성(스코프 체인 설정)
   - 현재 컨텍스트가 어느 스코프(외부환경)를 참조하는지 저장
3. this 값 결정
   - 실행 방식에 따라 this 값이 결정됨

### 2.실행단계

코드가 한 줄씩 실행되면서 변수가 실제 값으로 변경되고, 연산이 수행된다.

```js
function test() {
  var a = 100;
  console.log(a);
}
test();
```

1. test()가 호출되면 새로운 실행 컨텍스트가 생성된다
2. a가 선언되고 100이 할당된다.
3. console.log(a)실행된다.
4. test()실행이 끝나면 실행 컨텍스트가 스택에서 제거된다.

## 실행 컨텍스트 스택

자바스크립트 엔진은 실행 컨텍스트를 스택 구조로 관리한다.

```js
function first() {
  console.log("first function");
  second();
}

function second() {
  console.log("second function");
}

first();
console.log("Global Execution");
```

1. 전역 실행 컨텍스트 생성(Global Execution Context)
2. first() 호출 -> 새로운 실행 컨텍스트 push
3. console.log('first function') 실행
4. second()호풀 -> 새로운 실행 컨텍스트 push
5. console.log('second function')실행 후 second()컨텍스트 pop
6. first() 실행 종류 후 first() 컨텍스트 pop
7. console.log('Global Execution')실행
8. 모든 실행이 끝나면 전역 실행 컨텍스트 pop

## 실행 컨텍스트와 클로저

클로저(closure)는 실행 컨텍스트가 종료 된 후에도 외부 변수를 기억하는 개념이다.

```js
function outer() {
  let x = 10;
  function inner() {
    console.log(x);
  }
  return inner;
}

const closureFunc = outer();
closureFunc();
```

- outer() 실행이 끝나도 x는 inner()의 Lexical Environment에 저장된다.
- 그래서 closureFunc()실행시 x값을 실행할 수 있다.

## 실행 컨텍스트와 this 바인딩

### 객체 메서드의 this

```js
const obj = {
  name: "Alice",
  showThis: function () {
    console.log(this.name);
  },
};
obj.showThis(); //'Alice'
```

- this는 obj를 가리킴

### 일반 함수에서 this

```js
const fn = obj.showThis;
fn(); //undefined(전역 실행 컨텍스트에서 실행됨)
```

- 일반 함수로 호출하면 this가 window 또는 undefined가 됨

### 화살표 함수 에서 this

```js
const obj2 = {
  name: "Bob",
  showThis: () => {
    console.log(this.name);
  },
};

obj2.showThis(); //undefined
```

- 화살표 함수는 상위 스코프의 this를 유지하므로 undefined
