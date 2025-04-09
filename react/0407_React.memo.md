# React.memo

컴포넌트를 메모이제이션(memoization)해서, 불필요한 리렌드링을 방지해주는 고차 컴포넌트(Higher Order Component)이다. <br>
즉, props가 변경되지 않으면 컴포넌트를 다시 렌더링 하지 않도록 해준다.

## 사용방법

```jsx
const MyComponent = React.memo(function MyComponent({ value }) {
  console.log("렌더링 됨");
  return <div>{value}</div>;
});
```

## 예제

```jsx
import React, { useState } from "react";

const Child = React.memo({count} =>{
  console.log('Child 렌더링')
  return <div>Count:{count}</div>
})


function Parent(){
  const [count, setCount ]= useStat(0)
  const [text, setText] = useState(
    ''
  )

  return (
    <div>
      <Child count={count}/>
      <button onClick={()=> setCount(count+1)}>카운트 증가</button>
      <input value={text} onChange={(e)=>setText(e.target.value)}/>
    </div>
  )

}
```

- text를 입력해도 child는 리렌더링 되지 않는다.
- count가 바뀔때만 child 컴포넌트가 리렌더링 됀다.

## 추가

- React.meme는 기본적으로 얕은 비교만한다.
- props가 객체, 배열이면 변화를 감지 못할 수도 있다. -> useMemo나 useCallback과 함께 사용하면 좋다.
- 커스텀 비교 함수도 설정할 수 있다.

```jsx
React.memo(Component(prevProps, nextProps)=>{
  return prevProps.value === nextProps.value
})
```
