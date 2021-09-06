# WebSquare5 배워보기 - 고급 과정

✍️ *Written by Yunju Jang*

 🚩*2021.09.06*

## 2. javascript 자원 정리

#### 2-1) 웹 기반 페이지의 문제점

- 전역 변수, 전역 함수를 생성하면 해당 페이지에서 이를 생성하는데에는 제약을 받지 않지만,
- 생성 후 이 객체들을 따로 삭제하지 않으면 브라우저에서 이 페이지를 열 때마다 메모리가 누적된다.
- 이러한 동작이 반복되면 <mark>메모리가 과도하게 쌓여 비정상적인 동작을 유발한다.</mark>

<br/>

<br/>

#### 2-2) 자원의 해제 방법 두가지

- 직접 해제

  - 과도한 메모리 누적 방지를 위해 페이지를 닫을 때 전역 객체의 자원을 직접 해제한다.

  ``` javascript
  var a = ""; // 전역 변수 생성
  
  // 전역 함수 생성
  function aa (){
      
  };
  
  scwin.onpageload = function() {
      
  };
  
  scwin.onpageunload = function() {
      // 사용한 전역 변수 및 함수 삭제
      delete a;
      delete aa;
  };
  ```

  - 그러나, 번번히 직접 객체를 삭제할 경우 script 작성 시 불편함을 초래한다.

<br/>

<br/>

- namespace 기반 전역 객체 작성

  ``` javascript
  var obj = {}; // obj 객체 생성
  
  // obj 객체의 하위로 전역 변수 및 함수 작성
  obj.a = "";
  
  obj.fnTest = function (){
      
  };
  
  swcin.onpageload = function() {
      
  };
  
  scwin.onpageunload = function() {
      delete obj; // 자원 해제
  };
  ```

  - 이와 같이 namespace를 이용하여 생성한 변수 및 함수 등이 모두 obj라는 객체의 하위로 관리된다.
  - 따라서, 페이지를 닫을 때 obj 객체에 대해서만 삭제 처리를 진행한다.
  - 개별 관리보다 훨씬 효율적인 관리가 가능하다.

<br/>

<br/>

#### 2-3) scwin이란 무엇인가?

- 웹스퀘어 신규 페이지 생성 시 보여지는 객체로, 위 사례의 obj와 같은 기능을 한다.
- script에서 event, function 생성 시 scwin이라는 객체의 하위로 생성되어 관리된다.
- 위의 obj 객체처럼 닫을 때마다 <mark>삭제 처리를 따로 하지 않아도 웹스퀘어 엔진에서 알아서 삭제</mark>해주는 기능을 가지고 있다.
- config.xml 파일을 통해 이름을 선언하는 부분을 확인할 수 있다. --> spa로 선언된 부분
  - variable 속성 
    - scwin이라는 이름을 사용하고 있음을 알 수 있고, 다른 객체 명으로 등록하거나 ','를 이용해 2개 이상의 이름을 사용할 수도 있다.
  - scriptCache 속성
    - 외부 모듈에 대한 cache 처리를 설정할 수 있따.
  - autoReload 속성
    - true로 설정하면 뒤에 선언된 count의 숫자만큼 페이지가 로드되었을 때 브라우저를 다시 Reload하여 누적된 메모리를 초기화한다.

