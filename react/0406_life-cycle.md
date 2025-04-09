# 리액트 라이프사이클이란?

컴포넌트가 생성되고, 업데이트되고, 사라지는 과정에서 호출되는 특정함수나 타이밍을 말한다.
컴포넌트의 생애 주기에 따라 어떤 일이 언제 일어나는지를 관리할 수 있는 시스템이다.

## 리액트 컴포넌트의 생애주기 3단계

### 1. Mounting

컴포넌트가 DOM에 처음 생성될 때

### 2. Updating

props,state등이 바뀌어 컴포넌트가 리렌더링 될때

### 3. Unmounting

컴포넌트가 DOM에서 제거될 때

## 함수형 컴포넌트에서의 라이프사이클

함수형 컴포넌트에서는 useEffect()훅으로 라이프 사이클을 제어한다.

```tsx
import { useEffect, useState } from "react";

const Timer = () => {
  const [count, setCount] = useState(0);

  //Mount+Update
  useEffect(() => {
    console.log("컴포넌트가 렌더링됨 mount or update");
  });

  //Mount only (한번만 실행)

  useEffect(() => {
    console.log("처음 마운트됨");

    return () => {
      console.log("컴포넌트가 언마운트됨");
    };
  }, []);

  return (
    <div>
      <p>{count}초</p>
      <button onClick={() => setCount(count + 1)}>+1</button>
    </div>
  );
};
```

- 컴포넌트 처음 렌더링 : useEffect(... [])실행 -> '처음 마운트됨' 출력
- count 업데이트 : 일반 useEffect()실행 -> '컴포넌트가 렌더링됨' 출력
- 컴포넌트 제거 : return 안에 함수 실행 -> '컴포넌트가 언마운트됨' 출력

## 클래스형 컴포넌트의 라이프사이클 메서드

| 메서드                 | 시점               |
| ---------------------- | ------------------ |
| componentDidMount()    | 마운트 후 실행     |
| componentDidUpdate()   | 업데이트 후 실행   |
| componentWillUnmount() | 언마운트 직전 실행 |

## 언제 사용 ?

| 상황              | 훅/메서드                                    |
| ----------------- | -------------------------------------------- |
| API 요청          | useEffect(()=>{...}.[]) <- 마운트 시 한 번만 |
| 이벤트 등록/해제  | useEffect() + return                         |
| 애니메이션 트리거 | 업데이트 감지용 useEffect([deps])            |
| cleanup 작업      | 언마운트에서 return () =>{...} 사용          |

## 정리

- React 라이프사이클 = 컴포넌트 탄생, 변화, 제거 과정을 다루는 개념
- 함수형 컴포넌트는 useEffect() 훅으로 관리
- 마운트/ 업데이트/언마운트를 구분해서 작성 가능
- 리액트에서 **사이드 이펙트(부수효과)**가 필요할 때 반드시 이 개념을 이해하고 활용해야 함

* 부수적 효과 (Side Effect)
  리액트 컴포넌트의 사이드이펙트란 컴포넌트가 어떤 동작을 했을 때
  발생하게 되는 파생적인 효과
