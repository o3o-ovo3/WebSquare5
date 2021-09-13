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
- 파일을 생성하지 말라고 하셨다! (파일 입출력으로 인한 성능 문제)

<br/>

<br/>

<b>방법 3) 쉘 스크립트 자체를 자바가 읽게하고, 별도의 결과 파일 없이 바로 자바스크립트에서 브라우저에 표현한다.</b>

- 페이지 이동 없이 단순히 필요한 데이터만 받는 경우
- 컨트롤러에 @ResponseBody를 붙여 ajax를 이용해 jsp 페이지와 model 데이터가 아닌 <b>필요한 데이터만을 받아온다.</b>

``` java
/* 쉘 스크립트 실행 및 통신 */
	
	@RequestMapping("/training/getLog.do")
	@ResponseBody
	public String getLogOneLine() throws Exception {
		StringBuilder sb = new StringBuilder();
		try {
			String line;
			String command;
			InputStream is;
			
			// 쉘 스크립트 실행 부분
			// 1. 스크립트를 실행
//			command = "powershell Get-Content C:\\\\WEBSQUARE_DEV_PACK\\\\workspace\\\\ws5\\\\logs\\\\web.log -Tail 1";
			
			// 2. 스크립트 파일 실행
			command = "powershell.exe  \"C:\\WEBSQUARE_DEV_PACK\\workspace\\ws5\\logs\\myLog.ps1\" ";
			
			is = Runtime.getRuntime().exec(command).getInputStream();
			BufferedReader br = new BufferedReader(new InputStreamReader(is));
			
			while((line = br.readLine()) != null) {
				sb.append(line); // 쉘 스크립트 실행 결과를 String Builder에 저장
			}
//			sb.append(br.readLine());
			br.close();
			is.close();
		} catch (IOException e) {
			e.printStackTrace();
		}
		
		System.out.println("//////////////" + sb.toString());
		return sb.toString();
	}
```

- Controller에 @ResponseBody 어노테이션을 붙인다.
  - viewResolver를 생략하고 데이터만 응답하게 된다.
  - 지금은 String을 return 했으나, 컨트롤러의 return 타입을 변경하면 int나 dto와 같은 데이터도 전송할 수 있다.
  - 해당 데이터를 받기 위해서는 ajax를 사용해야한다. (나는 웹스퀘어를 이용하기 때문에 submission을 이용해 처리했다.)
    - 이 방법은 첫번째 reference 참고!

``` javascript
	scwin.submission1_submitdone = function(e) { // submission이 끝나면 그 결과를 e에 반환
        // e.responseText : Response Data 원본으로 String 형태 반환
		document.write(e.responseText);
	};
```

- WebSquare를 활용했기 때문에 submission의 API를 이용하여 통신 후 결과 데이터를 받아와 원본 String을 출력했다.
- 이 방법은 Vue, React 등 웹 프론트 프레임워크를 사용할 때 많이 사용하는 방법이다.

<br/>

<br/>

<br/>



<hr>


### Reference📖

- https://admm.tistory.com/54
- https://stackoverflow.com/questions/29545611/executing-powershell-commands-in-java-program
