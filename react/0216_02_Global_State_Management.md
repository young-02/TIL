# 전역상태관리 useContext, Redux 사용하는 차이

전역상태관리(Global State Management)를 해야하는 경우 `useContext`와 `Redux`를 사용하는데 차이를 알려면 상태(State)가 얼마나 복잡한지 에 따라 선택하는 것이 좋다.

## 1. `useContext`와 `Redux`의 기본개념

### useContex

- React의 내장기능, `Context API`를 사용해서 전역상태를 공유할 수 있다.
- `useContext`는 단순한 전역 상태 공유에 적합하고, 추가적인 기능을 제공하지 않는다.

### redux

- 상태 관리 라이브러리로 더 큰 규모의 애플리케이션에서 복잡한 상태를 예측 가능하게 관리할 수 있다.
- 전역 상태 저장소(Store)를 만들고, 상태를 변경할 때 Reducer(리듀서)를 통해 상태를 업데이트 한다.
- useReducer와 비슷한 개념이지만, 미들웨어(Redux Thunk, Redux Saga)등을 통해 비동기 상태관리도 가능하다.

## 2. `useContext`와 `Redux`의 차이점

| ---              | useContext                                              | Redux                                         |
| ---------------- | ------------------------------------------------------- | --------------------------------------------- |
| 기본개념         | React의 내장된 전역 상태 관리 기능                      | 전역 상태 관리 라이브러리                     |
| 복잡한 상태 관리 | 간단한 전역 상태 관리에 적합                            | 복잡한 상태 관리에 적합                       |
| 상태변경방식     | `useState`, `useReducer`와 함께 사용                    | `Reducer`와 `Action`을 통해 상태 변경         |
| 비동기 처리      | 기본제공하지 않는다(추가 로직 필요)                     | `Redux Thunk`,`Redux Saga`등 미들웨어 제공    |
| 성능             | context값이 변경되면 모든 하위 컴포넌트가 리렌더링 된다 | 필요한 컴포넌트만 선택적으로 리렌더링 가능    |
| 전역상태 구조화  | 상태 구조를 직접 관리해야함                             | `Store`,`reducer`,`action` 등 구조화 되어있음 |
| 커뮤니케이션     | 컴포넌트 간 직접 통신 불가능                            | 컴포넌트 간 직접 통신 가능                    |
| 러닝커브         | 쉽고 빠르게 이해 가능                                   | 초기 학습 비용이 높음                         |

## `useContext` 사용 예제

테마(theme)상태를 전역으로 관리 할때 효율적이다.

```jsx
//1.ThemeContext.tsx(Context 생성)
import { createContext, useState, useContext } from "react";

//Context 생성
const ThemeContext = createContext(null);

// Context Provider 생성
export function ThemeProvider({ children }) {
  const [theme, setTheme] = useState("light");

  return (
    <ThemeContext.Provider value={{ theme, setTheme }}>
      {children}
    </ThemeContext.Provider>
  );
}

//useTheme 훅 생성(편리한 사용을 위해)
export function useTheme() {
  return useContext(ThemeContext);
}
```

```jsx
//3. ThemeToggle.tsx
import { useTheme } from "./ThemeContext";

function ThemeToggle() {
  const { theme, setTheme } = useTheme();

  return (
    <div>
      <p>현재테마: {theme}</p>
      <button onClick={() => setTheme(theme === "light" ? "dark" : "light")}>
        Toggle Theme
      </button>
    </div>
  );
}

export default ThemeToggle;
```

:white_check_mark: 간단한 전역 상태 공유 할수 있음, 하지만 상태가 많아지면 리렌더링 성능 문제가 발생할 수 있다.

## `Redux` 사용 예제

복잡한 상태 관리가 필요한 경우 적합
예- 로그인 사용자정보와 같은 상태는 앱 전역에서 관리해야 하고 여러 컴포넌트에서 변경될수 있다.

```jsx
//1. store.ts(Redux Store 설정)
import { configureStore, createSlice, payloadAction } from "@reduxjs/toolkit";

// Slice 생성 (상태 정의 + Reducer)
const userSlice = createSlice({
  name: "user",
  initialState: { name: "", loggedIn: false },
  reducers: {
    login: (state, action: PayloadAction<string>) => {
      state.name = action.payload;
      state.loggedIn = true;
    },
    logout: (state) => {
      state.name = "";
      state.loggedIn = false;
    },
  },
});

// Store 생성
const store = configureStore({
  reducer: {
    user: userSlice.reducer,
  },
});
//Action export
export const { login, logout } = userSlice.actions;
export type RootState = ReturnType<typeof store.getState>;
export type AppDispatch = typeof store.dispatch;
```

```tsx
//2. App.tsx(Redux Provider 설정)
import { Provider } from "react-redux";
import { store } from "./store";
import useProfile from "./UserProfile";
function App() {
  return (
    <Provider store={store}>
      <UserInfo />
    </Provider>
  );
}
export default App;
```

```tsx
//3.userProfile.tsx(상태 사용)

import { useSelector, useDispatch } from "react-redux";
import { login, logout, RootState } from "./store";

function UserProfile() {
  const { name, loggedIn } = useSelector((state: RootState) => state.user);
  const dispatch = useDispatch<AppDispatch>();

  const handleClick = () => {
    if (loggedIn) {
      dispatch(logout());
    } else {
      dispatch(login("홍길동"));
    }
  };

  return (
    <div>
      {loggedIn ? <p>안녕하세요, {name}님!</p> : <p>로그인이 필요합니다.</p>}
      <button onClick={handleClick}>{loggedIn ? "로그아웃" : "로그인"}</button>
    </div>
  );
}

export default UserProfile;
```

:white_check_mark:`useSelector
()`를 사용하여 필요한 상태만 가져올 수 있어서 불필요한 리렌더링을 줄일수 있다.

## 5. 언제 `useContext` vs `Redux`를 사용할까?

### `useContext`

- 전역상태가 간단한 경우
- 데이터 흐름이 비교적 단순 할때
- props drilling문제를 해결할 때

:white_check_mark: 예제

- 다크모드.라이트모드 테마 관리
- 현재 로그인된 사용자 이름 한줄 표시

### `Redux`

- 전역상태가 많고 복잡한 경우
- 여러 컴포넌트에서 자주 상태를 변경하는 경우
- 비동기처리(서버에서 데이터 가져오기 등)가 필요한 경우

:white_check_mark: 예제

- 로그인/인증상태관리
- 쇼핑몰 장바구니 관리
- 서버에서 받아오는 데이터(API)관리
