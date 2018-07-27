## 2018년 6월 29일 오후 수업

---

**Push**
내 PC의 로컬 저장소에서 변경된 이력을 원격 저장소에 공유하려면, 로컬 저장소의 변경 이력을 원격 저장소에 업로드해야 합니다.

**Clone**
저장소를 복사하는 행위. 복제란 원격 저장소의 내용을 통째로 다운로드하는 것을 말합니다. 복제한 저장소를 다른 PC에서 로컬 저장소로 사용할 수 있게 됩니다.

**Pull**
원격 저장소에서 로컬 저장소로 업데이트하려면 풀(Pull)을 실행합니다.pull 을 실행하면, 원격 저장소에서 최신 변경 이력을 다운로드하여 내 로컬 저장소에 그 내용을 적용합니다.


이번 실습은 로컬 폴더의 자료를 깃을 이용해 버전을 컨트롤하고 그 변경 사항을 깃헙에 push하는 과정을 헌법개정안 자료를 이용하여 실시하였습니다.

### Gitbash

깃을 설치했다면 터미널을 이용해 직접 디렉토리에 변경을 가하고 바로 원격저장소(remote = github in this case)에 올리는 작업을 하게 됩니다. 
이것을 하는 곳이 바로 Git bash. Git bash는 google에 검색하여 맞는 OS, 34/64bit에 맞춰 설치합니다.


### 실습01 - 1987년 헌법개정안으로 git, remote, add, commit, push 이해하기

1. 다음의 링크에서 파일을 다운로드 받습니다. 파일명이 같기 때문에 1987년 파일을 먼저
받습니다.
https://drive.google.com/drive/u/0/folders/11REn11b5WaOTWVeHy-T3ddM48_Y_P7CB

2. git으로 관리할 폴더를 로컬(내 컴퓨터)에 하나 생성합니다. 폴더명은 constitution-kr 로 합니다.

> **주의 사항**
>
> 중간 경로에 띄어쓰기가 된 이름이 없도록 유의하자.

3. git init 을 합니다.

4. git add “대한민국 헌법.txt” 로 git 으로 관리할 파일이라는 것을 지정해 줍니다. (여기에 있는
따옴표와 커밋하는 따옴표는 다르기 때문에 복붙하시지 말고 직접 타이핑 합니다.) 

5. git commit -m “1987년 헌법" 으로 커밋 메시지를 작성하고 커밋합니다.
-m 이라는 옵션은 메시지를 뜻하며 옵션에 대한 도움말은 git commit -h 로 볼 수 있습니다.
git 명령어 -h로 대부분의 명령어에 대한 옵션 도움말을 볼 수 있습니다.

6. 여기까지 로컬 컴퓨터에 있는 파일에 1987년 헌법 파일을 생성했습니다.

7. 그럼 github으로 돌아가서 동일한 명칭으로 constitution-kr 이라는 저장소를 생성합니다.

> **참고**
>
> 다음은 리드미 파일을 만들지 않고 아무런 옵션도 체크하지 않고 레파지토리를 만들었을 때 깃헙이 주는 안내다.
밑에 적힌 코드를 깃배시를 통해 constitution-kr 디렉토리를 찾아들어가 입력하면 
"# constitution-kr"이 적혀진 README.md파일이 생성되어 깃헙에 푸시될 것이다.
>
> echo "# constitution-kr" >> README.md
>
> git init
>
> git add README.md
>
> git commit -m "first commit"
> 
> git remote add origin https://github.com/pje1740/constitution-kr.git
>
> git push -u origin master

8. git remote add 로 리모트 저장소를 추가합니다.


---

**윈도우 SSH key**

지난 수업을 통해 소스트리를 이용한 ssh키 습득고 인증은 오류가 발생한다는 걸 알 수 있었다. 

8번의 리모트 저장소는 git@로 시작하는 ssh key 주소를 의미한다. 

다음은 윈도우를 위한 ssh key 등록 방법이다. 



1. ssh key를 가지고 있는지 확인을 먼저 해보자. 깃배시에서 다음과 같이 입력한다.
> cd ~/.ssh

숨김설정 된 파일도 보기 위해 다음을 입력한다.

> ls -al

주소에 id_rsa.pub, id_rsa 파일이 있어야지 ssh key를 가지고 있는 것이다.
id_rsa.pub 에 있는 key 가 github 에 등록되어 있어야 ssh 프로토콜을 사용할 수 있다.

2. 현재 작업 중인 디렉토리로 cd를 이용해 돌아오자.

git config --list를 깃배시에 입력하면 여러 줄이 뜨는데 이 때 밑에 remote.origin.url=<주소>가 있다.

일전에 https링크로 연동해두었다면 https링크가 적혀있을 것이다.

3. 깃헙으로 돌아가자. 

Settings > SSH로 가면 이전에 등록했던 ssh key가 있는데 삭제하고 다시 등록을 해야한다.

이곳에 기입할 ssh key는 깃배시에서 다음을 입력하여 얻을 수 있다.

> ssh-keygen -t rsa -b 4096 -C "계정주소"

이 뒤에 따라오는 부분은 추가적인 메세지를 생성할지에 대한 옵션인데 없다면 엔터로 넘어가자.

