# WebSquare5 배워보기 - 고급 과정

✍️ *Written by Yunju Jang*

 🚩*2021.09.07*

## 6. 대용량 data 성능 개선

#### 6-1) 데이터 처리 방식

- json
  - 웹에서 많이 사용하는 데이터 처리 방식
  - 처리 속도가 빠르며, data 손실을 방지할 수 있다.
  - 대용량 data에 대해서는 빠른 속도라 할 수 없다.

<br/>

- Array
  - 1차원 Array의 경우 json에 비해 data size가 보다 줄어들어 비교적 빠른 처리 속도를 보인다.
  - 그러나 가독성이 좋지 않고 data를 조작하기에 적합하지 않다.

<br/>

- xml
  - 전문 형태의 구조를 가질 수 있다.
  - data size가 크기 때문에 속도가 느리며, data 손실을 유발할 수 있어 현재는 잘 사용하지 않는다.

<br/>

<br/>

#### 6-2) WebSquare Array

- 대용량 데이터 성능 개선을 위한 처리 방식이다.

- json 구조의 형태로 1차원 Array의 처리 속도를 가진다.

- json 과의 비교

  - 일반적인 json 형태는 Mybatis Query를 바로 호출

  - WebSquare Array 방식은 별도의 Handler를 통해 구현

    ``` java
    public class WqLargeResultHandler implements ResultHandler {
    
    	private int totRowCount = 0;
    	private int totColCount = 0;
    	private ArrayList<String> columnArr = null;
    	private ArrayList<Object> dataArr = null;
    	private Map<String, Object> result = null;
    
        ...
            
    	private void mapTypeRowHandler(LinkedHashMap rowMap) {
    		if (totRowCount == 0) {
    			columnArr = new ArrayList<String>();
    			Set keySet = rowMap.keySet();
    			Iterator<String> keys = keySet.iterator();
    			totColCount = keySet.size();
    
    			while (keys.hasNext()) {
    				String key = (String) keys.next();
    				columnArr.add(key);
    			}
    		}
    
    		for (int i = 0; i < totColCount; i++) {
    			dataArr.add(rowMap.get(columnArr.get(i)));
    		}
    		totRowCount++;
    	}
        ...
    }
    ```

    - 위와 같이 column 정보와 data 정보를 각각 1차원 배열에 담아 결과 값을 하나의 Map 형태로 만들어 return 한다.
    - Mybaits를 사용할 경우 ResultHandler를 상속 받아 구현할 수 있다.

<br/>

<br/>

<br/>

## 7. gridView의 속성

#### 7-1) CUD API 사용

- dataList와 gridView가 합쳐진 구조에서 성능을 향상시키는 방법

  - insertRow를 이용
    - 100건의 data 입력 시 각 cell 별로 data를 넣기 때문에 API 가 500번 수행된다.
    - WebSquare에서는 빈번하게 API를 호출하게 되면 화면 반영 시간이 걸려 수행 속도가 느려진다.
  - insertJSON 이용
    - for문 수행 시 API를 호출하지 않고 입력할 data만 미리 생성한 후 API를 단 한번 호출하는 형태이다.
    - API를 한 번만 호출하기 때문에 속도가 비교적 빠르다.

  <br/>

  <br/>

- BroadCast 기능

  - 특정한 이유로 여러번 API를 부득이하게 반복 수행해야 할 때
  - setBroadCast 속성에 false 값을 적용
    - API는 반복 수행하되, 화면에 반영하지 않는다.
    - 모든 API를 수행한 후 다시 true 값을 적용하면 그 때 화면에 반영한다.
    - 여러번 API를 수행해도 화면 반영은 한번이기 때문에 속도를 향상시킬 수 있다.

  <br/>

  <br/>

- removeRow vs removeRows

  - 다건 삭제 시 removeRow를 여러번 반복하는 것보다 removeRows를 통해 한번에 처리하는 것이 훨씬 빠르다.

  <br/>

- setRowJSON

  - row 단위로 한번에 값을 적용한다.
  - 일일이 setCellData를 통해 적용하는 것보다 훨씬 간결하다.

<br/>

<br/>

#### 7-2) Cell 병합

- colMerge 속성
  - true로 적용하면 실제 병합을 하지 않고 첫번째 data만 보이게 한다.
  - 나머지 data는 보이지 않기 때문에 마치 병합된 것처럼 보이게하는 방식이다.

<br/>

- mergeCells
  - 실제로 병합을 수행한다.
  - column 별 속성을 제어하는 것이 아니라 gridView 전체에 적용되는 속성이다.
  - 속성 값 설명
    - never : mergeCells에 의해 merge된 것들을 해제한다.
    - bycol : 같은 column 내에 연속적으로 데이터가 같은 row들을 병합한다.
    - byrow : 같은 row 내에 연속적으로 데이터가 같은 col들을 병합한다.
    - bycolrec : bycol 수행 후, 병합되지 않은 cell 들을 대상으로 byrow를 진행한다.
    - byrestriccol : 같은 col 내에서 연속적으로 데이터가 같으면서, 자신의 왼쪽에 위치한 col이 병합된 경우 해당 row들을 병합한다. (n+1 컬럼에 n 컬럼을 upperColumn으로 지정한 상태)
    - byrestricrow : 같은 row 내에서 연속적으로 데이터가 같으면서 자신의 위쪽에 위치한 row가 병합된 경우 해당 row들을 병합한다. (n + 행에 n행을 upperRow로 지정한 형태)

<br/>

<br/>

#### 7-3) Scroll

- fastScroll
  - true : 보다 부드럽게 scroll이 적용되지만, 저사양일 경우 '화면 갱신중입니다...' 라는 메세지가 보인다.
    - 화면에 그려줄 수 있는 부분까지 우선 적용한 후 미처 그리지 못한 영역에 대해 메세지로 대체하여 보다 원할하게 세로 scroll을 반영해준다.
  - false : 부드럽게 scroll이 되지 않고, 약간의 loading 시간이 있지만, 화면 갱신 중 메세지는 보이지 않게 된다.
  - 브라우저의 성능이 좋은 경우 둘의 차이가 거의 없다.
    - 가상 환경에서 접속하거나 저사양의 브라우저를 지원하는 경우 사용한다.

<br/>

<br/>

#### 7-4) customFormatter 적용 방식

- API 적용 

  - ex) setCellBackground, setCellColor 등

  ``` javascript
  // setCellBackground, setCellColor 등 API를 이용한 구현
  scwin.ui_grid_POSITION_CD = function(data, formattedData, rowIdx, colIdx){
      if(data === "07"){
          ui_grid.setCellBackgroundColor( rowIdx, colIdx, "blue" );
          ui_grid.setCellColor( rowIdx, colIdx, "#fff" );
      }
      return formattedData;
  };
  ```

  - 장점 : Excel 다운로드 시 원본 데이터로 다운 받는다.
  - 단점 : innerHTML 방식보다 속도가 느리다.

<br/>

- innerHTML 방식

  - return되는 formattedData를 변경하는 방식이다.

  ``` javascript
  // return 된 formattedData를 변경하는 방식
  scwin.ui_grid2_GENDER_CD = function(data, formattedData, rowIdx, colIdx){
      if(data === "F"){
          return "<span style='color:orange'>" + formattedData + "</span>";
      }
      return formattedData;
  };
  ```

  - 장점 : 렌더링 속도가 매우 빠르다.
  - 단점 : 엑셀 다운로드 시 변경된 데이터 포맷으로 다운 받아진다.



