# Ch2. 알아두어야 할 자바스크립트
<br>

## 2.1 ES2015+
----

### 1. ES2015+ ?

- 2015년 자바스크립트 문법에 큰 변화가 있었음. 이제는 ES2015 이상의 자바스크립트 문법을 배울 때다. 

- ES2015 이상의 자바스크립트를 통틀어 ES2015+라고 하겠음.

- 노드 6 버전부터는 ES2015 문법을 사용할 수 있다.
<br>

### 2. const, let

- 보통 자바스크립트를 배울 때는 var로 변수 선언하는 방법부터 배움. 하지만 var은 이제 const와 let으로 대체함.

**const와 let의 공통점 : 블록 스코프(범위)**
````javascript
if (true) {
  var x = 3;
}
console.log(x); // 3

if (true) {
  const y = 3;
}
console.log(y); // Uncaught ReferenceError: y is not defined
````
- var은 함수 스코프를 가지므로 if문의 블록과 관계없이 접근할 수 있음.

- const와 let은 블록 스코프를 가지므로 블록 밖에서는 변수에 접근할 수 없음.

- 함수 스코프 대신 블록 스코프를 사용함으로써 호이스팅 같은 문제도 해결되고 코드 관리도 수월해짐.

> **호이스팅?**
> - 함수 안에 있는 선언들을 모두 끌어올려서 해당 함수 유효 범위의 최상단에 선언하는 것을 말한다.
> 
> - 즉, 함수 내에서 아래쪽에 존재하는 내용 중 필요한 값들을 끌어올리는 것이다.
> 
> - 실제로 코드가 끌어올려지는 건 아니며, 자바스크립트 Parser 내부적으로 끌어올려서 처리하는 것이다.
<br>

**const와 let의 차이점 : const는 상수 개념.**
````javascript
const a = 0;
a = 1; // Uncaught TypeError: Assignment to constant variable.

let b = 0;
b = 1; // 1 / 가능

const c; // Uncaught SyntaxError: Missing initializer in const declaration
````
- const는 상수의 개념.
  - 한 번 값을 할당하면 다른 값을 할당할 수 없음.

  - 초기화할 때 값을 할당하지 않으면 에러 발생.

- let은 다른 값 할당 가능.
<br>

### 3. 템플릿 문자열

