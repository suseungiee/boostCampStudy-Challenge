# Day2

root계정에서

**adduser k043**  // k043이름의 계정생성

비밀번호도 입력하라고하는데 이때 입력하면 된다

userdel -r 유저이름 //유저정보 삭제 가능

![Day2%206e268f96d64b457fba71fced1ad5cbfa/Untitled.png](Day2%206e268f96d64b457fba71fced1ad5cbfa/Untitled.png)

이후 virtual Box → 설정 → 네트워크 → 고급 → 포트포워딩에서

Rule1과같이 포트포워딩을 해준다

**포트포워딩**

포트란 서버에서 할 일을 나눠서 받는 통로?

ex) ftp 파일 요청 : 21번 포트 , 웹사이트 요청 : 80번 포트

공유기와 여러 pc가 연결되어있고 공유기 외부로부터 특정 pc로 특정 작업 요청이 들어왔을때 공유기는 이를 사용자가 원하는 pc의 특정포트로 정확히 전달해야한다. 이러한 이정표작업을 포트포워딩이라한다.

즉 192.168.56.1 1234포트로 접속 요청이 들어오면 10.0.2.15 22포트로 넘겨준다는 의미

192.168.56.1 : 가상머신 host 기본 ip      / 10.0.2.15 가상머신 ip 

1234포트 : 내가 임의로 정한 접속 요청용 포트 / 22번포트 : SSH기본포트  

**SSH**

원격 시스템에서 명령 실행 및 파일 복사 등을 하게해주는 프로토콜

![Day2%206e268f96d64b457fba71fced1ad5cbfa/Untitled%201.png](Day2%206e268f96d64b457fba71fced1ad5cbfa/Untitled%201.png)

이후 putty에서 

![Day2%206e268f96d64b457fba71fced1ad5cbfa/Untitled%202.png](Day2%206e268f96d64b457fba71fced1ad5cbfa/Untitled%202.png)

다음과같이 host Name에 192.168.56.1 (가상머신 default ip), port번호 1234로 입력하면 연결이된다.

이때 사용자 이름으로 k043, 비밀번호를 치면 다음과 같이 새로운 계정으로 로그인이 된다.

![Day2%206e268f96d64b457fba71fced1ad5cbfa/day2_.png](Day2%206e268f96d64b457fba71fced1ad5cbfa/day2_.png)

================================================================

![Day2%206e268f96d64b457fba71fced1ad5cbfa/day2_backup.png](Day2%206e268f96d64b457fba71fced1ad5cbfa/day2_backup.png)

mkdir // 디렉토리를 만드는 명령어

로그인한뒤 

mkdir ./backup //  로그인한 계정의 현재 디렉토리에 "backup"폴더 생성

ls -al //현재 디렉토리내의 모든파일 정보 볼 수 있는 명령어

chmod -R 764 ./backup // ./backup파일의 접근권한을 764로 바꿔준다

-R옵션은 backup폴더 하위의 파일들도 모두 같은 접근 권한 부여

================================================================

Virtual Box에 ubuntu설치 시 자동으로 위치를 잡아주기때문에

터미널에서 date명령어만 치면 자동으로 현재시간과 동기화 된 것을 볼 수 있다

![Day2%206e268f96d64b457fba71fced1ad5cbfa/day2_%201.png](Day2%206e268f96d64b457fba71fced1ad5cbfa/day2_%201.png)

================================================================

**sudo apt update && sudo apt upgrade**

**sudo apt install curl**

