# Ch2. 알아두어야 할 자바스크립트
<br>

## 2.1 ES2015+
----

### 1. ES2015+ ?

- 2015년 자바스크립트 문법에 큰 변화가 있었음. 이제는 ES2015 이상의 자바스크립트 문법을 배울 때다. 

- ES2015 이상의 자바스크립트를 통틀어 ES2015+라고 

- 6 버전부터는 ES2015 문법을 사용할 수 있다.
<br>

### 2. const, let

- 보통 자바스크립트를 배울 때는 var로 변수 선언하는 방법부터 배움. 하지만 var은 이제 const와 let으로 대체함.

- **const와 let의 공통점 : 블록 스코프(범위)**
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
  - 
<br>
