# Day9-학습정리

**VCS(Version Control System)- 버전 관리 시스템**

local VCS : 로컬 버전 관리 시스템 

간단한 db를 이용해서 파일의 변경 정보 관리

- RCS : 기본적으로 patch set(파일에서 변경되는 부분)관리

centralized VCS : 중앙집중식 버전 관리 시스템 - 협업

파일을 관리하는 서버가 별도로 있고 클라이언트가 중앙 서버에서 파일의 마지막 스냅샷 사용

관리자가 프로젝트 참여자 관리 용이 but 서버 다운되면 그동안 협업 x + 하드에 문제 생기면 모든 프로젝트 잃을 수 있다

- Subversion(SVN)

SubVersion의 줄임말. 형상관리/소스 관리 툴

SVN서버의 Trunk에 프로젝트 소스 위치 → Local에서 작업 후 commit. branch, merge기능 존재

- CVS, Perforce, ClearCase, TFS

distributed VCS : 분산 버전 관리 시스템 - 협업

클라이언트가 파일 스냅샷 가져오는 것이 아닌 저장소 자체 복제 → 이걸로 서버 복구가능

리모트 저장소가 존재하며 저장소가 많을 수도 있다. → 동시 다양한 그룹, 방법으로 협업 가능

- Git : Github. 쉘 스크립트 이용해 기본기능 조합 → 편리한 기능 생성
- Mercurial : Git과 유사 but 편리한 기능들이 번들 확장에 존재.
- BitKeeper : SVN과 비슷한 중앙 통제 방식 → 대규모 프로젝트에서 빠른 속도

## **git Area**

**working directory**

소스코드 작업 영역. 코드 추가, 수정, 삭제 이루어지는 영역

**staging Area**

- wd에서 add명령어 실행하면 해당 영역으로올라온다.
- 소스코드 상태정보 (modified, unmodified )확인가능

**git Area**

staged Area에서 commit명령어 실행하면 git Area영역에 반영된다

## **파일 상태**

untracked : wd에 추가되었지만 git에서 관리 x

unmodified : 신규로 파일 추가되었을 때 상태. staged에서 commit 이후 상태

modified : 파일 추가 이후 파일 수정된 상태

staged : git의 staging area에 반영된 상태

실제 git 명령어와 구현 명령어 차이

add

내 코드 : 마지막 스냅샷 사용

실제 : 지속적으로 추적

commit 

staging영역 → git 영역으로 이동

메모기능

push

remote저장소로 저장

**얕은 복사**

원본 변경 시 사본 변경내용 자동 update

객체 주소값 복사

같은 객체 공유하므로 메모리 절약 + 빠르다(?)

add명령어 → 파일 추적에서 사용되지 않을까..

**깊은 복사**

복제

객체 실제 값 복사

branch나 clone같은거