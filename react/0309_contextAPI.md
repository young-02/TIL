# contextAPI

React에서 전역 상태를 관리 하기 위한 기능이다. <br>
props를 통해 부모에서 자식으로 데이터를 전달해야 했지만 ContextAPI를 사용하면 컴포넌트 트리의 깊숙한 곳까지 데이터를 쉽게 전달 할수 있다.

## 필요한 이유?

react에서 데이터는 단방향 데이터 흐름을 가지고 있으며 부모로 부터 자식으로 props를 통해 데이터를 내려 줘야 한다. 하지만 컴포넌트의 구조가 깊어질수록 "props drilling"이 발생한다.

## 사용방법

1. createContext로 컨텍스트를 생성한다.
2. Provider로 값을 감싸서 하위 컴포넌트에 전달한다.
3. useContext로 필요한 곳에서 값을 가져온다.

```jsx
import React, { createContext, useContext, useState } from "react";

//1.Contxt 생성
const ThemeContext = createContext('light')

const App() =>{
  const [theme, setTheme] = useState('dark')

  return(
    //2. Provider로 값 전달
    <ThemeContext.Provider value={theme}>
    <Parent>
    </ThemeContext.Provider>
  )
}
  const Parent = () =>{
    return <Child>
  }

  const Child = () =>{
    const theme = useContext(ThemeContext);

    return <div>현재테마 :{theme} </div>
  }
export default App;
```

- Child 컴포넌트가 theme값을 직접 받을수 있어서 props를 여러 번 전달할 필요가 없다.

## 장점

- props drilling을 방지할 수 있음
- 전역적으로 상태를 공유하기 현리함
- Redux와 같은 상태 관리 라이브러리 없이도 간단한 상태 관리를 할 수 있음.

## 단점

- context값이 변경될때, 이를 사용하는 모든 컴포넌트가 다시 렌더링됨
- 복잡한 상태 관리에서는 적합하지 않음(redux,Recoil 같은 라이브러리가 더 적합)

## 언제 사용?

- 전역적인 테마, 언어 설정, 인증 정보 등 관리 할때
- 리덕스를 사용하기엔 너무 가벼운 전역 상태 관리 필요할때
- props drilling문제를 해결하고 싶을때

복잡한 상태 관리에서는 zustand, redux 같은 라이브러리가 더 적합함.
