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

- 자바 스크립트와 노드에서는 주로 비동기를 접한다. 특히 이벤트 리스너를 사용할 때 콜백 함수를 자주 사용.

> **비동기?**
> - 특정 코드의 실행이 완료될 때까지 **기다리지 않고** 다음 코드를 먼저 수행하는 자바스크립트의 특성
<br>

- ES2015+ 는 자바 스크립트와 노드의 API들이 콜백 대신 프로미스 기반으로 재구성되며, 콜백 지옥 현상을 극복했다는 평가를 받고 있다.

````javascript
const condition = true // true면 resolve, false면 reject
const promise = new Promise(resolve, reject) => { // 프로미스 객체 생성
  if (condition) {
    resolve('성공');
  } else {
    reject('실패');
  }
});

// 다른 코드가 들어갈 수 있음

promise
  .then((message) => {
    console.log(message); // 성공(resolve)한 경우 실행
  })
  .catch((error) => {
    console.error(error); // 실패(reject)한 경우 실행
  })
  .finally(() => { // 끝나고 무조건 실행
    console.log('무조건');
  });
````

- new Promise로 프로미스를 생성할 수 있으며, 그 내부에 resolve와 reject를 매개변수로 갖는 콜백 함수를 넣는다.

- 프로미스 내부에서 resolve가 호출되면 -> then이 실행 / reject가 호출되면 catch가 실행

- finally 부분은 성공/실패 여부와 상관없이 실행

- resolve와 reject에 넣어준 인수는 각각 then과 catch의 매개변수에서 받을 수 있음.
  - resolve('성공')이 호출되면 then의 message가 '성공'이 됨.

  - reject('실패')가 호출되면 catch의 error가 '실패'가 됨.

  - condition 변수를 false로 바꿔보면 catch에서 에러가 로깅된다.

- 프로미스를 쉽게 설명하자면, **_실행은 바로 하되 결과값은 나중에 받는 객체_** 이다. 
  - 결과값은 실행이 완료된 후 then이나 catch 메서드를 통해 받는다.

````javascript
promise
  .then((message) => {
    return new Promise((resolve, reject) => {
      resolve(message);
    });
  })
  .then((message2) => {
    console.log(message2);
    return new Promise((resolve, reject) => {
      resolve(message2);
    });
  })
  .then((message3) => {
    console.log(message3);
  })
  .catch((error) => {
    console.error(error);
  });
````
- 위와 같이 then이나 catch에서 다시 다른 then이나 catch를 붙일 수 있다.
  - 이전 then의 return 값을 다음 then의 매개변수로 넘긴다. 프로미스를 return한 경우에는 프로미스가 수행된 후 다음 then이나 catch가 호출됨.

- 처음 then에서 message를 resolve하면 다음 then에서 message2로 받을 수 있음.

- 여기서 다시 message2를 resolve한 것을 다음 then에서 message3으로 받음.

- 단, then에서 new Promise를 return 해야 다음 then에서 받을 수 있다는 것을 기억해야 한다.

- 이를 이용해서 콜백을 프로미스로 바꿀 수 있다.

**콜백 함수 버전**
````javascript
function findAndSaveUser(Users) {
  Users.findOne({}, (err, user) => { // 첫 번째 콜백
    if (err) {
      return console.error(err);
    }
    user.name = 'zero';
    user.save((err) => { // 두 번째 콜백
      if (err) {
        return console.error(err);
      }
      Users.findOne({ gender: 'm' }, (err, user) => { // 세 번째 콜백
      // 생략
      });
    });
  });
}
````

- 콜백 함수가 세 번 중첩되어 있다. 이는 콜백 함수가 나올 때마다 코드의 깊이가 깊어지는 것을 알 수 있다.

- 또한 콜백 함수마다 에러도 따로 처리해줘야 해서 복잡하다.

