# git공부 + wsl

### **github respository에 파일 추가하기!!**

### **레포지토리를 clone**해온다

1. 그러면 repository와 같은 이름의 폴더가생기는데 여기에 반영되는것이 다시 저장된다

### **레포지토리이름이랑 같은 폴더로 들어가서 여기서 git init**을해준다

(git clone해온 폴더상위에서 git init하고 push하면 submodule추가되서 파일 없어진다..명심!!)

1. git status로 변경사항 확인하고 git add . 해준다
2. 그다음 git commit하고 git remote add origin ~하고 git push origin 하면된다

### git push origin master -f 쓰지말기!! 덮어쓰기다!!

### **주의사항!**

clone해오지않고 특정 폴더만 추가할수는 없다 → 드래그앤 드롭밖에 없음

clone안하고 하려면 뭐 pull해주면되는데 clone이랑 다를게 없다

clone은 통째로 내려받기 + remote설정 자동으로

pull은 remote설정 되어있고, 변경사항 다운로드할때

아무튼 clone하고 작업해!!

### **git push할때 token**

git bash말고 linux나 터미널에서 git init하고 작업할때 원래 사용자 이메일, 비밀번호만으로 사용자 인증을 했다. 하지만 이제는 변경되어서 token을 써야한다

### **토큰 생성방법**

내 github → settings → Developer settings → Personal access tokens들어가서 토큰생성

Note : 토큰이름

Select scopes란 수행할 기능만. 주로  repo만 사용한다

그다음에 해당키 다른데 복사해놓고 git push할때 비밀번호 입력하라고하면 입력하면된다.

### **wsl(windows subsystem for linux)**

- 윈도우에서 리눅스 가상머신 설치안하고 리눅스 사용하게해준다
- 윈도우 & 리눅스 폴더 공유하는거

설치방법

[https://www.44bits.io/ko/post/wsl2-install-and-basic-usage](https://www.44bits.io/ko/post/wsl2-install-and-basic-usage) 참고!

[https://docs.microsoft.com/ko-kr/windows/wsl/install-win10#step-4---download-the-linux-kernel-update-package](https://docs.microsoft.com/ko-kr/windows/wsl/install-win10#step-4---download-the-linux-kernel-update-package) 참고!!

1. Windows Terminal 1,0설치
2. terminal 관리자로 실행해서 해당 명령어 입력

dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart

1. 재부팅한다음 terminal 관리자로 실행해서 wsl 입력
2. 링크나오는데 여기들어가서 Ubuntu 설치
3. Ubuntu실행하고 id, pw 입력(? 언제쓸까?)
4. Terminal에서 wsl -l -v하면 버전 1로 나올꺼다

[https://docs.microsoft.com/ko-kr/windows/wsl/install-win10#step-4---download-the-linux-kernel-update-package](https://docs.microsoft.com/ko-kr/windows/wsl/install-win10#step-4---download-the-linux-kernel-update-package)

위 링크들어가서 4단계 Linux 커널 업데이트 패키지 다운로드하고 실행한다

1. 그다음에 

wsl --set-version Ubuntu 2

wsl --set-default-version 2

wsl -t Ubuntu

입력해주고 다시 wsl -l -v로 확인하면 버전 2로 되어있을거다

그다음에 사용하면된다

wsl기본경로는 terminal에서 설정들어가서→ Ubuntu → '디렉토리를 시작하는중'을 원하는 경로로  바꿔주면 여기가 홈으로 된다. but Ubuntu에는 여전히 홈은 변경안되어있다

Ubuntu에서는 제일 상위로 올라가서 mnt폴더들어가면 여기가 windows, linux 공유폴더 있는위치다.

or 탐색기→ 작업하고 싶은 폴더 → 주소창에 wsl하면 해당위치에서 wsl 실행된다.