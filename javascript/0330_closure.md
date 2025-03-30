# 클로저(closure)?

클로저란 함수가 생성될 때의 환경(Lexical Environment)를 기억하고, 생성된 이후에도 해당 환경에 접근할 수 있는 함수를 말한다.

## 클로저가 만들어 지는 원리

클로저는 함수가 선언될 때의 스코프를 기억 한다는 점에서 중요한 개념이다.
자바스크립트에서 함수는 실행될 때마다 새로운 실행컨텍스트 (Execution Context)를 생성하는데, 내부 함수는 바깥함수의 변수를 참조할 수 있다.<br>
이때, 바깥 함수가 실행을 마치고 사라져도 내부 함수는 바깥 함수의 변수를 계속 기억할 수 있다.
즉, 함수가 선언될 당시의 환경(Lexical Scope)을 기억하는 것이 클로저의 핵심이다.

```js
function outer() {
  let count = 0; //외부함수의 변수

  return function inner() {
    //내부 함수 (클로저)
    count++; // 외부 변수에 접근
    console.log(count);
  };
}

const counter = outer(); // outer() 실행 후, 내부 함수 반환
counter(); //1
counter(); //2
counter(); //3
```

1. outer() 함수가 실행되면 count 변수를 포함한 환경이 생성된다.
2. outer() 함수 내부에서 inner()함수를 반환한다.
3. counter 변수에는 inner() 함수가 저장되지만, count 변수는 사라지지 않는다.
4. counter()를 호출할때 마다 count가 증가 한다.
   - count는 outer() 함수 실행이 끝났어도 메모리에 유지된다.
   - 내부 함수 inner()가 count 변수를 참조하기 때문이다.

## 클로저 특징

1. 외부 함수의 변수에 접근 가능: 클로저는 외부함수의 변수 (비공개 데이터)를 캡슐화하여 유지할 수 있다.
2. 데이터 은닉 가능 : 클로저를 사용하면 외부에서 직접 접근할 수 없는 변수를 만들 수 있다.
3. 상태 유지 가능: 클로저를 이용하면 함수 실행 이후에도 변수 상태를 유지할 수 있다.

## 클로저 활용 예시

### 1. 데이터 은닉

```js
function createCounter() {
  let count = 0; // 외부에서 접근 불가능한 변수

  return {
    increment: () => {
      count++;
      console.log(count);
    },
    decrement: () => {
      count--;
      console.log(count);
    },
    getCount: () => count,
  };
}

const counter = createCount();
counter.increment(); //1
counter.increment(); //2
console.log(counter.getCounter()); //2
console.log(counter.count); //undefined(직접접근 불가능)
```

- count 변수는 createCounter() 내부에서만 접근 가능하며, increment()와 decrement()메서드를 통해서만 수정할 수 있다.

### 2. 특정 조건을 만족하는 함수 생성

```js
function makeMultiplier(multiplier) {
  return function (num) {
    return num * multiplier;
  };
}

const double = makeMultiplier(2);
console.log(double(5)); //10

const triple = makeMultiplier(3);
console.log(double(5)); //15
```

- makeMultiplier(2)를 호출하면 내부에서 multiplier 값이 2로 설정된 클로저가 생성된다.
- double(5)를 호출하면 5\*2가 수행된다.

## 클로저 사용시 중의점

1. 메모리 누수 가능성

   - 클로저는 외부 함수의 변수를 계속 참조하므로, 불필요한 데이터가 메모리에 남을 수 있다.
   - 필요하지 않은 경우 클로저참조를 제거하는 것이 중요하다.

2. 과도한 사용 주의
   - 모든 함수가 클로저를 사용할 필요는 없다.
   - 클로저를 남발하면 코드가 복잡해질 수 있다.

## 정리

- 클로저란? 함수가 선언될 때의 환경을 기억하고, 실행된 이후에도 접근할 수 있는 함수
- 왜 중요한가? 데이터 은닉, 상태 유지 , 메모리 효율성 등을 활용할 수 있음
- 사용예시
  - 상태 유지
  - 데이터 은닉
  - 커스텀 함수 생성

클로저는 자바스크립트의 강력한 기능 중 하난로, 함수형 프로그래밍과 객체형 프로그래밍에서 유용하게 활용된다.
