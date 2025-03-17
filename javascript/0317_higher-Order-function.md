# 고차함수 (Higher-Order-Function)

함수를 인자로 받거나, 함수를 반환하는 함수 <br>
함수 자체를 조작할 수 있는 함수

1. 코드를 더 간결하고 모듈화 할수 있음
2. 추상화 수준을 높여 가독성을 개선
3. 함수형 프로그래밍 스타일을 지원

## 고차 함수 예제

1. 함수를 인자로 받는 경우

```js
function repeat(n, action) {
  for (let i = 0; i < n; i++) {
    action(i);
  }
}

repeat(3, (i) => console.log(`반복 ${i + 1}`));
//반복 1
//반복 2
//반복 3
```

- repeat 함수는 콜백함수를 받아서 n번 실행하도록 함

  2.함수를 반환하는 경우

```js
function createMultiplier(multiplier):(num) =>{
  return (num)=> num * multiplier
}

const double = createMultiplier(2)
console.log(double(5)) //10

const triple = creteMultiplier(3)
console.log(triple(5)) //15
```

- createMultiplier(2)실행하면 `num*2`를 수행하는 함수가 반환됨
- double(5) 는 `5*2 = 10`을 반환함

3. 배열 메서드(map, filter, reduce)

```js
const numbers = [1, 2, 3, 4, 5];

const doubled = numbers.map((num) => num * 2);
console.log(doubled); // [2, 4, 6, 8, 10]

const evens = numbers.filter((num) => num % 2 === 0);
console.log(evens); // [2, 4]

const sum = numbers.reduce((acc, num) => acc + num, 0);
console.log(sum); // 15
```

## 정리

- 고차 함슈는 함수를 인자로 받거나 함수를 반환하는 함수
- 코드를 간결하고 재사용 가능하게 만들어줌
- 배열 메서드 (map, filter, reduce)에서 많이 활용됨.
