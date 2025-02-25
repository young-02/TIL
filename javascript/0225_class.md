# Class

클래스(Class)는 객체지향 프로그래밍(OOP, Object-Oriented Programming)의 핵심 개념 중 하나로 객체를 생성하기 위한 청사진 역할을 한다. 우선, 객체가 무엇인지 이해 하는게 중요하다.

## 1. 객체 (Object)

객체는 속성(데이터)과 동작(메서드)을 포함하는 독립적인 단위이다.

```js
const car = {
  brand: "Tesla",
  model: "Model 3",
  drive() {
    console.log("driving...");
  },
};

console.log(car.brand); //Tesla
car.drive(); //driving..
```

`car`는 객체이며, `brand`,`model`은 속성(데이터),`drive`는 동작(메서드)이다.

## 2. 클래스란?

객체를 만들 때 마다 같은 구조를 반복해서 작성하는 건 비효율적이다.
클래스는 객체를 생성하는 틀(청사진) 역할을 해서 같은 구조를 반복해서 만들 필요가 없게 한다.

### 클래스의 역할

1. 객체를 체계적으로 만들기 위한 틀 제공
2. 여러 객체를 일관된 방식으로 생성할 수 있도록 도움
3. 코드를 재사용하고 유지보수하기 쉽게 만듦

## 3.클래스 문법

객체를 만들기 위해 클래스를 정의하고, 그 클래스를 이용해 여러 개의 객체를 생성할 수 있다.

### 기본 클래스 선언

```js
class Car {
  brand: string;
  model: string;

  constructor(brand: string, model: string) {
    this.brand = brand;
    this.model = model;
  }

  drive() {
    console.log(`${this.brand} ${this.model} is driving...`);
  }

  const myCar = new Car('Tesla', "Model3");
  console.log(myCar.brand)// Tesla
  myCar.drive() //Tesla Model3 is driving...
}
```

### 2. 클래스의 구성요소

1. 속성(Property):brand, model 같은 데이터
2. 생성자(Constructor):constructor는 객체가 생성될 때 자동으로 실행되는 속성을 초기화 한다.
3. 메서드(Method):drive() 처럼 특정 동작을 정의하는 함수

## 4.접근 제한자(Access Modifier)

클래스의 속성이나 메서드의 접근 범위를 설정할 수 있다.
typeScript에서는 `public`, `private`, `protected` 키워드를 사용한다
|접근 제한자|설명|
|---|---|
|public|모든 곳에서 접근 가능(기본값)|
|private|클래스 내부에서만 접근 가능|
|protected|클래스 내부 및 상속된 클래스에서만 접근 가능|

### public: 기본값 (어디서든 접근 가능)

```js
class Person {
  public name:string; // public이므로 어디든 접근 가능

  constructor(name:string){
    this.name = name
  }
}

const person = new Person('Alice')
console.log(person.name) //Alice
```

### private:클래스 내부에서만 접근 가능

```js
class BankAccount {
   private balance:number;

   constructor(initialBalance:number){
    this.balance = initialBalance;
   }

   deposit(amount:number){
    this.balance += amount
   }

   getBalance(){
    return this.balance
   }
}

const account = new BankAccount(1000);
account.deposit(500)
console.log(account.getBalance())//1500
console.log(account.balance)//error - private 속성으로 접근 불가
```

- private 장점: 클래스 내부에서만 값이 변경되므로 데이터 보호가 가능함.

### 상속(inheritance)

상속은 기존 클래스를 확장하여 새로운 클래스를 만들수 있게 한다

```js
class Animal {
  name: string;

  constructor(name: string) {
    this.name = name;
  }

  makeSound() {
    console.log("Some generic sound");
  }
}

// Dog 클래스가 Animal 클래스를 상속함
class Dog extends Animal {
  breed: string;

  constructor(name: string, breed: string) {
    super(name); // 부모클래스의 생성자 호출
    this.breed = breed;
  }

  makeSound() {
    console.log("Woof! Woof!");
  }
}

const dog = new Dog("Buddy", "Golden Retriever");
dog.makeSound(); // Woof! Woof!
console.log(dog.name); // Buddy
console.log(dog.breed); // Golden Retriever
```

상속의 장점

- 중복 코드 없이 부모 클래스의 기능을 재사용할 수 있음.
- 필요에 따라 메서드를 오버라이딩(덮어쓰기)할 수 있음.

### 추상클래스(Abstract Class)

추상 클래스는 직접 객체를 생성할 수 없고, 상속을 통해서만 사용 하는 클래스이다.

```js
abstract class Shape{
  abstract getArea():number; //자식 클래스에서 구현해야함

}

class Circle extends Shape{
  radius:number;

  constructor(radius:number){
    super();
    this.radius = radius;
  }

  getArea():number{
    return Math.PI * this.radius * this.radius
  }
}

const circle = newCircle(5)
console.log(circle.getArea()) //78.53981633974483
```

추상 클래스 역할

- 특정 클래스가 반드시 구현해야 하는 메서드를 강제 할 수있음.