이제 생성이 됐다면 

> :q

를 입력하여 그 화면을 나가자. 

직접 코드를 복사해도 좋지만 간단하게

> clip < ~/.ssh/id_rsa.pub

를 입력하여 클립보드에 복사하자.

이후 깃헙에 코드를 붙여넣고 ssh key를 연동하자.

generating new ssh key는 다음의 주소에서 조금 더 자세하게 과정을 볼 수 있다.

https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/

4. 다시 깃배시로 돌아오자.

> git remote set-url origin <레파지토리의 ssh주소>

를 입력하여 깃헙과 로컬을 ssh로 연동하자.

이 과정에 정확히 됐는지 확인하려면

git remote -v를 입력해보면 된다.

이 때 
> origin <레파지토리의 ssh주소>

가 뜬다면 성공!

4번의 과정은 다음 링크를 참조하여도 좋다.

https://help.github.com/articles/changing-a-remote-s-url/

**여기까지 SSH KEY 연동 방법이었습니다**

---

9. 이제 로컬에 있는 파일을 github으로 관리할 수 있도록 push 해줄게요. git push -u origin master
위에서와 마찬가지로 git push -h 로 옵션에 대한 설명을 볼 수 있습니다.
보통 업스트림을 의미하는 -u와 강제로 푸시하는 -f 를 주로 사용할 예정입니다.

> **origin? master?**
> 
> master란 내 로컬 마스터 브랜치를 의미한다.
> 
> origin이란 원격저장소(깃헙)의미한다. 
> 
> 즉 git push -u origin master는
> 
> 내가 마스터 브랜치에서 수정한 사항을 오리진으로 푸시해서 업데이트 해달라는 요청이다.
> 
> 문법적인 부분은 다음 링크를 참고하면 좋다.
> https://stackoverflow.com/questions/18137175/in-git-what-is-the-difference-between-origin-master-vs-origin-master (참고)

10. github 으로 가서 해당 파일이 업데이트 되었는지 확인해 봅니다. 


실습01 정리) git bash에 타이핑할 1~10번까지의 전체 소스 코드입니다.
> git init
>
> git add "대한민국 헌법.txt"
>
> git commit -m "1987년 헌법"
>
> git remote add origin https://github.com/oranjieunk/constitution-kr.git
>
> git push -u origin master
>

**오류 해결 방법**
오류 메시지를 그대로 google에 검색하고, 해결 방법을 탐색해 봅시다.
예) Updates were rejected because the remote contains work that you do not have locally
가 뜨는 경우가 있는데 마지막에 git push -u origin master대신에 git push -f origin master를 사용하면 됩니다.

### 실습02 - 2018년 헌법개정안으로 브랜치 이해하기

1. 2018년 헌법개정안 파일을 다운로드 받습니다.
https://drive.google.com/drive/u/0/folders/11REn11b5WaOTWVeHy-T3ddM48_Y_P7CB

2. git checkout -b “2018” 로 만듭니다. (가끔 터미널에서 한글 인코딩 문제로 오류가 발생하기
때문에 영문과 숫자로만 사용하는 것을 권장합니다.) 해당 명령어는 브랜치를 만들고 변경해
주는 역할을 합니다.
[Git - 브랜치란
무엇인가?]( https://git-scm.com/book/ko/v1/Git-%EB%B8%8C%EB%9E%9C%EC%B9%98-%EB%B8
%8C%EB%9E%9C%EC%B9%98%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B
0%80%3F )

3. git branch 명령어를 실행하면 2개의 브랜치 목록이 나오며 활성화 되어 있는 브랜치 앞에
별표가 표시됩니다.

4. git checkout master 를 해보면 다시 마스터 브랜치로 이동하고, git checkout 2018로 2018
브랜치로 이동합니다.

5. 브랜치를 이동한 상태에서 다운로드 받은 2018년 파일을 이 폴더로 옮겨줍니다.
즉, 덮어씁니다.

6. git add “대한민국 헌법.txt” 로 변경상태를 Stage 상태로 보냅니다.
스테이지로 보낸다 함은 index로 집어넣는 개념과 동일. add문을 쓰고 있으니.

7. git commit -m “2018년 개정안" 으로 커밋 메시지를 작성하고 커밋합니다.

8. git push -u origin 2018 로 깃헙에 푸시합니다. (1987년 과정과 브랜치가 다릅니다.)

9. github 으로 가서 2018 브랜치를 master 브랜치로 pull request를 생성합니다.
이 pull request메시지는 깃헙에서 새로고침 해보면 상단에 바로 표시가 된다.

실습02 정리) git bash에 타이핑할 1~9번까지의 전체 소스 코드입니다.
> git checkout -b 2018
>
> git add "대한민국 헌법.txt"
>
> git commit -m "2018년 개정안"
>
> git push -u origin 2018
>
=> github 페이지에서 Pull request 생성하고, Merge하기

이전 실습에서는 포크해온 저장소에 풀리퀘스트를 보냈지만, 이번에는 같은 저장소에서 다른
브랜치를 통해 풀리퀘스트를 생성했습니다.
