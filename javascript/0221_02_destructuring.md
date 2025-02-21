# 디스트럭처링(Destructuring)

배열이나 객체에서 필요한 값만 쉽게 추출하는 문법
코드를 간결하고 가독성 있게 작성할 수 있도록 도와준다.

## 1.배열 디스트럭처링(Array Destructuring)

배열의 값을 변수에 한 번에 할당할 수 있다.

```js
const numbers = [1, 2, 3];
const [a, b, c] = numbers;

console.log(a); // 1
console.log(b); // 2
console.log(c); // 3
```

:white_check_mark : number배열에서 각 요소를 변수 a,b,c에 할당 <br>
:white_check_mark: 인덱스 순서대로 값을 가져온다.

### (1)일부요소만 할당하기

```js
const colors = ["red", "green", "blue"];
const [, secondColor] = colors;

console.log(secondColor); // "green"
```

:white_check_mark: 첫번째 요소는 무시하고 두번째 요소만 할당

### (2) 나머지 요소 받기 (rest 연산자)

나머지 요소들을 새로운 배열로 묶을 수도 있다.

```js
const fruits = ["apple", "banana", "cherry", "date"];
const [first, ...rest] = fruits;
console.log(first); // "apple"
console.log(rest); // ["banana", "cherry", "date"]
```

:white_check_mark: 첫번째 요소는 변수에 할당하고 나머지 요소들은 배열로 묶어서 변수에 할당

### (3) 기본값 할당하기

배열 요소가 부족하면 기본값을 설정할 수 도 있다.

```js
const scores = [80];
const [math = 50, english = 50] = scores;

console.log(math); // 80
console.log(english); // 50
```

:white_check_mark: 기본값이 설정되어 있으면 기본값이 할당된다.

## 2. 객체 디스트럭처링 (object Destructuring)

객체에서 원하는 속성만 골라서 변수로 만들 수 있다.

```js
const person = { name: "Alice", age: 25, city: "New York" };
const { name, age, city } = person;

console.log(name); // "Alice"
console.log(age); // 25
console.log(city); // "New York"
```

:white_check_mark: name,age,city를 객체에서 추출하여 동일한 이름의 변수에 저장

### (1) 변수 이름 바꾸기(Alias)

키 이름과 다른 변수명을 사용하고 싶다면 `:`을 사용하면 된다.

```js
const user = {username:'Bob, email:'bob@example.com}

const {username:userName, email:userEmail}= user;
console.log(userName); // "Bob"
console.log(userEmail); // "bob@example.com"
```

:white_check_mark: username을 userName으로 변경하여 할당

### (2) 기본값 설정하기

객체에 값이 없는 경우 기본값을 할당할 수도 있다.

```js
const settings = { theme: "dark" };
const { theme, language = "English" } = settings;

console.log(theme); // "dark"
console.log(language); // "English"
```

:white_check_mark: language에 기본값이 설정되어 있으면 기본값이 할당된다.

### (3) 나머지 속성 받기 (rest 연산자)

필요한 값만 변수로 받고, 나머지는 다른 객체로 저장할 수도 있다.

```js
const person = { name: "Alice", age: 25, city: "New York", country: "USA" };

const { name, age, ...rest } = person;
console.log(name); // "Alice"
console.log(age); // 25
console.log(rest); // {city: "New York", country: "USA"}
```

:white_check_mark: name과 age를 변수로 받고, 나머지는 rest 객체로 저장

## 3. 함수 파라미터에서 디스트럭처링 사용하기

함수의 매개 변수에서도 사용할 수 있다.

```js
const user = {id:1, username:'Alice', role:'admin'}

function printUser((username,role):{username:string, role:string}){
  console.log(`User:${username}, Role:${role}`)
}

printUser(user) // User:Alice, Role:admin
```

:white_check_mark: 함수 인지로 객체를 받아서, 필요한 속성맘ㄴ 분해하여 사용 <br>
:white_check_mark: {username, role}을 바로 추출하여 printUser 함수 내에서 사용

## 4. 중첩된 구조 디스트럭처링(Nested Destructuring)

객체나 배열이 중첩되어 있어도 디스트럭처링을 사용할 수 있다.

```js
const company = {
  name: "TechCorp",
  location: {
    city: "San Francisco",
    country: "USA",
  },
  employees: ["Alice", "Bob", "Charlie"],
};

const {name: companyName, location:{city, country}, employees[firstEmployßee]} = company
console.log(companyName) // "TechCorp"
console.log(city) // "San Francisco"
console.log(country) // "USA"
console.log(firstEmployee) // "Alice"
```

:white_check_mark: location 객체에서 `city와` `country를` 직접 추출할 수 있다. <br>
:white_check_mark: employees 배열에서 첫 번째 요소 ('Alice')를 firstEmployee변수에 저장

## 정리

### 배열 디스트럭처링

- 배열 요소를 순서대로 변수에 할당 가능
- 나머지 요소를 rest 연산자로 받을 수 있음
- 기본값을 설정할 수 있음.

### 객체 디스트럭처링

- 객체 속성을 변수에 할당 가능(순서 무관)
- 변수명을 변경할 수 있음(`:` 사용)
- 기본값을 설정할 수 있음
- 나머지 속성을 `rest`연산자로 받을 수 있음.

  ### 활용예시

  - 함수 매개변수에서 사용 가능
  - 중첩된 객체와 배열에서도 사용 가능
