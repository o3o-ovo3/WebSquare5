# WebSquare5 배워보기 - 개발자 과정

✍️ *Written by Yunju Jang*

 🚩*2021.09.02*

## 1. WebSquare5 란?

#### 1-1) WebSquare5 소개

- 웹 표준을 준수한 UI 프레임워크로 UI 컴포넌트와 Util API, 통합 개발 도구를 제공한다.
- 웹스퀘어로 개발 된 화면 파일은 단독으로 브라우저에서 실행할 수 없다.
  - 화면 파일으 웹스퀘어 JavaScript 엔진을 통해 실시간 해석되어 브라우저에 표현된다.
- XML 파일을 랜더링하여 Html 화면으로 보여주는 방식이다.

<br/>

<br/>

#### 1-2) HTML5 와의 차이

- head 태그에 모델 영역이 존재한다.
- <em>모델 영역의 구성</em>
  - DataCollection : 값들을 담아놓은 객체, 데이터를 주고 받을 때 사용
  - Submission : 통신을 정의해서 사용
  - Workflow

<br/>

<br/>

## 2. WebSquare5 Studio 사용하기 

#### 2-1) <em>5가지 탭</em>

- Design : Body 영역에 해당하는 컴포넌트들을 그려주는 탭

- Script : 자바스크립트 코드를 통해 비즈니스 로직을 제어하는 탭
- DataCollection : 데이터를 담는 객체
  - DataMap - 값이 하나일 때
  - DataList - 값이 여러개일 때
  - LinkedDataList - 이미 존재하는 데이터를 재사용할 때 (그 중 일부 사용 시)
  - AliasDataList/Map - 이미 존재하는 데이터를 재사용할 때 (프레임으로 나누어 사용 시 ex. 부모-자식)
- Submission : 통신 생성
- Source : 코드 확인용 (직접 작성 또는 수정하는 것은 삼가도록 함)

<br/>

<br/>

#### 2-2) <em>컴포넌트의 3가지 사용 방식</em>

-  <b>속성</b> : 컴포넌트 정적 제어 (늘 가져가야 하는 특성을 지정)
- <b>이벤트</b> : 동작을 부여하고, 동작 이후는 script가 제어할 수 있도록 함
- <b>API</b> : 동적으로 처리할 때 -> 스크립트에서 활용 ex. if-else

<br/>

<br/>

#### 2-3) <em>CSS 3가지 적용 방식</em>

- <b>inline 적용 방식</b>
  - 스타일 탭에서 적용하거나
  - 속성, 이벤트탭의 style 영역에서 적용
- <b>internal 적용 방식</b>
  - 로컬소스에서 class를 정의하여 사용한다.
  - outline 뷰에서 내부 스타일 추가를 클릭
- <b>external 적용 방식</b>
  - 외부 스타일 시트를 가져온다.
  - Design 화면에서 Drag&Drop으로 쉽게 적용 가능

<br/>

<br/>
