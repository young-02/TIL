# React

UI(사용자 인터페이스)를 만들기 위한 자바스크립트 라이브러리

## react 기본 개념

react는 컴포넌트 기반(Component-based)로 동작한다.
컴포넌트는 독립적인 UI 블록으로, 여러개를 조합하여 하나의 웹페이지를 만들수 있다.

## JSX문법

JSX(Javascript XML)라는 문법을 사용한다. HTML과 비슷하지만 Javascript코드도 함께 사용할 수 있다.

## React를 사용 하는 이유

1. 컴포넌트 기반 개발(Component-Based Architecture)

- UI를 독립적인 텀포넌트로 나눠서 관리하면 유지보수가 쉬워진다.
- 같은 UI 요소를 여러 번 재사용할 수 있다.

2. 가상 DOM - 빠른 렌더링(Virtual DOM)

- 실제 DOM을 직접 조작하는 대신, 가상 DOM을 사용하여 변경을 추적하고 최적화된 업데이트를 수행한다. (상태기반(state) 데이터 변경 시 자동 으로 UI 업데이트)
- 빠른 렌더링과 성능 향상을 제공한다.

3. 단방향 데이터 흐름(One-Way Data Flow)

- 데이터가 한 방향으로만 흐르며, 데이터의 변경을 추적하고 업데이트를 예측하기 쉽다.(부모->자식으로 데이터의 출처와 변경사항을 추적하기 쉽다.)
- 데이터의 흐름이 단순, 명확하여 디버깅 하기 쉽다.
- 복잡한 애플리케이션에서도 데이터의 변경사항을 쉽게 추적하고 제어 할수 있다.

4. 상태기반 데이터 관리(State-Based Data Management)

- 상태(state)기반으로 자동으로 UI가 업데이트 되어 직접 DOM을 조작할 필요가 없다.

**직접 DOM을 조작한다 의미**

- 직접 변경하고자 하는 HTML요소(DOM)을 찾아서 수정해야 한다.
- 상태(state)기반으로 자동으로 UI가 업데이트 되어 직접 DOM을 조작할 필요가 없다.

  ```html
  <p id="count">0</p>
  <button id="btn">+1 증가</button>

  <script>
    const countElement = document.getElementById("count");
    const btn = document.getElementById("btn");
    let count = 0;

    btn.addEventListener("click", () => {
      count += 1;
      countElement.innerText = count; //직접조작
    });
  </script>
  ```

  countElement.innerText = count; 처럼 직접 DOM을 수정하는데 이런 방식은 규모가 커질수록 복잡해지고 비효율적이다.

```javascript
import { useState } from "react";
function Counter() {
  const [count, setCount] = useState(0);
  return (
    <div>
      <p>{count}</p>
      <button onClick={() => setCount(count + 1)}>+1 증가</button>
    </div>
  );
}
```

DOM을 직접 수정하지 않아도 `count`가 변경되면 자동으로 UI가 업데이트 된다.

- 직접 document.getElementById()로 요소를 찾을 필요 없이 `setCount(count+1)만으로 간결하고 유지보수가 쉬움`
- 변경된 부분만 업데이트(Virtual DOM) 하기 때문에 전체 DOM을 다시 렌더링 하지 않아도 됨
- state만 관리하면 되므로 규모가 커질수록 유지보수등 관리하기가 쉬워진다.

## 정리

=> 재사용, 성능최적화, 자동 ui업데이트 의 장점을 가지고 있다.
