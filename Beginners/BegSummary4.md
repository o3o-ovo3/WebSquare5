# WebSquare5 배워보기 - 개발자 과정

✍️ *Written by Yunju Jang*

 🚩*2021.09.06*

## 5. CRUD 구현

\* data의 CRUD와 관련한 API는 그리드 뷰에서 사용하는 것이 아니라 dataList의 API를 이용해야 한다.

\* 디버깅 환경에서 DataCollection의 rowStatus를 살펴보면, 

삽입 시 'C', 수정 시 'U' 조회 시 'R' 삭제(delete) 시 'D', 삭제(remove) 시 'E'로 나타나는 것을 확인할 수 있다.

<br/>

#### 5-1) Insert

- insertRow : 신규 row를 생성한다.
- insertJSON : 신규 row를 생성하면서 json 형태의 초기 data를 함께 적용한다.
- insertXML : 신규 row를 생성하면서 XML 형태의 초기 data를 함께 적용한다.
- insertData : 신규 row를 생성하면서 1차원 Array 형태의 초기 data를 함께 적용한다.

<br/>

<br/>

#### 5-2) Delete

<b>삭제 처리에는 두가지 방식이 있다.</b>

- delete 처리 : 실제 데이터를 지우는 것이 아니라, rowStatus만 삭제 상태로 변경한다. ('D') 로 상태 변경
- remove 처리 : 실제 데이터를 삭제하는 방식으로, dataList에 남지 않기 때문에 rowStatus 자체가 존재하지 않는다.
  - remove API는 삭제된 data 자체를 반환한다. 따라서 변수를 이용하면 다시 활용할 수 있다.

<br/>

<br/>

#### 5-3) 상태 저장

<b>위와 같은 작업들을 저장하려면 이를 수행하는 submission을 생성한다.</b>

- 입력, 수정, 삭제 작업에 대해서만 처리를 원한다면, 화면에 보여지는 모든 data를 서버로 전송할 필요 없다.
- 영향을 받지 않은 data를 제외한 것들만 전송하는 옵션
  - submission의 Reference에 dataList를 아무 옵션 없이 설정하면 모든 data가 전송된다.
  - all : 모든 data 전송 (default)
  - inserted : 입력된 data 전송
  - deleted : 삭제된 data 전송
  - updated : 수정된 data 전송

<br/>

<br/>

#### 5-4) 다중 삭제 (delete)

- 체크 박스를 이용하여 선택 후 삭제할 수 있도록 한다.
  - 체크하면 rowStatus가 Update로 변한다는 문제가 있다.
  - 체크가 되더라도 상태값에 변화를 주지 않으려면 해당 데이터의 ignoreStatus 속성을 'true'로 변경한다.
- onclick을 작성할 때, 체크된 항목을 받아오기 위해 API를 사용한다.
  - getCheckedIndex : check된 row의 index를 배열로 반환
  - getCheckedData : check된 row의 data를 1차원 배열로 반환
  - getCheckedJSON : check된 row의 data를 json 형태로 반환
  - getCheckedXML : check된 row의 data를 xml 형태로 반환

<br/>

<br/>

#### 5-5) 초기화 (모든 데이터 삭제)

- DataList의 모든 데이터를 삭제하는 두가지 방식

  - removeAll

    - 초기화 적용을 위해 사용하는 dataList의 API
    - 한꺼번에 모든 값을 삭제하고, removeRow, removeRows와 마찬가지로 삭제된 data를 1차원 배열로 반환

    <br/>

  - setData

    - 삭제 data를 반환할 필요가 없을 때 사용
    - 인자로 빈 배열을 넣어주면 모든 data가 초기화 된다.
    - 이 경우 삭제된 data를 갖고있지 않아 <b>메모리를 훨씬 적게</b> 사용할 수 있다.
    - 삭제된 data를 활용하지 않는다면 이 방법을 권장한다.

<br/>

<br/>

<br/>

## 6. 그 외 gridView의 기능

#### 6-1) Excel 기능

- advancedExcelDownload

  - Excel Download를 처리하는 API
  - 옵션에 따른 data를 excel 파일로 다운로드할 수 있다.
  - 빈배열을 옵션으로 줄 경우 화면 상의 모든 data를 다운로드 한다.

  <br/>

- advancedExcelUpload

  - 업로드할 파일을 선택할 수 있는 팝업이 실행된다.
  - HeaderExist 옵션을 이용하여 헤더가 두번 보여지는 것을 방지할 수 있다.
  - 이 밖의 다양한 옵션이 API로 제공되니, 사용 시에 검색하여 알맞게 사용할 수 있다.

<br/>

<br/>

#### 6-2) 총합 표시

- gridView 영역 선택 후 마우스 우클릭하여 Footer를 추가한다.

- 선택한 column의 data 총합이 필요할 때 사용한다.

- 총합 계산을 위해 body와 Footer 모두 dataType이 number로 설정되어 있어야 한다.

- Footer의 Property에서 속성을 아래와 같이 변경한다.

  \* input type : expression

  \* expression : SUM('ROLE_CD') --> body의 ID를 사용

  - 실제 계산식에 해당
  - 제공되는 계산식은 SUM, AVG, MAX, MIN, COUNT
