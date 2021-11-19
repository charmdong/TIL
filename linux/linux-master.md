# Linux Master

## 17년 2월

* chown - 파일 소유자나 소유 그룹을 변경하기 위한 명령어
  * chown <mark style="color:blue;">user</mark>:<mark style="color:orange;">group</mark> /path/to/fileOrDirectory
  * \-R, --recursive : 하위 디렉토리까지 변경&#x20;
  * \-c : 변경된 파일만 자세하게 보여줌
  * \-f : 변경되지 않은 파일에 대해 오류 메시지를 보여주지 않음.
  * \-v : 작업 상태를 자세히 보여줌.



* Sticky-Bit
  * /tmp와 /var/tmp 디렉토리는 777 권한으로 누구나 파일을 생성하고 삭제할 수 있다. 이에 따라 중요한 파일을 누군가가 삭제할 수 있다는 문제가 발생하고, 이를 방지하기 위해 사용되는 권한 설정 방법이다.&#x20;
  * Sticky-Bit가 설정된 디렉토리 내에서는 다음 3가지 규칙이 적용된다.
    1. Permission이 <mark style="background-color:blue;">777</mark>인 파일에 대해서 파일의 소유자만이 삭제할 수 있다.
    2. 디렉토리 자체도 소유자만이 삭제할 수 있다.
    3. root는 1과 2가 가능하다.
  * 설정 방법 : chmod <mark style="color:blue;">**1777**</mark> file
