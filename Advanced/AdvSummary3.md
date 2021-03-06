# WebSquare5 배워보기 - 고급 과정

✍️ *Written by Yunju Jang*

 🚩*2021.09.06*

## 3. WebSquare의 SPA 적용

#### 3-1) SPA 란?

- Single Page Application

- 브라우저에 웹 페이지를 좀 더 빠르게 표현하기 위한 방법론 중 하나

- 웹 사이트를 사용할 때 화면의 전환 없이 로딩된 자원을 재활용하여 변경된 부분만 적용하는 방식이다,

- 전통 방식과 달리, 브라우저에서 자바스크립트에 의해 결과물이 만들어지는 방식이다.

  - 자원을 미리 모두 내려받아 이를 사용하여 웹 페이지를 구성하는 기법이다.

  > 전통적인 동적 웹 페이지 방식
  >
  > - 서버에서 결과물을 만들어내는 방식을 말한다.

<br/>

<br/>

#### 3-2) SPA 적용 장단점

- 장점
  - 빠른 페이지 전환이 가능하다.
  - 사용자의 사이트 이용 흐름을 유지할 수 있따.
  - 서버 트래픽이 감소한다.

<br/>

- 단점
  - 필요 자원을 초기에 모두 로딩하기 때문에 초기 로딩 속도가 느리다.
  - 페이지 전환 시 불필요한 자바스크립트 자원을 해제해야 한다.

<br/>

<br/>

#### 3-3) 웹스퀘어5 - SPA 적용 방식

- 웹스퀘어5에서는 IFrame 부분에 SPA가 적용되었다.
- 화면 내에서 사용하고자하는 IFrame의 개수만큼 자원을 메인 화면의 페이지 로드 시점에 모두 내려 받는다.
- 이후, IFrame을 사용할 때 이 자원들을 활용하는 형태이다.
  - IFrame 형태로 신규 화면을 열어도 메인 페이지 로딩 시에 받아둔 자원을 활용하기 때문에 자원을 다시 로드하지 않아도 된다.
- 브라우저의 새로고침 없이 전환할 페이지 리소스만 받아 표현이 가능하다.
  - 화면 전환 시 제공된 API를 사용한다.
- IFrame을 이용하는 컴포넌트가 동적으로 컨텐츠를 추가해야 할 경우, 초기에 IFrame을 미리 생성하여 재활용한다.
- 동적으로 컨텐츠를 추가하는 경우 화면에 사용할 최대 IFrame의 개수를 한정 시켜야 한다.

<br/>

<br/>

#### 3-4) SPA 속성

- spaInitCount : 지정된 숫자만큼의 자원을 미리 로드한다.
  - 사용자 요청 횟수에 관계 없이 정해진 숫자만큼 자원을 로드하기 때문에 자원낭비가 발생할 수 있다.
- spaAuto : 첫 페이지가 로드된 이후 다음에 열릴 페이지를 위한 하나의 자원만을 추가적으로 로드한다.
  - 불필요한 자원 낭비를 방지할 수 있다.
  - spaInitCount보다 우선순위가 높으며, 더 권장된다.
