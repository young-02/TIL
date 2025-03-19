# var,let

변수는 스코프(scope,범위)라는 것을 가진다. var는 함수 스코프를 가지고, let은 블록 스코프를 가진다.

## var

```js
function b() {
  var a = 1;
}
console.log(a); // uncaught ReferenceError: a is not defined
```

- a는 함수 안에서 선언 한 것이라 함수 밖에선 접근이 되지 않는다.
- 변수의 접근 가능한 범위는 b함수 안에서만 가능하다.

```js
if (true) {
  var a = 1;
}
console.log(a); //1

for (var i = 0; i < 5; i++) {}
console.log(i); //5
```

- 블록스코프 (if,for, while, switch) 밖에서 a를 접근이 가능하다.

## let

```js
if (true) {
  let a = 1;
}
console.log(a); // Uncaught ReferenceError : a is not defined

for (let i = 0; i < 5; i++) {}
console.log(i); //Uncaught ReferenceError : i is not defined
```

- let은 블록 스코프 이기 때문에 블록({}) 밖에서는 접근이 불가능하다.
