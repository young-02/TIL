# import와 export

javascript의 import와 export는 **모듈(module) 시스템을 통해 코드를 여러 파일로 나눠서 관리하고,
필요한 곳에서 재사용**할 수 있도록 도와주는 기능이다.

## 1. export(내보내기)

export는 다른파일에서 사용할 수 있도록 변수, 함수 , 클래스 객체 등을 내보내는 역할을 한다.

1. named export(이름 내보내기)
2. default export(기본 내보내기)

### 1-1. named export(이름 내보내기)

named export는 여러 개의 요소를 내보낼 수 있따.
각 요소는 이름을 가지고 있으며, 같은 이름으로 가져와야 한다.

```js
//util.js
export const PI = 3.12159; // 변수 내보내기

export function add(a, b) {
  //함수 내보내기
  return a + b;
}

export class Calculator {
  //클래스 내보내기
  multiply(a, b) {
    return a * b;
  }
}
```

:rocket: 가져올때 (import)

```js
import { PI, add, Calculator } from "./util.js";
console.log(PI);
console.log(add(1, 2));

const calculator = new Calculator();
console.log(calculator.multiply(2, 3));
```

:rocket: 여러개의 `export` 중 일부만 가져 올때

```js
import { add } from "./utils.js";

console.log(add(10, 20));
```

:rocket: 이름을 바꿔서 가져오려면 `as`사용

```js
import { add as sum } from "./utils.js";

console.log(sum(5, 5));
```

### 1-2. default export(기본 내보내기)

default export는 **파일에서 단 하나의 값만 내보낼 때 사용**
**보통 모듈의 핵심 기능을 대표하는 값**을 내보낼 때 사용한다.

```js

export default function logMessage(message){
  console.log('로그:'message)
}
```

:rocket: 가져올때(import)

```js
import log from "./logger.js";
log("Hello, World"); // 로그:Hello, World
```

`default export`는 이름을 자유롭게 변경해서 가져올 수 있다.

### 1-3. named export와 default export를 함께 사용

```js
//math.js
export const subtract = (a, b) => a - b;
export default function add(a, b) {
  return a + b;
}
```

:rocket:가져올때(import)

```js
import add, { subtract } from "./math.js";

console.log(add(10, 5)); //15
console.log(subtract(10, 5)); //5
```

:white_check_mark: default export는 이름을 자유롭게 정할 수 있고,
:white_check_mark: named export는 반드시 같은 이름으로 가져와야 한다.

## 2. import(가져오기)

| import 방법                                 | 설명                       | 예제                                      |
| ------------------------------------------- | -------------------------- | ----------------------------------------- |
| import {변수명} from '파일경로'             | named export가져오기       | import{add}from './math.js'               |
| import {변수명 as 다른이름} from '파일경로' | 이름 바꿔서 가져오기       | import {add as sum} from './math.js'      |
| import 변수명 from '파일경로'               | default export가져오기     | import add from './math.js'               |
| import \* as from '파일경로'                | 모든 export가져오기        | import \* as math from './math.js'        |
| import '파일경로'                           | 실행만하고 가녀오지는 않음 | import add, { subtract } from './init.js' |

## 3. 모든 export를 한번에 가져오기(import \* as)

```js
//util.js
export const greet = (name) => `Hello,${name}`;
export const age = 30;
```

:rocket : 가져올때 (import) - 객체 처럼 가져 올수 있다.

```js
import * as utils from "./utils.js";
console.og(utils.greet("Alice"));
console.log(utils.age);
```

:white_check_mark: 모든 export를 가져오면 객체 처럼 사용할 수 있다.

## 4. import와 export를 한번에 (re-export)

```js
//mathOperations.js
export { add, subtract } from "./math.js";
export { multiply, divide } from "./advanceMath.js";
```

:white_check_mark: 다른 모듈에서 여러 개의 export를 한번에 가져와서 중앙에서 관리 할 수 있다.

:rocket:가져올때(import)

```js
import { add, multiply } from "./mathOperations.js";
console.log(add(10, 5));
console.log(multiply(10, 5));
```

## 5. import 만 실행하는 경우

어떤 모듈을 실행만 하고, 값을 가져오지 않을 수 있다.

```js
//init.js
console.log("초기화 실행됨");
```

:rocket:가져올때 (import)

```js
import "./init.js";
```

:white_check_mark: 이 방식은 전역 설정 파일이나 초기화 코드를 실행할 때 유용하다.

## 정리

| 구분              | 설명                          | 예제                                  |
| ----------------- | ----------------------------- | ------------------------------------- |
| export            | 모듈을 내보냄                 | export const name = 'Alice'           |
| export default    | 기본 내보내기(파일당 1개가능) | export default function () {}         |
| import {변수명}   | named export 가져오기         | import{name}from './module/js'        |
| import 변수명     | default export 가져오기       | import myfunc from './module/js'      |
| import \* as 별칭 | ahems export가져오기          | import \* as utils from "./module/js" |
| import "경로"     | 실행만하고 가져오지 않음      | import './init.js'                    |

## 언제 named export와 default export를 사용할까?

- named export는 여러개의 값을 내보낼 때 사용한다.(유틸함수, 여러 개의 클래스 등)
  default export는 모듈의 핵심 기능 하나만 내보낼때 (라이브러리의 메인 함수)
