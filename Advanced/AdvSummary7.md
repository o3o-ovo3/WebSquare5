# WebSquare5 배워보기 - 고급 과정

✍️ *Written by Yunju Jang*

 🚩*2021.09.07*

## 8. Excel Provider

#### 8-1) 기본 Excel data 전송 방식

- advanvedExcelDownload API 사용
  - 이를 이용하여 client를 통해 대용량의 data를 전송하면 속도가 매우 느려진다.
  - 사용하는 WAS에게도 매우 큰 부담을 주게 되어 비정상 종료가 발생할 수 있는 등 많은 문제점이 있다.

<br/>

#### 8-2) provider 사용

\* gridView에서 대용량 data를 excel로 내려 받는 경우 사용한다.

\* client에서 전송하는 request data를 줄여주기 위해 사용한다.

- <b>기본 provider</b>

  - <b>dataProvider 옵션</b>
    - provider가 별도의 class를 지정하여 사용하고 있음을 알 수 있다.
    - 해당 class를 확인해보면, service call을 통해 data를 조회한 후, 1차원 배열 형태로 return하는 것을 알 수 있다.
  - client의 data를 request 정보로 전달하지 않고, 지정한 class를 통해 서버에서 직접 data를 호출하는 형태로 사용한다.
    - 이 class는 WebSquare5에서 지정하는 IExternalGridDataProvicer라는 Interface를 상속 받아 구현할 수 있다.

  <br/>

  - 구현 방법
    1. 인터페이스를 상속 받는다.
    2. service call을 통해 data를 조회한다.
    3. 조회된 data를 1차원 배열 형태로 return 한다.

  <br/>

  - 특징
    - client에서 많은 양의 data를 내려주지 않아도 되기 때문에 WAS의 부담을 줄여줄 수 있다.
    - 그러나, 10만건 이상의 큰 data를 조회할 경우에는 여전히 부담이 있다.

  <br/>

  <br/>

- <b>split provider</b>

  - 위에 언급한 WAS의 부담을 더 줄여주기 위해 사용한다.
  - 기본 provider 처럼 별도의 class를 지정하여 request 정보에 data를 전달하지 않고 사용한다.
  - 기본 provider와 다르게 <mark>data를 분할</mark>하여 처리하는 기능을 가지고 있다.
    - 그 덕분에 수행하는 WAS의 부담을 더 줄일 수 있다.
  - IExternalSplitPorvider 인터페이스를 상속 받아 구현한다.

  <br/>

  - 구현 방법
    1. 인터페이스를 상속 받는다.
    2. service call을 통해 data를 조회한다.
    3. 조회된 모든 data에 대해 지정된 건수 만큼 data를 분할하여 1차원 배열의 형태로 return 한다.

  <br/>

  - 특징
    - 기본 provider보다 훨씬 안정적이지만, 분할 처리를 하기 때문에 속도가 많이 빠르지는 않다.
    - config 파일의 excel download 부분에 maxRowCounter 속성이 있어 이를 통해 최대 row를 지정해야 한다.
      - 지정하지 않을 경우 10만 건까지밖에 사용할 수 없다.



