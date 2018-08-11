
### 오전수업

#### Git 과 Github 이해하기

- Slack chatbot 프로젝트 만들기
- `MIT라이센스` : 자유롭게 이용 가능하나 그로 인해 발생하는 문제는 책임지지 않음. 
- `GPL라이센스` : 무조건 gpl이 되어야 함.
- 라이센스가 명시되어있지 않다면, 원 저작권자에게 물어보아야 함.


#### 깃헙으로 깃 이해하기 실습

이번 수업에선 깃헙에 챗봇을 위한 레파지토리를 만들어 짝꿍과 함께 공동작업을 하는 방법을 익혀보았습니다. 

 - [실습] GitHub Repository와 Atom을 활용한 작업 @ Git Bash

    ~~~
    작업 경로 확인 : $ pwd
    폴더 변경 : $ cd 폴더명
    폴더 내의 파일 확인 : $ ls -als
    자신의 Repo를 Clone : $ git clone git@github.com:YoungestSalon/menubot.git
    자신의 Repo를 Atom에 띄움 : $ atom .
    수정 작업 (@ Atom : Ex. 문장 1개 추가 : print("Hello World!"))
    작업 내역 확인 : $ git status
    작업 내역 Add : $ git add main.py
    작업 내역 Commit : $ git commit -m "Hello World"
    작업 내역 Push : $ git push
    ~~~

  - [실습] GitHub Repository와 Atom을 활용한 협업 작업 @ Git Bash

    ~~~
    상위 폴더로 이동 : $ cd ..
    작업 경로 확인 : $ pwd
    폴더 내의 파일 확인 : $ ls
    동료의 Repo를 Clone : $ git clone https://github.com/YoungestSalon/Quotesbot
    동료의 Repo를 Atom에 띄움 : $ atom .
    수정 작업 (@ Atom)
    변경 내역 확인 : $ git diff
    작업 내역 확인 : $ git status
    작업 내역 Add : $ git add --all
    작업 내역 Commit : $ git commit -m "Add sentence"
    작업 내역 Push : $ git push
    Pull request 생성 (@ WEB : GitHub Repository) 
    
    참고) 현재 디렉토리의 작업 내역을 모두 삭제하는 경우 : $ git checkout --.
    ~~~

  - [실습] GitHub Repository Pull Request에서 Conflict가 발생한 경우 대처 방법 @ Git Bash

    ~~~
    [각자 작업]
    자신의 Repo로 이동 : $ cd 폴더명
    자신의 Local Clone을 최신화 : $ git pull
    자신의 Local Clone에 대한 수정 작업 + 작업 내역 Add - Commit (* Push는 제외)
    동료 Repo의 Local Clone으로 이동 : $ cd 폴더명
    동료의 Local Clone에 대한 수정 작업 + 작업 내역 Add - Commit - Push
    자신의 Local Clone 수정 작업에 대한 Push : Conflict가 발생
    
    [Conflict가 발생한 Pull Request를 올린 사람(=Fork해서 작업한 사람)이 작업]
    * 참조 : Conflict가 발생한 경우, PR을 날리는 쪽에서 해결해주는 것이 관례
    동료의 Local Clone으로 이동 : $ cd 폴더명
    동료의 원본 Repo(Fork한 Repo 아님!)를 upstream으로 설정 : $ git remote add upstream https://github.com/Yoonkimove/Quotesbot
    동료의 원본 Repo에서 최신본을 다운로드 받아 임시폴더에 저장 : $ git fetch upstream
    다운로드 받은 임시폴더의 최신본 + 기존의 작업 내역 : $ git merge upstream/master → 당연히 Conflict가 발생함
    수정 작업 (@Atom) : '<<<<<<< HEAD', '=======', '>>>>>>> upstream/master'의 형태로 충돌이 발생한 부분을 알려줌 → 충돌 해소 : 양자택일 or 합치기
    수정 작업 내역에 대한 Add - Commit - Push : 기존에 올린 PR의 Conflict가 해소됨
    Merge : 
    ~~~



### git, github, gitbash 이용하기

#### 깃헙 레퍼지토리

- 깃헙 이용 시, `create a new project`(우측 상단 초록색 버튼)을 누르게 되면 깃헙 서버에 새로운 내 레퍼지토리가 생성됩니다.
- 다른 사람의 레퍼지토리를 가져오고 싶은 경우, 해당 레퍼지토리에서 `fork`를 눌러 본인의 레퍼지토리로 포크해 올 수 있습니다.



#### 로컬 PC로 클론 받아오기

새로 생성하거나, fork해 온 레퍼지토리를 로컬 PC에서 작업하기 위하여 클론을 받아와야 합니다. 

>  fork란, 깃헙 자체에서 편의상 이용되는 개념으로, 깃헙 상에서 다른 사람들의 레퍼지토리를 나의 깃헙 공간으로 clone해 오는 것을 말합니다.

- 먼저, 깃헙에서 로컬로 클론받아 올 레퍼지토리를 눌러 SSH key 주소를 복사합니다. (SSH key 주소는 초록색 `Clone or Download`버튼을 눌러 확인할 수 있습니다.)