- ES2015 문법에 새로운 문자열이 생겼음. 백틱(`)으로 감싸서 사용함.

- 이 문자열의 특이점은 문자열 안에 변수를 넣을 수 있다는 것이다.

**기존 ES5 문법을 사용한 문자열**
````javascript
var num1 = 1;
var num2 = 2;
var result = 3;
var string1 = num1 + ' 더하기 ' + num2 + '는 \'' + result + '\'';
console.log(string1); // 1 더하기 2는 '3'
````
- 문자열 string1은 띄어쓰기와 변수, 더하기 기호 때문에 가독성이 좋지 않음.

- 작은 따옴표를 이스케이프(escape)하느라 코드가 지저분함.

**ES2015+ 문법**
````javascript
const num3 = 1;
const num4 = 2;
const result2 = 3;
const string2 = `${num3} 더하기 ${num4}는 '${result2}'';
console.log(string2); // 1 더하기 2는 '3'
````
- ${변수} 형식으로 변수를 더하기 기호 없이 문자열에 넣을 수 있음.

- 기존 따옴표 대신 백틱을 사용해서 큰따옴표나 작은 따옴표도 함께 사용할 수 있음.
<br>

### 4. 객체 리터럴

**기존 방식**
````javascript
var sayNode = function() {
  console.log('Node');
};
var es = 'ES';
var oldObject = {
  sayJS: function() {
    console.log('JS');
  },
  sayNode: sayNode,
};
oldObject[es + 6] = 'Fantastic';
oldObject.sayNode(); // Node
oldObject.sayJS(); // JS
console.log(oldObject.ES6); // Fantastic
````

**ES2015+ 문법**
````javascript
const newObject = {
  sayJS() {
    console.log('JS');
  },
  sayNode,
  [es + 6]: 'Fantastic';
};

newObject.sayNode(); // Node
newObject.sayJS(); // JS
console.log(newObject.ES6); // Fantastic
````
- oldObject와 newObject를 비교해보자.

  1. sayJS와 같이 객체의 메서드를 정의할 때 콜론(:)과 function을 붙이지 않아도 됨.

  2. sayNode: sayNode 와 같이 속성명과 변수명이 같은 경우에는 한번만 써도 됨.
  ````
      { name: name, age: age} // ES5
      { name, age } // ES2015
  ````
  3. 객체의 속성명을 동적으로 생성 가능. ES6이라는 속성명을 만들려면,  
  <br>
  
    - 예전 문법 : 객체 리터럴(oldObject) **바깥**에서 [es + 6]을 해야 했음.
    - ES2015+ : 객체 리터럴(newObject) **안**에서 [es + 6]가 속성명으로 바로 사용됨.
<br>

### 5. 화살표 함수

- 화살표 함수라는 새로운 함수가 추가 되었으며, 기존 function() {}도 그대로 사용 가능.

````javascript
function add1(x, y) {
  return x + y;
}

const add2 = (x, y) => { // function 선언 대신 => 기호로 함수 선언
  return x + y;
}

const add3 = (x, y) => x + y; // 화살표 함수 내부에 return문 밖에 없는 경우 return문 생략 가능

const add4 = (x, y) => (x + y); // 위의 식을 보기 좋게 소괄호로 감쌀 수 있음

function not1(x) {
  return !x;
}

const not2 = x => !x; // 매개변수가 한 개면 매개변수를 소괄호로 안 묶어도 됨
````
- 기존 function과 다른 점은 this 바인드 방식이다.


**기존 방식**

````javascript
var relationship1 = {
  name: 'zero',
  friends: ['nero', 'hero', 'xero'],
  logFriends: function() {
    var that = this; // relationship1을 가르키는 this를 that에 저장
    this.friends.forEach(function (friend) {
      console.log(that.name, friend);
    });
  },
};
relationship1.logFriends();
````
- logFriends()안에 forEach문에서 function()문을 사용함.
- 각자 다른 함수 스코프의 this를 가지므로 that이라는 변수를 사용해서 relationship1에 간접적으로 접근하게 함.

**ES2015+ 문법**
````javascript
const relationship2 = {
  name: 'zero',
  friends: ['nero', 'hero', 'xero'],
  logFriends() {
    this.friends.forEach(friend => {
      console.log(this.name, friend);
    });
  },
};
relationship2.logFriends();
````
- 여기서는 화살표 함수를 사용했기 때문에 바깥 스코프인 logFriends()의 this를 그대로 사용할 수 있음.

- 상위 스코프의 this를 그대로 내려받는다고 이해하면 됨.
<br>

### 6. 구조분해 할당

- 구조분해 할당을 사용하면 객체와 배열로부터 속성이나 요소를 쉽게 꺼낼 수 있음.

- 다음은 객체의 속성을 같은 이름의 변수에 대입하는 코드이다.

**기존 버전**
````javascript
var candyMachine = {
  status : {
    name: 'node',
    count: 5,
  },
  getCandy: function() {
  this.status.count--;
  return this.status.count;
  },
};
var getCandy = candyMachine.getCandy;
var count = candyMachine.status.count;
````

**ES2015+ 버전**
````javascript
const candyMachine = {
  status : {
    name: 'node',
    count: 5,
  },
  getCandy() {
  this.status.count--;
  return this.status.count;
  },
};
const { getCandy, status: { count } } = candyMachine; // getCandy 와 count 변수 초기화
````
- candyMachine 객체 안의 속성을 찾아서 변수와 매칭함.

- count와 같이 여러 단계 안의 속성도 찾을 수 있음. ( candyMacine > status > count )

- 배열에 대한 구조분해 할당 문법도 존재함.

**기존 버전**
````javascript
var array = [ 'node.js', {}, 10, true ];
var node = array[0];
var obj = array[1];
var bool = array[3];
````

**ES2015+ 버전**
````javascript
const array = [ 'node.js', {}, 10, true ];
const [node, obj, , bool ] = array;
````
<br>

### 7. 클래스

- 클래스 문법도 추가. 하지만 다른 언어처럼 클래스 기반으로 동작하는 것이 아니라 프로토타입 기반으로 동작함.

- 보기 좋게 클래스로 바꾼 것이라고 이해하면 된다.

**프로토타입 상속 예제 코드**
````javascript
var Human = function(type) {
  this.type = type || 'human';
};

Human.isHuman = function(human) {
  return human instanceof Human; // human이 Human에 속하거나 Human을 상속받는 클래스에 속하면 true가 반환됩니다.
}

// Human.prototype이라는 빈 Object가 어딘가에 존재하고, Human 함수로부터 생성된 객체들은 어딘가에 존재하는 Object에 들어있는 값을 모두 갖다쓸 수 있습니다. 함수도 마찬가지.
Human.prototype.breath = function() { 
  alert('h-a-a-a-m');
};

var Zero = function(type, firstName, lastName) {
  Human.apply(this, arguments);
  this.firstName = firstName;
  this.lastName = lastName;
};

Zero.prototype = Object.create(Human.prototype);
Zero.prototype.constructor = Zero; // 상속하는 부분
Zero.prototype.sayName = function() {
  alert(this.firstName + ' ' + this.lastName);
};
var oldZero = new Zero('human', 'Zero', 'Cho');
Human.isHuman(oldZero); // true
````

- Human 생성자 함수가 있고, 그 함수를 Zero 생성자 함수가 상속한다. 뭔가 어설픈 느낌 ...

**클래스 기반 코드**
````javascript
class Human {
  constructor(type = 'human') {
    this.type = type;
  }
  
  static isHuman(human) { // 클래스 함수
    return human instanseof Human;
  }
  
  breathe() {
    alert('h-a-a-a-m');
  }
}

class Zero extends Human { // 상속 문법
  constructor(type, firstName, lastName) {
  super(type); // Human.constructor
  this.firstName = firstName;
  this.lastName = lastName;
  }

  sayName() {
    super.breathe();
    alert(`${this.firstName} ${this.lastName}`);
  }
}

const newZero = new Zero('human', 'Zero', 'Cho');
Human.isHuman(newZero); // true
````

- 전반적으로 class 안으로 그룹화 됨. 생성자 함수는 constructor 함수로 들어감. (super)

- 다만 이렇게 클래스 문법으로 바뀌었더라도 자바 스크립트는 프로토타입 기반으로 동작한다는 것을 명심하자 !
<br>

### 8. 프로미스

