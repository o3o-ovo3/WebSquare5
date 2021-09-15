# SMB

:writing_hand: *Assembled by Yunju Jang*

🚩 *2021.09.15*

<hr>

-  <b>SMB 란?</b>

  - 서버 메시지 블록 (Server Message Block)

  - Microsoft와 IBM, Intel에서 공동 개발한 프로토콜로, 로컬 네트워크에서 파일, 프린터 등을 액세스하기 위해 사용되는 프로토콜이다.

  - Unix의 NFS와 같은 기능을 한다.

  - client/server 모델을 이용하고, 여러 개의 네트워크 프로토콜 상에서 실행될 수 있다.

  - TCP/IP 기반하의 NetBIOS 프로토콜을 이용하기 때문에 NFS, NIS, Ipd와 같은 유닉스의 분산인증구조와 유사하다. 따라서 윈도우 중심의 네트워크 환경에서는 필수적이라고 할 수 있다.

    > <b> NFS 서버</b>
    >
    > - Network File System
    > - 유닉스 환경에서 오랫동안 사용된 네트워크 상에서의 자료 공유 방법
    > - 컴퓨터 사용자가 원격지 컴퓨터에 있는 파일을 마치 자신의 컴퓨터에 있는 것 처럼 검색, 저장, 수정하는 프로그램
    > - 사용자 시스템에는 NFS 클라이언트가 있어야하며 원격지 컴퓨터에는 NFS 서버가 설치되어있어야 한다.

<br/>

<br/>

- <b>SAMBA 란?</b>
  - 리눅스에서 동작하면서 윈도우의 랜 매니저 기능을 흉내내는 소프트웨어이다.
  - 윈도우 쪽에서 리눅스 서버의 하드디스크와 네트워크 프린터 자원을 공유하도록 환경을 설정할 수 있따.
  - 삼바를 통해 리눅스 쪽에서 윈도우 쪽 파일 시스템과 프린터로도 접근할 수 있다.
    - 이러한 것은 모두 삼바서버가 SMB/CIFS 프로토콜을 흉내냄으로써 가능해진다.

<br/>

<br/>

✔ 추가) 

- CIFS 란?
  - Common Internet File System
  - 인터넷을 위한 SMB 파일 공유 프로토콜의 확장 버전이다.
  - SMB 프로토콜 위에 DNS를 이용한 확장성, 느린 전화 접속 네트워킹을 위한 최적화, 유니코드를 따르는 파일 이름 지원, 윈도우와 유닉스 환경 동시 지원을 제공하는 인터넷의 표준 파일 규약이다.
  - 폐쇄적인 SMB 프로토콜과 달리 CIFS 규약 정의에 여러 유닉스 업체들이 참여했다.

<br/>

<br/>

<br/>

### Reference📖

- https://alsrbdmsco0409.tistory.com/223
- https://kim-dragon.tistory.com/38
- https://kkamagistory.tistory.com/228
- http://coffeenix.net/doc/network/SMB_ICMP_UDP(huichang).pdf
- https://jhnyang.tistory.com/279
- https://thebook.io/006718/part02/ch07/02/01/
