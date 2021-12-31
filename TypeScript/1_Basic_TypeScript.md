### 출처: [Book-Modern Full Stack Development](https://www.amazon.com/Modern-Full-Stack-Development-TypeScript-Node-js/dp/1484257375) 를 읽고 정리했습니다. 자세한 내용과 예제 코드는 일부 삭제/수정하고, 전체적인 내용만 간략히 다뤘습니다. 

# TypeScript

개발자들이 인정한 JavaScript의 문제점들을 고려해서 개발한 언어가 TypeScript이다. JS의 유효한 코드는 TypeScript에서도 유효하지만, TypeScript에서는 JS 위에 몇가지 사항을 더 추가했다고 보면 되며, 핵심 사항은 **데이터 타입**이다. 만약 숫자 타입에 문자열을 입력하면, 에러가 발생하게 되고, 어딘지 빠르게 나타낸다. 하지만, **이는 개발 때만 해당되는 이야기이고, runtime에는 적용되지 않는다**.

# JS랑 차이점

1. 브라우저나 Node에서 TypeScript 코드를 직접 실행할 수 없기 때문에, TS(TypeScript)는 컴파일 과정이 필요하다.
2. 모던한 JS 특징들을 지원한다. 또 컴파일 시, 옛날 버전의 JS 코드로도 변환이 가능하다 (Babel과 비슷). 

# 설치

```bash
npm install typescript
```

# 실행

```bash
tsc <filename>
```

## 1. Configuring TypeScript Compilation

한번에 여러 개의 파일을 컴파일 하고 싶을때는, tsconfig.json 파일을 설정하면 된다. 

참고로, **tsc는 tsconfig.json 파일이 있으면, 현재 디렉토리 그리고 하위디렉토리의 파일들을 기본(default)으로 컴파일 한다**. 

따라서 컴파일 하고 싶지 않은 파일이 있다면, “exclude”에 파일들을 나열하면 된다. 

