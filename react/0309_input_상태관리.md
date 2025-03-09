# react에서 input value를 관리 할때 useState와 useRef의 차이

## 1. useSate

- 값이 변경될때 마다 렌더링이 발생
- `onChange`이벤트 핸들러를 사용하여 state를 업데이트해야한다.

```jsx
import { useState } from "react";

export default function InputWithState() {
  const [value, setValue] = useState("");

  return (
    <div>
      <input
        type="text"
        value={value}
        onChange={(e) => setValue(e.target.value)}
      />
      <p>입력 값: {value}</p>
    </div>
  );
}
```

- setValue를 호풀하면 상태가 변경되고 컴포넌트가 다시 렌더링된다.
- 렌더링 될때 마다 input의 value가 업데이트된다.
- 입력 값이 화면에 즉시 반영된다.

## 2. useRef

- 렌더링 없이 값 유지 가능 -> 값이 바뀌어도 리렌더링 되지 않음
- `onChange` 없이 ref.current.value를 직접 조작 가능

```jsx
import { useRef } from "react";

export default function InputWithRef() {
  const inputRef = useRef < HTMLInputElement > null;

  const handleClick = () => {
    if (inputRef.current) {
      alert(`입력 값: ${inputRef.current.value}`);
    }
  };

  return (
    <div>
      <input type="text" ref={inputRef} />
      <button onClick={handleClick}>값 확인</button>
    </div>
  );
}
```

- inputRef.current.value를 통해 값에 접근하지만, 상태로 관리되지 않음
- input에 입력해도 컴포넌트가 리렌더링되지 않음
- ref를 활용하면 DOM 직접 조작 가능

## 언제 사용해야 할까?

### useState

- 입력 값이 변경될 때마다 UI에 즉시 반영해야 할때
- 입력 값이 컴포넌트상태(state)로 관리되어야 할때

### useRef

- 입력 값이 변경되어도 렌더링을 발생시키고 싶지 않을때
- input에 초점을 맞추는 등의 DOM 조작이 필요할때
- 특정 시점에서만 값을 가져와야 할때 (버튼 클릭시 입력값을 확인)
