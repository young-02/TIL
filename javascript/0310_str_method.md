# string method

## 1. include()

문자열에서 특정 문자열이 포함되어 있는지 확인하는 메서드

```js
const str = "Hello,world";
console.log(str.includes("world")); //true
console.log(str.includes("bye")); //false
```

- 포함되어있으면 true 포함되어 있지 않으면 false

## 2. split()

문자열을 특정 구분자 (separator)를 기준으로 나누어 배열(Array)로 반환하는 메세드.

```js
const str = "apple,banana,cherry";
console.log(str.split("")); // ["apple", "banana", "cherry"]

//공백기준
const sentence = "Hello world! TypeScript is awesome.";
console.log(sentence.split(" ")); // ["Hello", "world!", "TypeScript", "is", "awesome."]

//빈 문자열로 나누기 (한 글자씩 분할)
const word = "hello";
console.log(word.split(""));
// ["h", "e", "l", "l", "o"]

//구분자가 없을때
const word = "hello";
console.log(word.split()); // ["hello"]

//제한 개수
const str2 = "one,two,three,four,five";
console.log(str2.split(",", 3)); // ["one", "two", "three"] (최대 3개만 반환)
```
