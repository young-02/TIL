# React의 상태(state)관리란?

상태(State)는 컴포넌트의 데이터(값)이며, 이 값이 변경되면 자동으로 UI가 업데이트된다. 즉, 상태를 관리하는 것은 변경되는 데이터를 효율적으로 관리 하는 것을 의미한다.

## 1. 상태란?

`count` - 상태(state)이고 버튼을 클릭했을 때 `count`값이 변경되면 UI도 자동으로 업데이트 된다.

```javascript
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0); // count: 상태, setCount: 상태를 변경하는 함수

  return (
    <div>
      <p>현재 카운트:{count}</p>
      <button onClick={() => setCount(count + 1)}>+1 증가</button>
    </div>
  );
}

export default Counter;
```

:white_check_mark: setCount(count+1)을 실행하면, count 값이 변경되고, React가 자동으로 UI를 다시 그림 (직접 DOM을 조작하지 않아도 됨.)

## 2. 상태(satate) vs 변수(let, const) 차이

```javascript
let count = 0;
count = count + 1;
```

count를 let으로 선언하면 값은 바뀌지만 UI는 업데이트 되지 않는다.
:white_check_mark: useState를 사용해야 값이 바뀔때마다 UI가 자동으로 업데이트된다.

## 3. 상태 업데이트의 주의점

### (1)상태는 직접 수정하면 안된다.(불변성 유지)

```javascript
function Counter() {
  const [count, setCount] = useState(0);

  function handleClick() {
    count = count + 1; // 이렇게 하면 UI가 업데이트 되지 않는다.
  }

  return (
    <div>
      <p>현재 카운트:{count}</p>
      <button onClick={handleClick}>+1 증가</button>
    </div>
  );
}

export default Counter;
```

:white_check_mark: 반드시 setCount()같은 상태 변경 함수를 사용해야함.

```javascript
function handleClick() {
  setCount(count + 1); // 이렇게 하면 UI가 업데이트 된다.
}
```

### (2) 상태 업데이트는 비동기적으로 처리된다.

setState() 함수는 비동기적으로 실행되기 때문에 **이전 상태 값을 사용할 때 주의해야 한다.**

```javascript
function Counter() {
  const [count, setCount] = useState(0);

  function handleClick() {
    setCount(count + 1);
    setCount(count + 1);
    setCount(count + 1);
  }

  return (
    <div>
      <p>현재 카운트:{count}</p>
      <button onClick={handleClick}>+3 증가</button>
    </div>
  );
}

export default Counter;
```

- 버튼을 클릭하면 예상과 다르게 `count`값이 1만 증가함
- `setCount(count +1)`가 실행 될때, `count`는 여전히 **이전 값(0)이라서** 같은 값이 3번 적용된다.

:white_check_mark:해결방법 : 함수형 업데이트를 사용하면 이전 상태 값을 안전하게 가져올수 있다.

```javascript
function handleClick() {
  setCount((prevCount) => prevCount + 1);
  setCount((prevCount) => prevCount + 1);
  setCount((prevCount) => prevCount + 1);
}
```

:white_check_mark: `prevCount`가 최신 상태 값으로 가져오므로 `+3`이 정상적으로 적용된다.

## 4. 상태관리의 확장(전역상태관리)

여러 컴포넌트에서 상태 공유

### (1) 부모 컴포넌트에서 상태관리(Props Drilling)

```javascript
function Parent() {
  const [count, setCount] = useState(0);

  return <Child count={count} />;
}

function Child({ count, setCount }) {
  return (
    <div>
      <p>현재 카운트:{count}</p>
      <button onClick={() => setCount(count + 1)}>+1 증가</button>
    </div>
  );
}
```

- parant에서 상태를 만들고, child에게 props로 전달
- 하지만 컴포넌트가 많아지면 Props를 계속 전달해야 하는 문제가 발생한다. (Props Drilling)

### (2) Context API

- `useContext`를 사용하면 중간 컴포넌트에 Props를 전달하지 않아도 된다.

```javascript
import { createContext, useState, useContext } from "react";

//1. Context 생성
const CountContext = createContext(null);

function Parent() {
  const [count, setCount] = useState(0);
  return (
    <CountContext.Provider value={{ count, setCount }}>
      <Child />
    </CountContext.Provider>
  );
}

function Child() {
  const { count, setCount } = useContext(CountContext);
  return (
    <div>
      <p>현재 카운트:{count}</p>
      <button onClick={() => setCount(count + 1)}>+1 증가</button>
    </div>
  );
}
```

:white_check_mark:props없이도 상태를 공유 할 수 있음.

### (3)Redux/Zustand 전역 상태관리 라이브러리

더 큰 규모의 앱에서 Redux,zustand같은 전역 상태 관리 라이브러리 사용

## 정리

| 상태관리 방법 | 특징                                              |
| ------------- | ------------------------------------------------- |
| useState      | 컴포넌트 내부 상태 관리                           |
| Props 전달    | 부모->자식으로 상태 공유(Props Drilling문제 발생) |
| useContext    | 전역상태 공유가능, props없이 상태 공유            |
| Redux/Zustand | 더 큰 규모의 앱에서 사용, 전역상태 관리           |
