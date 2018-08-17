
- 나는 누구, 여기는 어디?

  - 웹 크롤링을 위한 Concept map

  ![Web Crawling의 Concept Map](https://github.com/YoungestSalon/TIL/blob/master/concept-map.JPG?raw=true)



- 프로젝트를 시작하는 방법들

  - 다른 사람의 소스 코드를 복제(Clone) 해서 시작

    - github에서 “fork”하여 내 계정의 repository로 가져온다.
    - 내 계정의 repository를 “clone”하여 내 컴퓨터로 가져온다.
    - 개발 시작

    

  - GitHub에 빈 Repository를 만들고 시작

    - github에서 “Create Repository”를 해서 빈 repository를 만든다.
    - “clone”하여 내 컴퓨터로 가져온다.
    - 개발 시작

    

  - 내 컴퓨터에서 시작 

    - 내 컴퓨터에서 빈 폴더를 만든다.
    - “git init” 명령을 입력하여 일반 폴더를 git repository로 변환한다.
    - 개발 시작
    - github에서 “Create Repository”를 해서 빈 repository를 만든다.
    - 내 컴퓨터에서 git add remote 명령으로 origin을 등록하고 push 한다.
    - 계속 개발




- (실습) 프로그래밍 연습 

  - (참조) Git Bash 명령어

    ~~~
    1. cd : Change Directory
    2. mkdir : MaKE DIRectory
    3. pwd : 현재 작업 중인 디렉토리는 어디?
    4. ls : 폴더 안에 있는 파일들은?
    5. ls -a : 폴더 안에 있는 파일들은? (숨겨진 파일/폴더 포함)
    6. git init : git 폴더로 설정
    7. atom . : 현재 폴더를 Atom 편집기에서 Open
    8. touch (파일명) : 파일의 최종 수정일을 변경, (없는 파일명이면) 새로운 파일을 생성
    9. echo (파일 내용) > (파일명)
      - '파일 내용'을 집어넣은 파일을 새로운 파일로 생성
      - 파일명이 기존에 존재하는 파일인 경우, 기존 파일에 '파일 내용'을 덮어씀
      - Ex. echo Hello > test.txt : Hello라는 내용을 넣은 test.text 파일을 생성
    10. echo (파일 내용) >> (파일명)
      - 앞의 명령어와 동일
      - 단, 파일명이 기존에 존재하는 파일인 경우, 덮어쓰는 것이 아니라 추가함.
    11. git commit -am "메시지"
      - git add와 git commit을 동시에 처리해줌
      - 단, Untracked 상태의 파일은 commit 처리해주지 못함
    12. git commit -am -all "메시지"
      - git add와 git commit을 동시에 처리
      - Untracked 상태의 파일도 commit 처리해줄 수 있음
    ~~~

  - 실습 환경 Setting

    ~~~
    1. Git Bash : 폴더 생성, git init, 파일 생성
    2. Atom : 테스트 코드 파일 생성 (반드시 test_로 시작하는 이름으로 생성)
    3. Anaconda Prompt : 가상환경 생성, 단위테스트 라이브러리 설치, 테스트 코드 실행
       - 가상환경 생성 : pipenv --python 3.6
       - 단위테스트 라이브러리 설치 : pipenv install pytest ( test 로 시작하는 def 모두실행 )
       - 테스트 코드 실행 : pipenv run pytest (성공하는지 확인 필요)
    4. Git Bash : 프로덕트 코드 파일 생성, '.gitignore' 파일 생성, git add/commit
    ~~~
    

  - Atom 꿀팁

    ~~~
    1. 동일한 단어를 동시에 수정하도록 선택하기 : Ctrl+D (Win) / Command+D (Mac)
    2. 여러 줄을 한꺼번에 주석 처리 : Ctrl + / (Win)
    3. 여러 줄을 한꺼번에 줄여쓰기 : Ctrl+C로 선택 후 Tab (Win)
    4. 저장 : Ctrl + S
    ~~~

