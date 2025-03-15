# 파라미터와 인수

```js
function a(parameter) {
  console.log(parameter);
}

a("argument");
```

함수를 선언 할때는 parameter(매개변수) <br>
함수를 호출 할때는 argument(인수) <br>

## 여러개의 매개변수

```js
function a(w, x, y, z) {
  console.log(w, x, y, z);
  console.log(arguments);
}
a("hello", "parameter", "Argument");
console.log(a()); // 'hello','parameter', 'Argument',undefined
Arguments(3)[("hello", "parameter", "Argument")];
```

- function 안에서는 argument라는 값이 있고 넣었던 인수들을 배열 모양으로 출력 해준다.

### 인수가 매개변수보다 많아면 무시된다.

```js
function add(a, b) {
  return a + b;
}
add(1, 2, 3); //
console.log(add()); //3
```
