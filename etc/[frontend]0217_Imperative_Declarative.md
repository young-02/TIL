# 프로그래밍 패러다임(programming Paradigm)

소프트웨어 개발을 위한 기본적인 접근 방식이나 스타일.

## 명령형 프로그래밍(Imperative Programming)

순서와 절차(어떻게 할 것인지)를 하나하나 직접 지시하는 방식

```md
1. 후라이팬을 가스레인지에 올린다.
2. 가스를 켜고 약한 불로 맞춘다.
3. 기름을 두른다.
4. 계란을 깨서 넣는다.
5. 3분간 익힌 후 뒤집는다.
6. 2분 더 익힌 후 접시에 옮긴다.
```

단계별로 정확하게 '어떻게(How)'할 것인지 지시한다.

```js
const number = [1, 2, 3, 4, 5];
const squaredNumbers = [];

for (let i = 0; i < numbers.length; i++) {
  squaredNumbers.push(numbers[i] ** 2);
}

console.log(squaredNumbers); //[1,4,9,16,25]
```

- 명확히 실행순서를 하나씩 지시
- for 루프를 사용하여 직접 ㅑ를 관리, 배열 요소를 순회하면서 값 변경

## 선언형 프로그래밍(Declarative Programming)

결과(무엇을 할 것인지)만 말하고, 세부적인 과정은 알아서 처리하는 방식

```md
계란 후라이를 만들어줘
```

내가 어떻게 만들지 설명할 필요 없이 결과(What)만 말한다.

```js
const numbers = [1, 2, 3, 4, 5];
const squaredNumbers = numbers.map((number) => number ** 2);

console.log(squaredNumbers); //[1,4,9,16,25]
```

- 반복문 없이 각 요소를 제곱한 배열을 만들어라 라는 의도를 한줄로 표현
- map() 함수가 배열의 각 요소를 자동으로 순회하고 새로운 배열을 생성

## 정리

|            | 명령형(imperative)          | 선언형(Declarative)                      |
| ---------- | --------------------------- | ---------------------------------------- |
| 설명       | 어떻게 실행할지 직접지시    | 무엇을 할지 선언                         |
| 코드스타일 | for루프, 반복문 같은 절차식 | map(),filter(),reduce() 같은 함수형 방식 |
| 장점       | 세부적인 제어 가능          | 코드가 간결하고 가독성 좋음              |
| 단점       | 코드가 복잡해질 수 있음     | 디버깅이 어려울 수 있음                  |

- `자바스크립트`는 명령어프로그래밍 스타일을 기본적으로 지원하지만, 함수형 프로그래밍도 가능하다.
- `리액트`는 선언형 프로그래밍을 기반으로 만들어 졌다.

|            | Javascript(명령형)                             | React(선언형)                       |
| ---------- | ---------------------------------------------- | ----------------------------------- |
| 방식       | 직접 DOM을 조작                                | 상태를 선언하면 자동으로 UI업데이트 |
| 예제       | document.getElementById('id'),addEventListener | useState, onClick                   |
| 코드스타일 | 실행 순서를 명령으로 지시                      | 원하는 결과만 선언                  |
| 유지보수   | 복잡하고 실수하기 쉬움                         | 코드가 간결하고 직관적              |

:rocket: "React는 Javascript 기반이지만, 선언형 스타일로 UI를 다루는 라이브러리이다."

## 참고

https://yozm.wishket.com/magazine/detail/2083/

## 참고 후 알아두면 좋을 것.

라액트 Concurrent UI 패턴 : 비동기 컴포넌트에서 결과물에 집중할수 있는 코드를 만들수 있따.

- errorBoundary
- Suspense
