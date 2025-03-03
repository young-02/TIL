# useRef

useRef는 React에서 제공하는 훅(Hook)중 하나로, **DOM요소에 접근하거나, 컴포넌트가 리렌더링될때도 유지 되는 값을 저장할때** 사용한다.
이는 상태 (useState)와 다르게 값이 변경되어도 **컴포넌트가 리렌더링 되지 않는다**는 특징이 있다.

## 1. useRef 사용법

### 기본 문법

```tsx
const ref = useRef(initialValue);
```

- initialValue: 초기 값(예:null, 0,{})
- 반환값은 {current:initialValue}형태의 객체이며, ref.current.를 통해 값을 일거나 수정할 수 있다.

## 2. useRef 주요 사용 사례

### 1. DOM요소에 접근

useRef는 직접 DOM를 조작할 때 사용된다. 예를 들어 input 요소에 포커스를 주는 경우

```tsx
import {useRef} from 'react';

export default function InputFocus(){
  const inputRef = useRef<HTMLInputElement>(null)

  const handleFocus = ()=>{
    if(inputRef.current){
      inputRef.current.focus(); //input 요소에 포커스 설정
    }
  }

  return (
    <div>
      <input ref={inputRef} type="text">
      <button onClick={handleFocus}>포커스 주기</button>
    </div>
  )
}
```

- ref를 input 요소에 연결하면 inputRef.current가 해당 DOM요소를 참조하게 된다.

### (2)값 유지 (렌더링이 일어나도 값 유지)

useRef는 렌더링이 발생해도 값이 유지된다.
반면 useState는 값이 변경되면 렌더링이 다시 발행하는 차이점이 있다.

```js
import { useState, useRef } from "react";

export default function Counter() {
  const [count, setCount] = useState(0);
  const countRef = useRef(0);

  const handClick = () => {
    setCount(count + 1); //상태 변경
    countRef.current += 1; // useRef 값 변경(렌더링 x)
    console.log("State count:", count);
    console.log("Ref count:", countRef.current);
  };

  return (
    <div>
      <p>State:{count}</p>
      <p>Ref:{countRef.current}</p>
      <button onClick={handleClick}>Increase</button>
    </div>
  );
}
```

- state count는 버튼 클릭할 때마다 리렌더링되어 화면에 업데이트됨
- ref count는 값이 바뀌어도 리렌더링 되지 않으며, console.log()로만 확인 가능

:white_check_box: useRef는 화면을 업데이트할 필요 없이 값을 저장할 때 적합!
:white_check_box: useState는 화면이 변경될 때 사용!

### (3)이전값 저장하기

useRef를 사용하면 컴포넌트의 이전 상태 값을 저장할 수도 있다.

```js
import { useState, useRef, useEffect } from "react";
export default function PreviousValue() {
  const [count, setCount] = useState(0);
  const prevCountRef = useRef(null);

  useEffect(() => {
    prevCountRef.current = count; // 현재 값을 저장
  }, [count]); // count가 변경될 때마다 실행됨

  return (
    <div>
      <p>현재 값: {count}</p>
      <p>이전 값: {prevCountRef.current}</p>
      <button onClick={() => setCount(count + 1)}>증가</button>
    </div>
  );
}
```

- count가 변경될 때마다 useEffect가 실행됨
- prevCountRef.current에 count의 이전 값을 저장
- 화면에는 현재 값과 이전 값이 표시됨.

### (4) setTimeout 과 useRef

리렌더링 시에도 setTimeout 을 취소하지 않도록 useRef를 사용할 수 있다.

```js
import { useEffect, useRef } from "react";

export default function Timer() {
  const timerRef = useRef(null);

  useEffect(() => {
    timerRef.current = setTimeout(() => {
      console.log("3초후 실행");
    }, 3000);

    return () => {
      if (timerRef.current) {
        clearTimeout(timerRef.current); //타이머 정리
      }
    };
  }, []);

  return <p>3초 후 콘솔에 메세지가 출력된다.</p>;
}
```

- 타이머 IDFMF useRef에 저장하면 컴포넌트가 리렌더링되더라도 ID가 유지되며, clearTimeout으로 안전하게 정리 가능

## useRef vs useState차이점

|              | useRef             | useState         |
| ------------ | ------------------ | ---------------- |
| 값 유지      | 렌더링 시에도 유지 | 렌더링 시 초기화 |
| DOM 접근     | 가능               | 불가능           |
| 이전 값 저장 | 가능               | 가능             |

## 언제 사용?

- DOM 요소를 직접 조작해야 할 때
- 렌더링 없이 값을 저장하고 싶을 때
- 이전 상태 값을 저장하고 싶을 때
- 타이머, 이벤트 핸들러 등을 지정하고 관리할때

## 정리

- useRef는 current 속성을 가지며, 컴포넌트가 리렌더링되더라도 값이 유지됨
- DOM 요소를 직접 조작할 때 유용, input,focus,scroll 등에 사용 가능
- useState와 달리 값이 변경되어도 리렌더링되지 않음
- 이전 값을 저장하거나, setTimeout 과 같은 비동기 작업을 관리 할때도 유용

:white_check_box:리렌더링 값만 저장하고 싶다면 useRef 사용
