# WebSquare5 배워보기 - 고급 과정

✍️ *Written by Yunju Jang*

 🚩*2021.09.07*

## 9. 다국어 적용하기

#### 9-1) Client 다국어 적용 방식

- config 파일의 languagePack 부분을 통해 적용 방식과 적용된 js file의 위치를 알 수 있다.
- 지정한 js 파일에 정의된 값을 다국어 적용 컴포넌트 localRef 속성에 적용한다.

<br/>

- 적용 방법
  - Studio 상단의 Window -> Show View -> Other -> WebSquare -> Locale 확인
  - 프로젝트에서 사용하는 다국어 js 파일 목록 확인
    - 이 목록은 config.xml의 물리적인 위치를 읽어들이는게 아닌 Project 설정 부분에서 가져오는 것
    - 확인 방법 : Project -> Properties -> WebSquare -> Engine Configuration -> languagePack 확인
  - 확인한 부분에 대해 config.xml 부분을 languagePack 설정 부분과 동일하게 적용하면 된다.

<br/>

<br/>

#### 9-2) Server 다국어 적용 방식

- config.xml의 pageURLPrefix를 확인하면 com.getI18NUrl 이라는 공통 함수를 호출하고 있는 것을 알 수 있다.
  - 이 함수는 websquare5의 경로를 I18N을 통해 호출하며, 이 때 locale을 함께 전달해준다.
- config 디렉토리의 websquare.xml 파일을 열어 <i18n> Node의 하위로 다국어 설정 시 확인하는 page source의 위치를 알 수 있다.
- server 방식은 client 방식처럼 locale을 사용하지 않는다.
  - 적용된 파일을 확인하기 위해서는 ServerLocale을 확인해야 한다.
    - 확인 방법 : Window -> Show View -> Other -> WebSquare -> Server Locale 선택
  - 이렇게  보여진 Server Locale에서 [use] 체크 후 다국어에서 사용할 properties file을 직접 선택한다.
