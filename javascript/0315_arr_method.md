# array method

## 추가

- push(요소) : 배열의 맨 뒤에 추가
- unshift(요소) : 배열 맨 앞에 추가

## 삭제

- pop() : 배열 맨 뒤에 삭제
- shift() : 배열 맨 앞에 삭제

## 수정

- splice(인덱스,갯수) :원하는 인덱스 요소에서 원하는 갯수를 삭제
- splice(인덱스): 원하는 인덱스 요소 부터 이후 요소 모두 삭제
- splice(인덱스,갯수, 요소):원하는 인덱스부터 원하는 갯수르 삭제후 새로운 요소 추가

## 검색

- includes(요소) : 요소를 검색했을때 있는지 여부 확인 (true/false)
- indexOf(요소): 배열의 해당 요소의 인덱스 값 확인 (0,1,2,3...)
- lastIndexOf(요소): 배열의 맨뒤에서 부터 인덱스 값 확인

## 특정위치의 요소 가져오기

- at(인덱스) : 인덱스의 요소를 가져온다. 마이너스로 뒤의 요소값을 가지고 올수 있다.at(-1)

## 배열 -> 문자열

- join(string) : 배열의 모든 요소를 쉼표나 지정된 구분 문자열로 구분하여 연결한 새 문자열을 만들어 반환한다.

```js
const fruits = ["apple", "banana", "cherry"];
console.log(fruits.join()); // "apple,banana,cherry" (기본값: 쉼표)
console.log(fruits.join("")); //"applebananacherry" (구분자 없이 붙이기)
```
