<Day01 - 0319>
<GitHub 사용법>

# Git 설치
 - git-scm.com 접속하여 64-bit Git for-Windows Set up 설치
 - cmd 창에서 설치 확인


# VScode 설치 (에디터 설치)
 - VScode 검색 후 접속하여 설치
 - VScode 설정, 폰트사이즈 테마변경 등


# cmd 명령어
 - 윈도우 버튼 누르고 cmd 검색하여 실행
 - cd -> 폴더(디렉토리) 이동 (change directory) 
            (ex) cd 이동할 경로
 - D: -> 드라이브 이동 
            (ex) D: = D디스크로 이동
 - cd.. -> 상위 경로(폴더)로 이동
 - cls -> 화면 지우기
 - dir /w -> 파일 또는 목록 보기
 - 3글자 + tab -> 파일명 겹치는 경우에 자동완성 기능


# Git 업로드 + 형상관리 
    (특정 작업한 시점을 기록)
 - #. 계정 연결  git config --global user.email "깃허브 가입 email"
                git config --global user.name "깃허브 가입 사용자명"
 - 1. git init 
        (저장소 생성. 로컬 레포지토리(로컬 저장소) 생성)
        * 보기 -> 표시 -> 숨긴항목 선택하면 .git 파일이 생성된 것이 표시됨
 - 2. git add .
        (스테이지 단계 / 파일을 올리는 단계)
        * 하나만 올릴 때는 git add . + 파일, 경로
        * 변경된 모든 파일 올릴 때는 git add .
 - 3. git commit -m "작업내용"
        (스냅샷 단계, 커밋 단계)
 - #. git log / git log --oneline : 한줄로 커밋 로그 확인
        (커밋 로그)
        * git log에서 못 빠져나갈 때는 알파벳q 누르기
 - 4. git branch
        * 현재 브랜치의 목록
        * 버전관리(형상관리)
        * git checkout 커밋ID : 입력한 ID 시점으로 돌아감
        * git checkout - : 직전 시점으로 이동
        * branch : 비슷한 성격끼리 묶어서 폴더를 나눈다.
 - 5. 브랜치 관리
        * git branch : 현재 브랜치의 목록
        * master : 기본 branch (기본적으로 만들어져 있음)
        * 새로운 브랜치 만들기 : git branch 생성할 브랜치 명 (현재 브랜치의 소스 -> 생성할 브랜치에 반영)
        * *가 있는 것은 현재 브랜치의 위치
 - 6. git checkout 브랜치명
        * 브랜치 변경
 - 7. git merge 병합할 브랜치명
        * 소스 합치기
        * 현재브랜치 <- 병합할 브랜치 소스
        * 최종본은 마스터에 병합
 - 8. 원격 브랜치 연결
        * 로컬 레포지토리 -> 원격 레포지토리 / 상태공유 (깃허브)
        * git remote add origin 원격 레포지토리 주소 -> 추가
        * git remote set-url origin 원격 레포지토리 주소 -> 변경

 - 9. git push origin 브랜치명
        * 로컬 저장의 브랜치를 원격 저장소의 브랜치로 상태 반영


# 집에서 작업할 때
 - 1. 폴더 생성
 - 2. git init
 - 3. git remote add origin 깃 주소
 - 4. git pull origin 원격 브랜치명
 - * git clone 원격 브랜치명 -> 위의 과정 모두 포함
 - 5. 작업 수정
 - 6. git add .
 - 7. git commit -m "변경 내용"
 - 8. git push origin 브랜치명


# pull request에서 설명 써서 master에 반영 
 - pull request
 - 작업에 대한 자세한 설명, 작업 내용 테스트 방법 등등 기록
 - master는 한명이 관리하는 것이 좋음


# master에 merge 하는 방법
 - 1. pull request
 - 2. New pull request
 - 3. 수정폴더 -> master 설정
 - 4. create pull request (이 버튼은 변경사항이 있을 때만 뜬다)
 - 5. 수정내용 기입 -> create pull request -> Merge pull request
 - 6. confirm merge (최종적으로 master에 반영) 


# 수정하다 충돌이 날 때
 - 1. git pull origin 브랜치명
 - 2. 충돌이 난 부분 확인 후 원하는 부분으로 수정
 - 3. git add.
 - 4. git commit -m "수정한 내용"
 - 5. git push origin 브랜치명


# 깃허브 브랜치 보호(잠금)
 - 1. settings
 - 2. Branches
 - 3. master 입력
 - 4. Require a pull request before mergind 체크
 - 5. Require approvals(승인횟수) -> 승인횟수 설정


# 작업 중 파란 글자 화면에 들어가면 나가는 방법
  - ESC + Shift + ; + q
  - 안되면 뒤에 ! 까지 입력 (강제로 빠져나가기)


# git tag
 - git tag 버전명칭 -> 생성 시점의 소스를 다운
 - git push origin 버전명칭 (v1.0.0)


# GUI - sorucetree
 - sourcetree 설치
 - 수정방법 : 파일상태 -> 스테이지에 올리기 -> origin/master에 바뀐 내용 즉시 푸시 -> 내용 입력 -> 커밋


# git ignore
  (원격 반영 배제)
 1. .gitignore 파일 생성
 2. 배제할 파일 이름 쓰기
 3. 폴더의 경우 -> /폴더명/
 4. 파일명.md -> 파일명으로배제
 5. 파일명.* -> 파일명이 같으면 확장자 달라도 모두 배제
 6. /폴더명/ -> 현재 경로의 폴더의 모든 파일 배제
 7. 폴더명/ -> 현재경로 포함 모든 경로의 이름이 같은 폴더의 파일 배제            



 