자세한 것은 [https://www.typescriptlang.org/docs/handbook/tsconfig-json.html](https://www.typescriptlang.org/docs/handbook/tsconfig-json.html) 

### 1.1 tsconfig.json 생성

```bash
tsc -init
```

### 1.2 Enabled Default Options

- **target** (es5): ECMAScript(JS) target version 명시
    - es3, es5, es2015, es2016, es2017, es2018, es2019, or esnext
- **module** (commonjs): 사용할 module loader system 명시
    - none, commonjs,amd, system, umd, es2015, or esnext
- **strict** (true): 모든 strict type-checking 옵션을 가능하게 한다.
- **esModuleInterop** (true): 모든 import에 대해 namespace 객체를 생성하여 CommonJS와 ES modules 사이 상호 운용성(interoperability)이 만들어지는 것을 가능하게 한다.

# Practice

## 1. Type Annotation

TS에서 타입을 따로 지정하지 않는다면 ‘**any**’ 타입으로 나타나진다. JS에서는 타입을 지정하지 않아도 되지만, **TS에서는 항상 타입을 지정해야 하며**, 만약 실제로 어떤 타입도 된다 하면 ‘any’로 지정해도 된다. 

### 1.1 Function Argument

아래 코드는 ‘words’에는 문자열 타입만 올 수 있도록 타입을 지정한 것이다. 

```jsx
// words 는 string type
function HelloWorld(words: string) {
	alert(words);
}
```

### 1.2 Function Return

반환되는 값도 타입 지정이 가능하다.

```jsx
function concatStrings(str: string): string { }
```

### 1.3 Variable

```jsx
let a: string = "Hello World";
```

## 2. Supported Types

1. **String**

```jsx
const saying: string = "Hello World!";
```

1. **Number**

```jsx
const a: number = 10;
const b: number = 10.10;
const c: number = 0xf001; //octal
const d: number = 0o744; //octal
```

1. **Boolean**

```jsx
const itItOkay: boolean = true;
```

1. **Any**

```jsx
let food: any = "pizza";
food = 101; // This is now okay
```

1. **Arrays**

```jsx
const animals: string[] = [ "Cat", "Dog" ];
const objects: any[] = [ "Cat", 12 ];
```

1. **Tuple**

```jsx
const authors: [ string, number ] = [ "Frank", 46 ];
```

1. **Enums**

Enum은 JS에서 지원하지 않는, TS에서 쓰이는 문법이다.  enum을 쓰면 차례로 값이 0,1,2 ... 할당되지만, 만약 원한다면 Jack처럼 특정 값을 직접 할당할 수 있다. 
Alice는 자연스럽게 그 다음 값인 101이 할당된다. 

```jsx
//const Pizza = 0;
//const FriedChicken = 1;
//const IceCream = 2;

enum Name { Lina, Joe, Jack=100, Alice};
let selectedName: Name.Lina;
alert(selectedName);
```

1. **Function**

```jsx
let myCalculator: (num1: number, num2: number) => string;

function add(n1: number, n2: number): string {
 return "" + n1 + n2;
}
myCalculator = add; //okay

function multiply(a: number, b: number): number {
 return a * b;
}
myCalculator = multiply; //not okay
```

1. **Object**

```jsx
let person: {
 firstName: string, lastName: string, age: number
} = {
 firstName : "Olivia", lastName : "Hatssan", age : 32
};
```

1. **Null, Void, and Undefined**

1.1 **null**

null-like 타입이랑은 다르다. 모든 타입의 서브 타입이기 때문에, 어느 곳에도 할당이 가능하다. 

```jsx
let myFavoriteNumber: number = null;
let myFavoriteString: string = null;
```
1.2 **undefined**

undefined 마찬가지로 모든 타입의 서브타입이기 때문에 어느 곳에도 할당이 가능하다. 

```jsx
let myVariable1;
let myVariable2 = undefined;
//myVariable1 == myVariable2
```

null, undefined 가 아닌 것을 확신하고 싶을 때는 tsconfig.json 파일을 수정하면 된다.

```jsx
 "strictNullChecks": true
```

1.3 **void**

void는 **no type**을 의미하며, 함수에서 return 값에 쓰일 경우, 어떠한 값도 리턴하지 않겠다는 의미가 된다. 

void를 사용하면 오직 null만 할당이 가능하다(단, tsconfig.json에서 “strictNullChecks”가 true가 아니여야 한다) . 

## 3. Custom Type Aliases

아래와 같이 똑같은 타입의 객체를 생성한다고 하면, 코드가 중복되어서 보기 안 좋다.

```jsx
let animal1 = {
 name: "cuty", species: "cat" , age : 3
};
let animal2 = {
 name: "mimi", species: "tortoise", age : 14
};
```

‘type’을 이용해서 자신의 객체에 맞게 커스텀할 수 있다. 

```jsx
type AnimalType = {
 name: string, species: string, age: number
};

let animal1: AnimalType = {
 name: "cuty", species: "cat" , age : 3
};
let animal2: AnimalType = {
 name: "mimi", species: "reptile", age : 14
};
```

## 4. Union Types

개발할 때, any 타입은 아니지만 여러개의 타입을 받을 수 있는 변수를 원할 때가 있다. 

union 타입을 쓰면 된다.

```jsx
let myAge: number | string;
myAge = 46;
myAge = "46";
myAge = true; // comile error
```

# TypeScript == ES6 Features

하지만 모든 ES6 기능을 TS에서 쓸 수 있는 것은 아니다. 쓰지 말아야하는 기능들은 

[https://kangax.github.io/compat-table/es6/](https://kangax.github.io/compat-table/es6/) 에 자세히 나와있다. 

## 1. let, const, var

**let, const** ⇒ block scope

**var** ⇒ global scope

따라서 var은 버그를 만들 확률이 매우 높다. 특별한 이유가 아니면, 쓰지 않는 것을 권장한다. 

## 2. Arrow Functions

Arrow 함수는 “function”, “return” 이라는 키워드를 쓰지 않게 한다.

```jsx
const addNums = (a,b)=> a+b;
alert(addNums(1,2));
```

하지만, 실제 Arrow Function이 유용한 이유는 “this”에 있다. Lexical Scope 가 사용되는데

- 함수가 Global Scope 에서 호출 ⇒ this는 브라우저를 가리킴
- 함수가 객체안에서 호출 ⇒ this는 해당 객체를 가리킴

## 3. Template Literals

\ (backtick) 문자를 쓰면 

- ${ } 내부에 JS 코드를 넣을 수 있다.
- 여러 개의 라인으로 작성할 수 있다.

```jsx
alert(`Hello, ${name.toUpperCase().substr(2)}`);
alert(`Hello,
 your name is
 ${name}
`);
```

## 4. Default Parameters

```jsx
const multNums = (a: number, b: number = 10): number => a * b;
alert(multNums(3));
```

## * 5. Spread and Rest (and Optional
Arguments)

설명 잘되어있는 글: [07. spread 와 rest 문법 · GitBook (vlpt.us)](https://learnjs.vlpt.us/useful/07-spread-and-rest.html) 

**Spread Operator** “...” 는 iterable item (배열, 문자열)이 arguments에서 확장되거나, array나 객체에서 0개 이상의 key-value에서 확장될 때 쓰인다. 

```jsx
const addNums = (a?: number, b?: number): number => a + b;
const nums: number[] = [ 5, 6 ];
alert(addNums(...nums));
```

**‘?’ 은 optional argument**라 있을 수도 없을 수도 없다는 것을 의미한다. 만약 이를 사용할 경우, **argument 중 항상 마지막에 오도록** 해야한다. 

하지만, 위 코드의 경우 처음 2개의 숫자만 더해져서 alert가 된다. 만약 nums 배열에 3개 이상의 숫자가 있고, 다 더해지기 원하면 다음과 같이 코드를 수정하면 된다. 

```jsx
const addNums = (...rest: number[]): number =>
 a.reduce((acc, val) => acc + val);
const spread: number[] = [ 5, 6, 7, 8 ];
alert(addNums(...spread));
```

내용 추가하자면 함수 호출 시, parmaeter 일일이 spread[0], spread[1], spread[2] ... 이렇게 주는 것은 너무 힘들다. 그래서 배열의 값들을 “펼쳐서” 주는 의미로 spread이다.

 Rest의 경우, 함수 패러미터로 몇개의 값이 들어올지 모른다.  이때 사용하면 좋은 것이 rest 이다. 

## 6. Destructuring

TS는 2가지의 destructuring을 제공한다; **Object** & **Array**. 

**Bad**

```jsx
const person = {
 firstName : "John", lastName : "Donald", age : 50
};
const firstName = person.firstName;
const lastName = person.lastName;
const age = person.age;
```

**Good (Object)**

```jsx
const { firstName, lastName, age } = person
```

**Good (Array)**

```jsx
const vals = [ "John", "Donald", 50 ];
const [ firstName, lastName, age ] = vals;
// firstName=vals[0]
// lastName=vals[1] 
// age=vals[2]
```

# Classes

## 1. Properties

Constructor에서 properties를 선언하는 것보단, 더 엘레강스하게 선언하는 방법이 있다. 이는 JS가 더 OOL(Object-Oriented-Language) 하게 보이게 한다. 

**Not Good**

```jsx
class ExampleClass {
 constructor() {
 this.name = null;
 this.number = null;
 }
}
```

**Good (with constructor) in TS**

```jsx
class ExampleClass {
 name: string;
 number: number;
constructor(inName: string, inNumber: number) {
 this.name = inName;
 this.mass = inNumber;
 }
}
```

## 2. Member Visibility

**public** (default) - 어디서든 접근 가능

**private** - 클래스 내부에서만 접근이 가능

**protected** -  클래스 내부 + 자식 클래스(해당 클래스를 extends)만 접근이 가능

```jsx
class ParentClass {
 private name: string = "none";
 protected parentNumber: number;
 constructor(inName: string, inParentNumber: number) {
 this.name = name;
 this.parentNumber = inParentNumber;
 }
 public printName() {
    alert(this.name);
 }
}
```

## 3. Inheritance

```jsx
class ChildClass extends ParentClass {
	private isChild: boolean = true;
	constructor(){
		super("Child1", 1); //super class constructor()
	}
}

let j = new ChildClass();
j.printName(); // work
alert(j.name); //not work (private)
```


## 4. Getters and Setters

Getter/Setter는 private한 데이터에 접근할 때 사용하기 유용한 패턴으로 여겨진다. 

```jsx
class ParentClass {
 private _name: string = "No name set";
 get name() {
 return `This Animal's name is '${this._name}'.`;
 }
set name(inName: string) {
 this._name = inName;
 }
}
```

*** Note**

**_ (언더바)** 가 붙는 것은 private property를 나타내며, 이는 컨벤션이다. 맨 앞에 고정적으로(prefix)로 붙인다. 

**readonly** prefix도 있다. public이 default다.

```jsx
class Animal {
 readonly name: string = "No name set";
}
let p: Animal = new Animal();
alert(p.name); // Okay
p.name = "Tacos"; // Error
```

## 5. Static Members

“static”은 지금까지 본 instance member과는 다르며, 클래스 내부에서 선언되어도, 클래스 인스턴스가 생성되기 전에 만들어지는 property이다.

```jsx
class Animal {
 static isFurry: boolean = true;
}
alert(Animal.isFurry); // true
```

## 6. Abstract Classes

abstract class는 스스로 인스턴스를 만들 수 없는 클래스이다. interface와 비슷하지만, 그래도 일부 함수를 어느정도 구현할 수 있다는 점에서 다르다.

아래 예시에서  abstract인 BaseAnimal 클래스는 절대 만들어질 수 없고, Dog 클래스는 만들어 질 수 있음을 보인다. 

```jsx
abstract class BaseAnimal {
	 name: string;
	 age: number;
	 constructor(inName: string, inAge: number) {
		 this.name = inName;
		 this.age = inAge;
	 }
	abstract printAgeTimesNumber(anyNumber: number): void;
	 calcTenTimesAge() {
		 return this.age * 10;
	 }
}

class Dog extends BaseAnimal {
 printAgeTimesNumber(anyNumber: number) {
     // ... 
 }
}
```