- 레퍼지토리 폴더를 생성할 로컬 경로로 가서 git bash를 실행시킵니다.
- `git clone 클론받아올 레퍼지토리의 주소` 를 입력하면 자동으로 깃으로 관리되는 로컬 폴더가 생성됩니다.

git 을 클론해오변 원래의 저장소에는 origin이라는 이름을 붙여줍니다.



#### 로컬에서 편집한 파일을 git으로 관리하기

로컬 PC에서 여러가지 파일들을 수정 및 생성한 후 깃헙에 업로드합니다.

- `git init`: 만약 폴더를 새롭게 생성한 경우, git으로 관리하기 위하여 적어줍니다.

- `git status` 여러가지 현재 로컬 파일의 정보들을 확인해 볼 수 있습니다. 새로 생성된 파일이 untracked 상태임을 알 수 있습니다.
- `git add 파일명`: untracked 상태였던 파일을 tracked 상태로 올립니다.

실습 시간에 로컬 PC에서 새로 생성하여 작업했던 main.py 파일을 변경한 다음, 다음을 수행해 봅니다.

```bash
$ git status
On branch master
Your branch is up to date with 'origin/master'.

Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        new file:   main.py

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   main.py
```

```bash
$ git commit -m "Hello world 작성"

$ git status
On branch master Your branch is ahead of 'origin/master' by 1 commit. (use "git push" to publish your local commits)

nothing to commit, working tree clean
```

터미널을 이용하여 커밋을 해 주었기 때문에 `git status`를 확인해 보니 커밋할 것이 없는 상태입니다.

- `git push`:  origin의 master로 push되어 깃헙에 반영됩니다. (레퍼지토리 생성 시 따로 지정해주지 않으면 master브랜치가 기본 브랜치로 설정됩니다.)

##### git으로 파일 관리하기의 과정

1. 파일을 생성하고 수정합니다. 
2. 해당 파일은 현재 untracked & unstaged 상태입니다.
3. add 해 주면 tracked & staged 상태로 변경됩니다.
4. 또 다시 파일을 수정합니다.
5. 해당 파일은 tracked 이지만, modified(unstaged) 상태로 변경됩니다.
6. add 해 주면 tracked & staged 상태로 변경됩니다.
7. 파일을 commit 합니다.
8. 해당 파일이 committed 상태로 변경되어 github의 기록에 남습니다.



#### 다른 사람의 프로젝트에 기여하기

포크해 온 다른 사람의 레퍼지토리를 내 로컬PC로 클론 받아옵니다.

- `git add upstream 다른 사람의 레퍼지토리 주소`: 다른 사람의 레퍼지토리를 upstream 으로 설정해줍니다.

  ('down'load와 'up'load처럼, 이 경우에는 'up'stream이 본래의(다른 사람의) 레퍼지토리가 됩니다.)

- 본인의 로컬 PC에서 수정한 파일을 origin(본인의 깃헙)으로 add, commit, push해 줍니다.

- 본인의 깃헙 계정의 해당 레퍼지토리로 이동하여 pull request를 생성합니다.

- 상대방이 해당 request를 읽어 본 후, 의견을 조율하여 merge를 해 준다면 완료!



#### 여러가지 git 명령어들

- `pwd`: print working directory
- `ㅣㅣ`: 현재 디렉토리의 폴더 리스트가 보여집니다.
- `-v`: 'verbal'의 의미로, 더 자세하게 설명해줍니다.
- `[tab]`: 'tab'버튼은 전체 파일명을 입력하지 않아도 앞 몇 글자만으로도 파일명을 쉽게 입력할 수 있게 도와줍니다.
- `git diff`: 수정된 내용이 보여집니다.
- `git status `: 현 상태에서 자주 사용하는 git 명령어를 함께 출력해 줍니다.
- `git checkout -- main.py`: 파일을 수정하기 이전 버전으로 돌아갈 수 있습니다. (commit된 상태의 파일들은 대부분 기록이 남지만, add만 되어 있는 상태의 파일들의 기록은 남지 않습니다.)
- `git fetch upstream`: git ignore파일 어딘가에 upstream의 수정된 내용을 임시로 저장해 둡니다. (upstream의 실제 커밋을 내 로컬PC 어딘가에 저장해둡니다. working directory에 반영되지는 않습니다.)
- `git merge upstream/master`: 변경된 내용들을 merge해 줍니다. (현재 브랜치와 fetch에서 받아온 것들을 합쳐줍니다.)
- `--rebase`명령어는 위의 과정들을 깔끔히 해 주는 굉장히 강력한 도구이기 때문에 잘 사용해야 합니다.



#### 아나콘다 프롬프트로 파이썬 실행하기

- `cd 경로`: 실행할 파일이 있는 폴더로 이동해줍니다.
- `python 실행할파일명.py`로 파이썬 파일을 실행시켜 줍니다.
  - `ctrl+c`를 눌러 실행을 종료합니다.
- `python`: 현재 파이썬 버전을 확인합니다.
  - `quit()`으로 중단합니다.
