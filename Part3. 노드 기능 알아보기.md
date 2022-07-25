# ch3. 노드 기능 알아보기
<br>

## 3.1 REPL 사용하기
----

- 자바 스크립트는 스크립트 언어기 때문에 미리 컴파일을 하지 않아도 코드를 실행할 수 있다.

- 노드에서도 브라우저 콘솔과 비슷한 콘솔을 제공하는데, 입력한 코드를 **읽고(read)**, **해석하고(eval)**, 결과물을 **반환하고(print)**, 종료할 때까지 **반복한다(loop)** 고 해서 **REPL**이라고 부른다.

- 노드의 REPL을 사용하려면 터미널을 열고 node를 입력하면 된다.

  <img width="288" alt="image" src="https://user-images.githubusercontent.com/68415644/180740739-926c6834-29d3-4491-9c98-82963497782d.png">

- 위와 같이 프롬프트가 > 모양으로 바뀌었다면 자바 스크립트 코드를 입력할 수 있다.

  <img width="295" alt="image" src="https://user-images.githubusercontent.com/68415644/180741330-f804aad3-d126-49e9-8941-673f84f7f584.png">

- 위와 같이 출력되었다면 정상적으로 작동한 것이다. 이후 REPL을 종료하려면 Ctrl + C 를 두번 누르거나, REPL 창에 .exit을 입력하면 된다.

- REPL는 한 두줄짜리 코드는 확인 해보기 좋지만 여러 줄의 코드를 실행하기에는 불편하기 때문에 자바 스크립트 파일을 만든 후 파일을 실행하는 것이 좋다.
<br>

## 3.2 JS 파일 실행하기
----

- 자바 스크립트 파일을 아래와 같이 만들어서 실행해보자. vsCode를 이용하여 만들었다.

````javascript
function helloWorld() {
    console.log('Hello World');
    helloNode();
}

function helloNode() {
    console.log('Hello Node');
}

helloWorld();
````

- 이렇게 만든 파일을 Node를 통해 실행시키려면, 콘솔에서 node [자바 스크립트 파일 경로]로 실행하면 된다. 이때 확장자(.js)는 생략해도 된다.

  <img width="567" alt="image" src="https://user-images.githubusercontent.com/68415644/180743243-b0a46ae8-cd48-4ed9-ad9a-f545921b4312.png">
