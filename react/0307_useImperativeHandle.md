# useImperativeHandle

부모 컴포넌트가 자식 컴포넌으틔 특정 메서드나 속성에 직접 접근할 수 있도록 만드는 역할을 한다. <br>
일반적으로 Ref를 사용할때, 자식 컴포넌트의 내부 기능을 제한적으로 노출시기키고 싶을 때 유용하다.

### 언제 사용?

보통 컴포넌트 내부의 상태나 기능을 외부에서 직접 조작할 필요가 있을 때 사용한다.

- 모달 창을 열고 닫는 메서드 제공
- 커스텀입력(input)에서 focus()제어
- Canvas나 특정 UI 요소를 직접 조작

### 기본적인 useRef와 차이

- useRef는 일반적으로 DOM 요소에 직접 접근할때 사용된다.
- useImperativeHandle은 컴포넌트가 특정 메서드만 외부로 공개하도록 제어 할 수 있다.

## 사용방법

### input에 focus 제공

```jsx
import React, { useRef, useImperativeHandle, forwardRef } from "react";

//자식컴포넌트
const Child = forwardRef((props, ref)=>{
  const inputRef = useRef<HTMLInputElement>(null)

  useImperativeHandle(ref, ()=>{
    return {
      focus: () =>{
        if(inputRef.current){
          inputRef.current.focus()
        }
      }
    }
  })

  return<input ref={inputRef} type="text" placeholder="입력해주세요" />
})

//부모 컴포넌트
const Parent = () => {
  const inputRef = useRef<{focus : ()=>void} |null>(null)
  return (
    <div>
      <Child ref={childRef} />
      <button onClick={() => inputRef.current?.focus()}>focus</button>
    </div>
  );
};
```

- Child 컴포넌트에서 useRef를 사용해 실제 input 요소를 참조
- useImperativeHandle(ref,()=>{...}) 을 사용해 focus 메서드만 외부로 노출
- Parent 컴포넌트에서 useRef를 사용해 Child을 참조하고 버튼 클릭시 focus() 호출

### 모달 컨트롤

```jsx
import React, { useState, useImperativeHandle, forwardRef } from "react";

// 자식 컴포넌트 (Modal)
const Modal = forwardRef((_, ref) => {
  const [isOpen, setIsOpen] = useState(false);

  useImperativeHandle(ref, () => ({
    open: () => setIsOpen(true),
    close: () => setIsOpen(false),
  }));

  if (!isOpen) return null;

  return (
    <div style={{ background: "rgba(0,0,0,0.5)", padding: "20px", position: "fixed", top: 0, left: 0, right: 0, bottom: 0 }}>
      <div style={{ background: "white", padding: "20px" }}>
        <p>모달 창입니다!</p>
        <button onClick={() => setIsOpen(false)}>닫기</button>
      </div>
    </div>
  );
});

// 부모 컴포넌트
const Parent = () => {
  const modalRef = React.useRef<{ open: () => void; close: () => void } | null>(null);

  return (
    <div>
      <button onClick={() => modalRef.current?.open()}>모달 열기</button>
      <Modal ref={modalRef} />
    </div>
  );
};

export default Parent;

```

## 정리

- useImperativeHandle은 부모가 자식의 특정 메서드에 접근할 수 있도록 함.
- 직접 DOM을 노출하는 useRef와 달리 필요한 기능만 외부로 제공.
- 모달, 커스텀 입력 필드, 애니메이션 제어 등에 유용.
- forwardRef와 함께 사용해야 함.
