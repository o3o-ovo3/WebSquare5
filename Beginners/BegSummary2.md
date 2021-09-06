# WebSquare5 배워보기 - 개발자 과정

✍️ *Written by Yunju Jang*

 🚩*2021.09.02*

## 3. UI Design

참고) WebSquare5에서의 화면 디자인 방식은 HTML에서 CSS를 적용하는 방식과 같다.

#### 3-1) <em>화면 구성 방법</em>

- <b>Static Position</b>

  - WebSquare에서 사용하는 default position이다.
  - static일 경우 팝업을 제공하여 기준 컴포넌트를 기점으로 새 컴포넌트가 배치된다.
  - 소스 순서대로 화면에 배치되는 것이 원칙이다.
    - top, left 값이 무시된다.
  - 눈에 보이는 대로 렌더링되기 때문에 흐트러질 염려가 거의 없다.
  - 위치값을 안 가지기 때문에 내리거나 사이 여백을 두는 것이 불가능하다.
    - 필요시 style 영역에 직접 명명해야 한다.

  <br/>

- <b>Absolute Position</b>

  - 팝업을 제공하지 않고 사용자가 놓은 그 자리 그대로 컴포넌트가 배치된다.
  - 컴포넌트마다 자신의 기준점 (left, top) 을 가지고 있다.
  - 거의 사용하지 않는다.
    - 렌더링 순서와 위치 값이 보장되지 ㅇ낳기 때문에 순차적으로 그려지지 않기 때문이다.
    - 이 경우, 유지보수를 거듭하면 언젠가는 흐트러질 가능성이 농후하다.

<br/>

<br/>

#### 3-2) group 컴포넌트 사용

- group은 css에서 영역을 표시하는 <b>div에 해당</b>한다.

- block 특성을 가진 group 안에 inline 방식의 input box를 넣어 사용할 수 있다.

- 브라우저에 따라 유연한 화면을 구성하기 위해 group에 고정 크기를 부여하지 않는 것이 좋다.

  - 너비는 부모를 따라가려는 특성이 있어 width를 설정하지 않으면 부모의 크기를 부여 받는다.
  - 높이는 자식을 따라가려는 특성이 있어 height를 설정하지 않으면 자식의 높이에 맞추어 크기를 부여 받는다.

  > float 특성
  >
  > - 너비, 높이에 상관없이 지정된 위치 (ex. 오른쪽 끝 등) 에 놓고싶을 경우 사용한다.
  > - 자식의 특성에 float를 사용하면 붕 떠있기 때문에, 부모가 자식의 높이를 잡지 못한다.
  > - 이때는 부모의 특성에 overflow - hidden을 사용하여 해결한다.



\* 화면 구성 tip ) snippets을 사용하여 미리 만들어둔 것을 사용할 수 있다.

- snippets은 조각 조각을 미리 그려두어 그것을 활용하는 것을 말한다.

<br/>

<br/>

#### 3-3) <em>목록성 컴포넌트를 사용하는 3가지 방법</em>

\* 목록성 컴포넌트에는 radio box, check box, select box 등이 있다.

- <b>하드코딩하는 방법</b>

  - ㅎ나번 정해지면 바뀌지 않을 경우에 사용한다.
  - 컴포넌트를 더블 클릭하여 설정한다.
    - select의 경우 all, choose를 선택할 수 있다.
    - radio, check 등의 경우 rowspan, collspan 등을 설정할 수 있다.

  <br/>

- <b>스크립트에서 API로 만들어 동적으로 활용하는 방법</b>

  - Script의 onpageload 등의 함수에 설정하여 사용한다.

  <br/>

- <b>DataCollection에 담아 컴포넌트에 표현하는 방법</b>

  - 가장 많이 사용하는 방식이다.
  - 컴포넌트를 더블 클릭하여 BindItemSet 영역에서 DataCollection을 엮을 수 있다.
  - NodeSet : 엮을 DataCollection을 선택한다.
  - Label : 눈으로 보여지는 것을 선택한다. (코드명과 같은)
  - Value : 코드값이 담겨진 항목이다.

  \* DataCollection은 Outline 탭에서 추가하면 간편하다.
