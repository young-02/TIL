# useCallback

함수 자체를 메모이제이션하는 Hook이다. <br>
컴포넌트가 리렌더링될 때도 동일한 함수를 유지하고 싶을 때 사용한다.

```jsx
const memoizedCallback = useCallback(() => {}, [deps]);
```

## 언제 사용?

- 자식 컴포넌트에 콜백 함수를 props로 전달할 때
- 매 렌더마다 함수가 새로 생서되어 불필요한 리렌덜이을 유발할 때
- React.memo와 함께 사용할 때 효과 적이다.

## 예시

```jsx
import REact, { useState, useCallback } from "react";

const Child = React.memo(({ onClick }) => {
  console.log("Child");
  return <button onClick={onClick}>click</button>;
});

function Parent() {
  const [count, setCount] = useState(0);

  const handleClick = useCallback(() => {
    console.log("클릭");
  }, []);

  return (
    <div>
      <Child onClick={handleClick} />
      <button onClick={() => setCount(count + 1)}>부모카운트 증가</button>
    </div>
  );
}
```

- handleClick이 useCallback없이 정의되면, Parent가 리렌더링 될 때마다 Child도 리렌더링된다.
- useCallback을 사용하면 handleClick함수가 메모이제이션되어 Child는 리렌더링 되지 않는다.

## 주의

- 모든 함수를 무조건 useCallback으로 감싸는건 오히려 불필요한 최적화 일수 있다
- 오직 props로 함수를 넘길 때 또는 함수가 자주 생성되어 성능에 영향이 있을 때 사용하는게 좋다.
