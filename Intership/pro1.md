# 1️⃣ 웹 화면에 로그 띄우기

요구사항)

✔ Shell Script - tail 명령어를 이용하여 가장 최근 로그의 첫 라인을 가져온다.

✔ javascript 를 이용하여 화면에 뿌려준다.

<br/>

### Step1. PowerShell을 이용하여 로그 파일의 가장 최근 첫 라인 가져오기

- 쉘 스크립트 생성 

  ``` shell
  # myLog.ps1 스크립트 작성
  # 대상 로그 파일명의 가장 최근 로그 1라인을 받아서 redi.txt라는 파일로 저장하는 스크립트
  Get-Content web.log -Tail 1 > C:\경로\redi.txt
  ```

  

  ``` shell
  # myLog.sh 스크립트 작성
  #!/bin/bash
  tail -1 <web.log> > redi.txt
  ```

  - tail : 파일의 내용을 뒤에서부터 출력해주는 쉘 명령어 
  - PowerShell에서는 : Get-Count 파일명 -Tail 라인 수
  - \> 파일명 : 스크립트 실행 결과를 지정한 파일로 추출

<br/>

<br/>

### Step2. 가져온 로그를 javascript를 이용하여 웹 화면에 뿌려주기

<b>방법 1) 파일을 input 받아서 FileReader로 내용 추출하여 뿌려주기</b>

``` javascript
	scwin.btn_textFile_onclick = function(e) {
		var input = document.createElement("input");
		
		input.type = "file";
		input.accept = "text.plain";
		
		input.onchange = function(event){
			processFile(event.target.files[0]);
		};
		
		input.click();
	};
	
	function processFile(file){
		var reader = new FileReader();
		console.log("hi");
		
		reader.onload = function() {
			document.write(reader.result);
			console.log(reader.result);
		};
		
		reader.readAsText(file);
	};
```

- 로컬에서 사용자가 직접 가져와야하기 때문에 좋은 방법이 아닌 것 같다.

<br/>

<br/>

<b>방법 2) 파일을 프로젝트 내부에 넣어두고 그걸 자바스크립트가 읽게 한다. </b>

``` javascript
	// jQuery 이용
	scwin.onpageload = function() {
		$.get("redi.txt", function(data){
			document.write(data);
		});
	};
```

- 자동으로 쉘 스크립트 실행해서 결과 파일을 첨부한게 아니라서 좋은 방법이 아닌 것 같다.

<br/>

<br/>

<b>방법 3) 쉘 스크립트 자체를 자바가 읽게하고, 프로젝트 안에 결과를 생성해서 그걸 자바가 읽게 한다.</b>
