# 불변성(immutability)

불변성은 변수나, 객체, 배열 등의 값을 변경하지 않고, 그 값을 그대로 유지하는 것을 의미한다.<br>
즉 **값을 변경하지 않고 새로운 값을 만들어내는 방식을 사용하는 개념**이다. <br>
불변성을 유지하려면 데이터를 수정하는 대신, **변경이 필요한 데이터의 복사본을 만들어서 수정하고, 원본은 그대로 두는 방법을 사용**한다.

## 불변성의 이유와 중요성

1. 예측 가능성: 데이터가 변하지 않으면, 해당 데이터의 상태가 예측 가능하고 버그를 줄일 수 있다.
2. 디버깅 용이성: 불변 데이터를 사용하면 상태 추적이 더 쉽고, 어디서 문제가 발생했는지 찾기 쉬워진다.
3. 동시성 문제 해결 : 불변 데이터를 사용하면, 여러 곳에서 데이터에 접근할 때 동시성 문제를 예방할 수 있다. 여러 곳에서 데이터를 동시에 수정하려 할 때 충돌이 발생할 수 있기 때문이다.
4. React 에서의 불변성: React에서는 상태(sate)가 변경될 때 불변성을 유지하는 것이 중요하다. 상태를 직접 변경하지 않고 새로운 객체나 배열을 반환해야 리렌더링을 제대로 할 수 있다.

## 불변성 적용 방법

### 1. 배열의 경우

- 원본 배열을 변경하는 대신, 새로운 배열을 만들어서 반환한다.
- 예 : `push`,`pop`,`shift`,`unshift`등을 사용하지 않고, `concat`, `slice`,`map`등을 사용해 새로운 배열을 만든다.

```js
const arr = [1, 2, 3];
//잘못된 방법
arr.push(4); // 배열직접 수정 x, 원본배열이 변경됨

//올바른 방법 (새 배열을 생성)
const newArr = [...arr, 4]; // 원본 배열은 변경되지 않음
```

### 2. 객체의 경우

- 객체의 속성을 직접 변경하지 않고, 객체를 복사한 후 속성을 변경한 새로운 객체를 만든다.
- 예:`Object.assign` 또는 스프레드 연산자(...)를 사용하여 객체를 복사한다.

```js
const obj = { a: 1, b: 2 };

//잘못된 방법
obj.a = 3;

//올바른 방법(새 객체를 생성)
const newObj = { ...obj, a: 3 }; // 원본 객체는 변경되지 않음.
```

이렇게 불변성을 유지하면, 데이터 변경이 예측 가능하고 오류가 발생할 확률이 납아진다. React에서는 이런 불변성 개념이 특히 중요하므로, 상태를 변경할 때도 이 원칙을 따르는 것이 좋다.

## 3. React에서의 불변성

React에서는 상태(State)를 직접 변경하면 리렌더링이 제대로 이루어지지 않거나 예기치 않은 동작이 발생할 수 있기 때문에 **불변성을 유지하면서 상태를 업데이트 하는 것이 중요**하다.

### 잘못된 상태 변경 예시

```js
import { useState } from "react";

export default function App() {
  const [numbers, setNumbers] = useState([1, 2, 3]);

  // 직접 상태를 변경하는 잘못된 코드
  const addNumber = () => {
    numbers.push(4); // 원본 배열이 변경됨
    setNumbers(numbers); // 상태가 바뀌었지만 React는 변경을 감지하지 못할 수 있음
  };

  return (
    <div>
      <button onClick={addNumber}>Add Number</button>
      <p>{numbers.join(", ")}</p>
    </div>
  );
}
```

**문제가 되는 이유?** <br>

- push를 사용하면 기존 배열 numbers가 직접 변경된다.
- React는 numbers가 같은 배열 참조를 갖고 있기 때문에 setNumbers(numbers)를 호출해도 변경을 감지하지 못할수 있다.
- 따라서 컴포넌트가 리렌더링되지 않거나, 예상치 못한 동작이 발생할 가능성이 높다.

### 올바른 상태 변경 예시 (불변성 유지)

```js
import { useState } from "react";

export default function App() {
  const [numbers, setNumbers] = useState([1, 2, 3]);

  // 직접 상태를 변경하는 잘못된 코드
  const addNumber = () => {
    numbers.push(4); // 원본 배열이 변경됨
    setNumbers(numbers); // 상태가 바뀌었지만 React는 변경을 감지하지 못할 수 있음
  };

  return (
    <div>
      <button onClick={addNumber}>Add Number</button>
      <p>{numbers.join(", ")}</p>
    </div>
  );
}
```

- setNumbers([...numbers,4])를 사용하여 **새로운 배열을 생성**하고 그 상태를 업데이트 한다.
- 이렇게 하면 React가 numbers의 변경을 감지하고 정상적으로 리렌더링을 수행한다.

## 4. React 객체상태를 변경할 때 불변성 유지방법

### 잘못된 상태 변경

```js
const [user, setUser] = useState({ name: "Alice", age: 25 });

const updateAge = () => {
  user.age = 26; // 원본 객체 변경 (잘못된 방법)
  setUser(user); // 상태 변경을 감지하지 못할 수 있음
};
```

### 올바른 상태 변경(불변성 유지)

```js
const [user, setUser] = useState({ name: "Alice", age: 25 });

const updateAge = () => {
  setUser({ ...user, age: 26 }); // 새 객체를 만들어서 업데이트
};
```

- 객체를 변경할 때는 Object.assign 또는 { ...obj } 사용

### 정리

React의 useSate에서 불변성을 유지하면서 새로운 객체/배열을 생성해야 React가 변경을 감지하고 리렌더링이 제대로 된다.<br>
React상태 관리에서 불변성 유지는 필수적인 개념이므로, 항상 `"직접 변경하지 않고 새로운 값을 만들어야한다"`는 원칙을 기억해야 한다.
