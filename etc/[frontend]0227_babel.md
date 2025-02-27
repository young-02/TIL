# Babel이란?

Babel은 javascript의 필수적인 **트랜스파일러**이다.
최신 javascript문법을 구형 브라우저에서도 실행할 수 있도록 변환하는 역할을 한다.

### 1. 최신 javascript(ES6))를 구형 버전(ES5)으로 변환

브라우저마다 javascript지원 범위가 다르다.
IE11 같은 구형 브라우저는 최신 JS기능을 지원하지 않는다.
Babel을 사용하면 최신 문법을 옛날 문법으로 변환 할수 있다.

```js
let name = "Babel";
const greet = () => console.log("Hello,${name}");
```

Babel 변환

```js
"use strict";

var name = "Babel";
var greet = function greet() {
  console.log("Hello,${name}");
};
```

- let -> var로 변경됨 (구형 브라우저 호환성 때문)
- 화살표함수 => -> 일반 function 으로 변환됨
- const -> var 로 변경

### 2.JSX 변환(React)

JSX는 브라우저가 직접 이해할수 없기 때문에 Babel이 변환해줘야 한다.

```jsx
const element = <h1>Hello,Babel</h1>;
```

Babel 변환

```js
const element = React.createElement("h1", null, "Hello,Babel");
```

- h1 -> React.createElement함수로 변환됨
- 브라우저가 실행 가능하도록 변경됨

### 3. TypeScript 변환

Typescript 파일을 Javascript로 변환
Typescript에서는 타입 주석을 사용할수 있지만 브라우저는 이해하지 못한다.

```ts
const add = (a: number, b: number): number => {
  return a + b;
};
```

Babel 변환

```js
const add = () => {
  return a + b;
};
```

- :number 같은 타입 주석이 제거됨
- 브라우저에서 실행할 수 있는 순수 JS코드로 변환됨
- TypeScript를 변환할 때는 `@babel/preset-typescript` 플러그인이 필요하다.

### 4.Polyfill추가

Polyfill은 브라우저에서 지원되지 않는 기능을 대신 구현하는 코드이다.
예를 들어 Promise나 fetch()같은 최신기능을 지원하지 않는 브라우저에서는 Babel이 자동으로 Polyfill을 추가한다.

```js
const promise = new Promise((resolve) => resolve("done"));
```

Babel 변환

```js
import "core-js/stable";
import "regenerator-runtime/runtime";

var promise = new Promise(function (resolve) {
  return resolve("done");
});
```

- core-js 와 regenerator-runtime이 추가되어 구형브라우저도에서도 Promise를 사용할 수 있음
- Polyfill을 적용하려면 @babel/polyfill 또는 core-js를 사용해야 한다.

## Babel설치 및 사용법

Node.jsdhk npm이 설치되어 있어야 한다.

```js
npm install --save-dev @babel/core @babel/cli @babel/preset-env

```

- @babel/core → Babel의 핵심 기능
- @babel/cli → 터미널에서 Babel을 실행할 수 있는 명령어 제공
- @babel/preset-env → 최신 JavaScript를 변환하는 기본 프리셋

### 2. Babel 설정 파일 생성

Babel이 어떻게 변환할지 설정해야 한다.
루트 폴더에 .babelrc 파일을 생성하고 아래 설정을 추가한다.

```json
{
  "presets": ["@babel/preset-env"]
}
```

- @babel/preset-env -> 브라우저 지원 범위에 맞춰 최신 JS문법 변환

### 3. Babel실행하기

변환할 js파일을 src폴더에 넣고 실행하면 된다.

```
npx babel src --out-dir dist
```

- src 폴더의 최신 JS파일을 dist 폴더에 변환된 상태로 저장
- 변환된 파일은 구형 브라우저에서도 실행가능

## Babel + Webpack설정

Babel을 Webpack과 함께 사용하면 프론트엔드 프로젝트에서 더 편리하게 사용할 수 있습니다.

- webpack.config.js

```js
module.exports = {
  entry: "./src/index.js",
  output: {
    path: __dirname + "/dist",
    filename: "bundle.js",
  },
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: {
          loader: "babel-loader",
          options: {
            presets: ["@babel/preset-env"],
          },
        },
      },
    ],
  },
};
```

- .js파일을 babel-loader로 처리하여 변환
- @babel/preset-env 를 사용하여 최신 문법 변환

## 결론

- Babel은 최신 JS코드를 변환하여 구형 브라우저에서도 실행 가능하도록 만들어 주는 도구
- React JSX, TypeScript 코드도 변환가능
- Webpack과 함께 사용하면 더욱 강력한 환경 구성 가능
- 폴리필(@babel/polyfill)을 추가하면 최신 기능도 지원 가능

즉, 모든 환경에서 최신 Javascript를 사용할 수 있도록 도와주는 필수 도구 이다.