**curl -s [https://get.sdkman.io](https://get.sdkman.io) | bash**

**sdk install kotlin**

이후 터미널 다시열고

**apt install default-jre**

**curl** 

웹으로 http메세지 보내고 결과 요청하는 명령어

즉 파일 업로드, 다운 시 필요

**bash??**

이로써 리눅스에 kotlin을 설치하였다

터미널창에 **kotlin -version**으로 확인가능하다

![Day2%206e268f96d64b457fba71fced1ad5cbfa/day2_kotlin.png](Day2%206e268f96d64b457fba71fced1ad5cbfa/day2_kotlin.png)

================================================================

현재 day1.kt파일은 윈도우에, 실행해야는 곳은 virtual Box의 리눅스

따라서 윈도우에서 리눅스로 파일을 전송해줘야한다

우선 리눅스에서 scp설정을 해주기위해

Virtual Box →설정 → 고급 → 포트포워딩에서

다음과 같이 Rule2를 설정해준다

이때 포트번호는 22번으로 고정이다 (기본 ssh 포트는 22번)

![Day2%206e268f96d64b457fba71fced1ad5cbfa/Untitled%203.png](Day2%206e268f96d64b457fba71fced1ad5cbfa/Untitled%203.png)

그 다음 윈도우에서 cmd창을 열고 전송할 파일이 있는 경로로 간다

그 다음 

**scp day1.kt k043@192.168.56.1:/home/k043/backup**

연결이 되고나면 비밀번호를 k043계정의 비밀번호를 입력한다

성공하면 k043계정의 backup파일안에 day1.kt파일이전송된다

![Day2%206e268f96d64b457fba71fced1ad5cbfa/Untitled%204.png](Day2%206e268f96d64b457fba71fced1ad5cbfa/Untitled%204.png)

![Day2%206e268f96d64b457fba71fced1ad5cbfa/Untitled%205.png](Day2%206e268f96d64b457fba71fced1ad5cbfa/Untitled%205.png)

그 다음 실행시키기위해 

-include-runtime //실행가능한 jar파일 만들기

-d day1.jar // 생성하는 jar 파일 이름 설정

따라서 **kotlinc day1.kt -include-runtime -d day1.jar**를하면

![Day2%206e268f96d64b457fba71fced1ad5cbfa/Untitled%206.png](Day2%206e268f96d64b457fba71fced1ad5cbfa/Untitled%206.png)

day1.jar파일이 생긴것을 볼 수 있다

이제 이것을 java로 실행하면

**java -jar day1.jar**

![Day2%206e268f96d64b457fba71fced1ad5cbfa/Untitled%207.png](Day2%206e268f96d64b457fba71fced1ad5cbfa/Untitled%207.png)

다음과 같이 day1.kt파일은 Virtual Box의 리눅스에서 실행시킨 것을 볼 수 있다..

kotlinc컴파일러 이용해서 day1.jar라는 자바 바이트코드 모음으로 컴파일 한 뒤, java를 이용하여 JVM에 설치된 javac로 컴파일하는 순서

day1.kt → day1.jar(by kotlinc) → 실행(by javac)

================================================================

script 기본 문법

- #!/bin/bash // 해당파일을 bash쉘로 실행시키겠다는 의미
- $(date '+%Y') //현재 시간을 ' + %"포맷에 맞게 출력해준다
- 변수 사용시 '='앞 뒤에 공백있으면 안된다. 그리고 기본적으로 전역 string타입이다 ex) ${num}
- eq : 등호, -ne: not equal, # 주석

**압축 명령어**

tar -cvf 압축파일 이름 압축대상1 압축대상2 ...

**압축 풀기 명령어**

tar -xvf 압축파일

압축하는 script작성

파일명 "compressScript.sh"

![Day2%206e268f96d64b457fba71fced1ad5cbfa/script.png](Day2%206e268f96d64b457fba71fced1ad5cbfa/script.png)

복사하는 script작성

파일명 " copyScript.sh"

/var/log/syslog파일 접근 시 permission denied때문에 sudo로 명령어 실행

~~이때 계정 비밀번호 필요하기에 pipe로 비밀번호 전송 → 근데 안되는듯..~~

![Day2%206e268f96d64b457fba71fced1ad5cbfa/script%201.png](Day2%206e268f96d64b457fba71fced1ad5cbfa/script%201.png)

crontab -e에 등록

*/5 * * * * → 5분마다 실행

29, 59 * * * * → 매시간 29, 59분마다 실행

![Day2%206e268f96d64b457fba71fced1ad5cbfa/crontab.png](Day2%206e268f96d64b457fba71fced1ad5cbfa/crontab.png)

![Day2%206e268f96d64b457fba71fced1ad5cbfa.png](Day2%206e268f96d64b457fba71fced1ad5cbfa.png)

다음과같이 25분에 결과파일이 생긴것을 볼 수 있다

============================================================

리눅스에서 윈도우로 결과 가져오는 script

파일명 "toWindow.sh"

scp사용시 계정 비밀번호 필요하기에 pipe로 비밀번호 전송 ( 전송안된다..)

어떻게 해야하지....

![Day2%206e268f96d64b457fba71fced1ad5cbfa/script%202.png](Day2%206e268f96d64b457fba71fced1ad5cbfa/script%202.png)

**ssh-keygen**

공개키, 비공개키는 항상 한 쌍

공개키 : 자물쇠

비공개키 : 자물쇠 열쇠

공개키 등록 : 자물쇠를 걸어놓는다는 의미

공개키로 암호화된 데이터를 client는 자기가 가지고있는 비공개키로 데이터 확인 → 매번 인증필요

비밀키를 서버에 숨겨놓는다?

즉 비밀번호 계속 입력안해도 되게끔 비밀번호를 미리 등록해놓는 것. 암호입력보다 더 안전