**promise 객체 사용**
````javascript
function findAndSaveUser(Users) {
  Users.findOne({})
    .then((user) => {
      user.name = 'zero';
      return user.save();
    })
    .then((user) => {
      return Users.findOne({ gender: 'm' });
    })
    .then((user) => {
    //생략
    })
    .catch(err => {
      console.error(err);
    });
}
````
- 위 코드에서 then 메서드들은 순차적으로 실행된다. 에러도 마지막 catch에서 한 번에 처리할 수 있음.

- 모든 콜백 함수를 위와 같이 바꿀 수 있는 것은 아니고, 메서드가 프로미스 방식을 지원해야 가능하다.
  
- 예제 코드에서는 findOne과 save 메서드가 내부적으로 프로미스 객체를 가지고 있다고 가정함.
  - new Promise가 함수 내부에 구현되어 있어야 함.

**프로미스 여러 개를 한번에 실행하는 코드**
````javascript
const promise1 = Promise.resolve('성공1'); // 즉시 resolve하는 프로미스를 만드는 방법
const promise2 = Promise.resolve('성공2');
Promise.all([promise1, promise2])
  .then((result) => {
    console.log(result); // ['성공1', '성공2'];
  })
  .catch((error) => {
    console.error(error);
  });
````
- 프로미스가 여러 개 있을 때 Promise.all에 넣으면 모두 resolve 될 때까지 기다렸다가 then으로 넘어간다.

- result 매개변수에 각각의 프로미스 결과값이 배열로 들어가있음.

- Promise 중 하나라도 reject가 되면 catch로 넘어간다.
<br>

 ### 9. async/await
 
- 노드 7.6 버전부터 지원되는 기능이다. ES2017에서 추가되었으며, 알아두면 정말 편리한 기능이다.

- 프로미스가 콜백 지옥을 해결했다고 하지만 then과 catch가 계속 반복되기 때문에 여전히 코드가 장황하다. 이를 async/await 문법으로 프로미스를 사용하여 깔끔하게 줄일 수 있다.

**2.1.8절의 프로미스 코드**
````javascript
function findAndSaveUser(Users) {
  Users.findOne({})
    .then((user) => {
      user.name = 'zero';
      return user.save();
    })
    .then((user) => {
      return Users.findOne({ gender: 'm' });
    })
    .then((user) => {
    //생략
    })
    .catch(err => {
      console.error(err);
    });
}
````

**async/await 문법 사용 코드**
````javascript
async function findAndSaveUser(Users) {
  try {
    let user = await Users.findOne({});
    user.name = 'zero';
    user = await user.save();
    user = await Users.findOne({ gender : 'm' });
    // 생략
  } catch(error) {
    console.error(error);
  }
}
````
- 함수 선언부를 일반 함수 대신 async function으로 교체하고, 프로미스 앞에 await을 붙인다.

- 이는 해당 프로미스가 resolve 될 때까지 기다린 뒤 다음 로직으로 넘어간다.
  - 예를 들면, await Users.findOne({})이 resolve될 때까지 기다린 다음에 user 변수를 초기화한다.

- 에러 처리를 위해 try/catch문으로 로직을 감싼다.

**화살표 함수로 async 쓰기**
````javascript
const findAndSaveUser = async (Users) => {
  try {
    let user = await Users.findOne({});
    user.name = 'zero';
    user = await user.save();
    user = await Users.findOne({ gender : 'm' });
    // 생략
  } catch(error) {
    console.error(error);
  }
};
````

- for문과 async/await문을 같이 써서 프로미스를 순차적으로 실행할 수 있다. for문과 함께 쓰는 것은 노드 10 버전부터 지원하는 ES2018 문법이다.
````javascript
const promise1 = Promise.resolve('성공1'); 
const promise2 = Promise.resolve('성공2');
(async () => {
  for await (promise of [promise1, promise2]) {
    console.log(promise);
  }
})();
````

- for await of 문을 이용해서 프로미스 배열을 순회하는 코드이다. async 함수의 반환값은 항상 Promise로 감싸진다.

- 따라서, 실행 후 then을 붙이거나 또 다른 async 함수 안에서 await을 붙여 처리할 수 있다.
<br>
