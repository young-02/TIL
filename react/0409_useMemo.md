# useMemo

useMemo는 React는 성능 최적화 훅(Hook)중 하나로, 값의 계산 결과를 기억(memoization)해서 불필요한 재계산을 방지합니다.

```jsx
const memoizedValue = useMemo(() => computeExpensiveVale(a, b), [a, b]);
```

## 언제 사용?

1. 계산 비용이 높은 함수의 결과값을 기억하고 싶을 때
2. 리렌더링 될 때마다 같은 계산을 반복하지 않도록 할 때
3. 컴포넌트가 자주 렌더링되는데 특정 계산은 변경이 없을 때

## 예시

```jsx
import { useState, useMemo } from "react";

function Example() {
  const [count, setCount] = useState(0);
  const [other, setOther] = useState(0);

  const expensiveCalculation = (num) => {
    console.log("계산중... ");
    return num * 1000;
  };
}

const memoizedValue = useMemo(() => expensiveCalculation(count), [count]);

return (
  <div>
    <h1>계산된 값: {memoizedValue}</h1>
    <button onClick={() => setCount(count + 1)}>count증가</button>
    <button onClick={() => setOther(other + 1)}>other증가</button>
  </div>
);
```

- count 값이 바뀔때만 expensiveCalculation()이 실행된다.
- other가 바뀔 때는 계산 되지 않고 기존 값이 재사용 된다.

## 주의할 점

- 너무 남용하지 않아야 한다. 성능 최적화는 필요한 경우에만 사용.
- 종속성 배열([])을 정확하게 설정해야 한다.
