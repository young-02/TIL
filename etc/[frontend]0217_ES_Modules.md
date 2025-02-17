# ES모듈(ESM)이란?

**ES모듈(ESM,ECMAScript Modules)**은 javascript에서 파일을 나누고 가져오는 공식적인 방법이다.
코드를 여러 개의 파일로 나누어 관리하고, 필요한 부분만 가져올 수 있도록 도와주는 기능이다.
이전에는 `script` 태그로 여러 개의 js파일을 불러와야 했지만, ES모듈을 사용하면 `import`와 `export` 키워드를 사용해서 파일을 가져와 깔끔하게 코드를 관리를 할 수 있다.

## ES모듈이 왜 필요할까?

프로젝트가 커질수록 한 개의 JS파일만으로 관리하기가 힘들다.
모든 기능을 한 파일에(main.js)에 넣으면 문제가 생긴다.

```html
<script src="header.js"></script>
<script src="footer.js"></script>
<script src="main.js"></script>
```

- 스크립트가 많아지면 관리가 어려워짐
- 파일 순서에 의존적(main.js가 header.js보다 먼저 로드되면 오류 발생)
- 모든 코드를 하나의 파일에 넣으면 유지보수가 힘듦

위와 같은 문제를 해결하기 위해 ES모듈이 필요하다.

## ES모듈(ESM)방식

ESM에서는 `import`와 `export` 키워드를 사용해서 필요한 코드만 가져올 수 있다.

### 파일구조

```
/src
  /index.html
  main.js (메인코드)
  math.js(유틸리티 파일)
```

### math.js (모듈파일)

```js
export function add(a, b) {
  return a + b;
}

export function multiply(a, b) {
  return a * b;
}
```

`add`함수와 `multiply`함수를 export해서 다른 파일에서 사용할 수 있도록 한다.

### main.js (메인파일)

```js
import { add, multiply } from "./math.js";

console.log(add(1, 2)); // 3
console.log(multiply(3, 4)); // 12
```

`import`를 사용해서 math.js의 함수를 불러와서 사용한다.

### index.html

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>ESM Example</title>
  </head>
  <body>
    <script type="module" src="main.js"></script>
  </body>
</html>
```

`<script type="module">`을 사용하면 브라우저가 ES 모듈을 지원한다.

## 모듈의 장점

:white_check_mark: 코드를 여러 개의 파일로 나누어 관리 가능 ->(유지보수가 쉬움)<br>
:white_check_mark: 모듈 간의 의존성 관리 용이 ->(코드 재사용성 향상)<br>
:white_check_mark: 코드 중복 제거 ->(코드 중복 제거)<br>
:white_check_mark: 비동기 로딩 ->(코드 비동기 로딩)<br>
:white_check_mark: 필요한 코드만 가져오기 때문에 성능향상 <br>

## ES모듈과 Webpack/Vite의 관계

ES 모듈은 기본적으로 브라우저를 지원하지만, Webpack,Vite같은 번들러가 있으면 더 효율적으로 관리 할 수 있다.

- Webpack은 모든 모듈을 하나의 번들 파일로 묶어준다.
- Vite는 ES모듈을 그대로 사용하여 빠르게 개발 가능하다. (즉, vite는 ES모듈을 기본적으로 지원하기 때문에 Webpack보다 빠르다.)

## 결론

- ES모듈(ESM)은 JS코드를 여러 파일로 나누어 관리할 수 있도록 해주는 공식적인 방식이다.
- ` export``import `를 사용하면 필요한 기능만 불러올 수있다.
- `type="module"`을 사용하면 브라우저가 ES모듈을 지원한다.
- Webpack,Vite같은 번들러가 있으면 ES모듈을 더 강력하게 만들어준다.
