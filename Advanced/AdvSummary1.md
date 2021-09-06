# WebSquare5 배워보기 - 고급 과정

✍️ *Written by Yunju Jang*

 🚩*2021.09.06*

## 1. lazy = "false" 모드

- 전체 페이지의 <b>기본</b> 로딩 순서
  1) Component 생성
     - Design에서 배치된 component가 적용된 속성과 함께 생성됨
  2) Script 생성
     - Script에서 선언된 function 및 이벤트가 생성됨
  3) Script 실행

<br/>

- Component의 일부 속성 중에는 Script에서 function으로 등록하여 사용하는 것이 있다.

  ex) customFormatter

  - Script에 구현된 함수를 Component의 속성에서 적용하게 된다.
  - 이때, 함수의 생성 시점은 Component의 생성 시점보다 뒤에 있으므로, <mark>이 함수를 토대로 속성을 적용하고 있는 Component가 함수보다 먼저 생성</mark>되게 된다.
    - 따라서, <mark>함수의 실행이 제대로 이루어지지 않을 수 있다.</mark>
    - 이와 같은 문제점을 해결하고자 lazy = "false" 기능을 적용한다.

<br/>

<br/>

#### lazy = "false" 기능 적용

- 이 속성이 적용되면, scxript의 생성 시점을 앞당길 수 있다.
  - 적용 후 로딩 순서
    1. Script 생성
    2. Component 생성 (속성 적용 포함)
    3. Script 실행
- 즉, Script의 생성 시점을 Component 생성 전으로 앞당긴다.
  - Component에서 속성으로 적용하는 (Script에 정의 된) function을 활용할 수 있게 된다.
- 단, <mark>이렇게 적용할 때 실행문은 반드시 onpageload 부분에 작성</mark>해야 한다.
  - onpageload 부분의 실행은 Component 생성 이후이지만,
  - 다른 부분은 component가 생성되기 이전에 실행될 수 있다.
    - 이 경우 오동작을 유발할 가능성이 있다.
