# 객체 간의 비교

```js
{} === {}
//false
```

- 객체간 비교하면 false가 나온다.
- 새로 객체를 만들어서({}) 비교 하기 때문에 같을 수가 없음.
- 배열도 마찬가지 이다.

변수안에 값을 넣고 비교해야 값이 같아 진다.

```js
const a = { name: "maru" };
const array = [1, 2, a];
console.log(a === array[2]); //true
```

- 객체 a라는 변수에 저장 하고 다시 array에서 가져 오기 때문에 같다.

## 옵셔널 체이닝 (?.)

객체 프로퍼티에 안전하게 접근하는 방법
객체가 null 또는 undefined 일수 있을 때 일반적으로 프로퍼티에 접근하면 에러가 발생한다. 하지만 옵셔널 체이닝을 사용하면 안전하게 접근할 수 있다.

```js
const user = null;
console.log(user?.name); //undefined

const user = {
  profile: null,
};
console.log(user.profile?.age); //undefined
```

- 왼쪽 값이 null 또는 undefined이면 평가를 멈추고 undefined를 반환

## null 병합 연산자

좌항의 값이 null 또는 undefined일때만 우항의 값을 반환하는 연산자이다.

```js
const result = 값 ?? 기본값;
```

- 값이 null, undefined이면 기본값 반환
- 값이 0,false,''(빈문자열) -> 그대로 반환

### ||(OR연산자)와의 차이점

||는 false로 평가되는 값까지 기본값으로 대체 한다.
하지만 null은 false, 0, ''는 정상적인 값으로 취급한다

```js
const username = "";
console.log(username || "기본이름"); // 기본이름
console.log(username ?? "기본이름"); // ''빈문자열 그대로 유지

const count = 0;
console.log(count || 10); // 10(0, false 취급됨)
console.log(count ?? 10); // 0 (정상적으로 0으로 유지)
```

### 옵셔널 체이닝과 함께 사용

옵셔널체이닝(?.)과 null 병합 연산자(??)를 함께 사용

```js
const user = {
  profile: null,
};
console.log(user.profile?.name ?? "이름없음"); //이름없음
```

- user.profile?.name -> null -> undefined로 반환
- ?? 연산자 실행 -> 이름없음으로 반환
