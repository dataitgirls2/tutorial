#### This is made by Chaewon Kang, Sunmin Park, Yewon Jeong (Team A) for making Daitgirls' Github Tutorial.

# Tutorial 01 (0628, Thu)

## A. [수업 내] Github 실습 관련 내용

### (1) markdown (마크다운)

* 마크다운이란 무엇인가?

Markdown은 텍스트 기반의 마크업언어로 2004년 존 그루버에 의해 만들어졌다. 쉽게 쓰고 읽을 수 있으며 HTML로 변환이 가능하다. 특수기호와 문자를 이용한 매우 간단한 구조의 문법을 사용하여 웹에서도 보다 빠르게 컨텐츠를 작성하고 보다 직관적으로 인식할 수 있다. (출처: https://gist.github.com/ihoneymon/652be052a0727ad59601) 


* 마크다운의 파일 확장자는 .md 이다. e.g.) filename.md (from BLUENCE’s 0628 TWL)


* 마크다운 문법은 아래의 링크에서 참고하자. 문법을 활용하여 다양한 형태를 구현할 수 있다. 
https://gist.github.com/ihoneymon/652be052a0727ad59601
https://guides.github.com/features/mastering-markdown/


### (2) repository (저장소)

* 레퍼지토리란 무엇인가? 

레퍼지토리는 파일들을 저장하는 일종의 폴더이다. 쉽게 생각하면 개인 GitHub 계정에 생성하는 하나의 ‘저장 폴더’라고 생각하면 된다. 나의 로컬 환경 안에 생성하여 작업할 수 있다. GitHub메인 화면에서 repository 탭으로 들어가 New 탭을 통해 새 repository를 설정할 수 있다. 

* 깃헙에서 repository 생성 시 옵션

public으로 공개할 경우 무료이고, private은 유료이므로 주의한다. 우리 수업에서는 MIT license(수정/배포 자유, 실무 혹은 상업적 이용 가능, 오류발생 시 법적책임 없음)를 이용하여 생성하였다. (from Dayounghong’s 0628 TWL) 

* What is Repository? 

Repository is a location where all the files for a particular project is stored. Each project has its own repository, and one can access it with unique URL.  (from SaeromB’s 0628 TWL) 

* 오늘 수업에서 생성한 repositories?

수업 진행 중 세 개의 repositories 를 만들어 보았다. 

첫번 째, TIL repository는 내가 만든 나의 저장소로, 나의 로컬 (나의 컴퓨터 환경)에서 이용 가능하며 다른 사람들과 공유하지 않는 repository이다. 우리는 매일 각자가 커밋한 것을 TIL repository에 반영하여, 일일 커밋을 실행한다. 

두번 째, TWL repository는 daitgirls2 organization 에서 yebin 님이 만든 repository이며 데잇걸즈 전원이 권한을 가진다. 우리는 매일 배운 수업 내용을 TWL repository에 반영하여, tutorial making에 협력한다. 

tutorial repository는 daitgirls2 organization 에서 yebin 님이 만든 repository이며 이 또한 마찬가지로 데잇걸즈 전원이 권한을 가진다. 정해진 각 조는 돌아가면서 TWL repository에 반영된 내용을 정리하여 tutorial로 만든다. 정리된 내용이 완성되면 깃북을 통해서 복습과 실습에 참고할 수 있는 형태로 출력된다. 

### (3) fork (포크)

* 포크란 무엇인가? 

다른 사람이 생성한 repository를 fork하여 나의 로컬 환경으로 가져올 수 있는 기능이다. Git 시스템 상에서는 clone 기능과 상통한다. fork 해온 repository 안에서 fork 해 온 당시의 상태를 기준으로 액션들을 실행할 수 있다. 

### (4) pull request (풀 리퀘스트 a.k.a 풀리퀘)와 merge (머지) 

* 풀 리퀘스트란 무엇인가? 

" 수정했으니 반영해줘! ", " 내가 반영한 내용을 검토해봐! "

여러명이서 관리하고 있는 repository 안에서 자신이 실행한 액션들을 반영하기 위해, 해당 repository의 상위 관리자 (merge 기능을 가진 사람)에게 '반영 요청'을 보내는 것을 풀 리퀘스트, 줄여서 풀리퀘라고 한다. 

* 머지란 무엇인가?

" 그래, 합쳐줄게. ", " 이 내용 괜찮으니 반영해도 되겠어. "

머지는 머지 권한을 가진 사람이 실행할 수 있는 기능으로, 풀 리퀘스트를 파악한 후 그러한 사항을 반영할 것인지 말 것인지를 결정하고 허락하는 행위이다. 

(from BLUENCE's 0628 TWL) 

* 우리 수업에서는? 

우리 수업에서는 TWL 폴더의 merge 기능을 모두가 가지고 있으므로, 자신이 자신의 로컬 환경 (개개인의 github 페이지)에서 반영한 수정 사항들에 대해 daitgirls2 (중앙 관리 기구)에 풀 리퀘스트를 보내고, 스스로 머지 허락을 할 수 있다. 

### (4) issue (이슈)

* 이슈란 무엇인가?

프로젝트에서 개선되거나 해결되어야할 것을 의미한다. 이슈는 제목과 설명을 기입하고, 이슈가 할당되는 사람(처리해야 하는 사람), 기한 등을 입력해 등록하게 된다. 

- @+'사용자아이디'를 사용하여 참여시키고 싶은 사람을 언급할 수도 있다. 

- 이슈를 게시할 경우 고유한 넘버가 생성되며, 넘버는 '#'+'숫자'의 형태로 발생한다. 

- 어떠한 활동을 통해 full request를 보낼 때, 특정 이슈에 관한 사항임을 알리고자 할 경우 생성된 고유 넘버를 태깅해서 나타낸다.


### (5) Sourcetree (소스트리) 

소스트리는 내 로컬 컴퓨터의 자료와 깃헙을 연결해주는 프로그램으로, **SSH Key**를 생성해 로그인없이 편리하게 연동이 가능하다.
로컬에서 Git을 수정하면 Github에 자동으로 업데이트 되지 않으나 소스트리를 이용하면 이것이 가능해진다.

## B. [수업 내] 배로 선생님의 강의 관련 내용 

### (1) TIL (Today I Learned) 로 일일 커밋하기 
- 다른 사람의 저장소 따라하기
- Stack Overflow에서 배운 코드를 타이핑 (주의 : Ctrl C+V 하면 안됨)
    * Stack Overflow : 개발자들의 지식iN. https://stackoverflow.com/
- Kaggle에 있는 튜토리얼 따라하기
    * Kaggle (캐글) : 데이터 사이언티스트들의 지식iN 겸 경진대회장. https://www.kaggle.com/
- 책에서 본 코드를 따라 써보기
    * 각 IT출판사(길벗, 한빛미디어 등)의 베타리더, 리뷰어 모집에 응모해서 당첨된 책의 소스 리뷰하며 따라쓰기
- 간단한 튜토리얼 번역해보기 (ex. 장고걸스 튜토리얼)
- 스프린트 참여하기
    * 스프린트 : 오픈소스 발전에 기여하기 위해 현재 이슈 해결에 참여하는 것. 파이썬 한국 사용자 모임에서도 진행한다.
- 정적 블로그 운영 
    * 정적 블로그 : '~.github.io' 주소로 되어있는 블로그. 입문자용 튜토리얼을 참고하거나, 잘 만들어진 테마를 Fork해서 만들 수 있다.
    

### (2) 기타 Tips 
- 마크다운 문서 편집 : PC 브라우저/휴대전화로도 가능하므로 일일 커밋이 끊기지 않게 할 수 있다.

## C. [수업 외] 기타 

### (1) 애란 선생님의 부가설명 
 
 - 내 로컬 환경에 폴더를 하나 만든다. 그 폴더에 특정 파일을 넣을 경우, 자동으로 그것이 repository로 인식된다.
 - 그 repository 는 크게 두 영역으로 구분된다. untracked 영역, tracked 영역,
 - repository 에 파일 A 를 넣을 경우 A 는 untracked 영역으로 들어가게 되고, 이 때 A 는 Git 과는 관련없는 개체들이다.
 - 그러나 A 에 add 를 실행할 경우 A 는 tracked 영역으로 옮겨지며, 이 때 부터 버전 관리가 가능하게 된다.
 - add 는 ntracked 영역에 있는 개체들을 tracked 영역으로 옮기기 위해 실행하는 명령이다. 
 - tracked 영역은 다시 staged 와 unstaged 로 나뉜다.
 - staged 는 파일이 '영구히 저장될 준비'가 되었다는 것을 뜻한다. 즉, add 를 실행하면 파일은 untracked 에서 tracked + staged 로 이동한다.
 - tracked + staged 에 놓인 파일 A 를 수정해서 A'를 만들면, A'는 tracked + unstaged로 이동한다.
 - tracked + unstaged 에 놓인 파일 A' 를 tracked + staged 영역으로 옮길 때도 add 를 실행한다.
 - 즉, add 는 tracked + staged 로 옮길 때도 사용하고, tracked + staged 상태에서 수정을 가해 tracked + unstaged 로 간 것을 다시 tracked + staged 로 이동시킬 때에도 사용한다.
 - 이러한 결과를 '영구히 저장'하고자 할 때 commit 을 한다.
 - commit 은 tracked + staged 영역에 놓인 내용들이 통째로 복사가 되어 duplicated 되는 것을 뜻한다.
 - commit 을 하는 순간, 옛 버전은 v1이 되고, 현재 버전이 v2가 되는 것이다. 이런 식으로 v3, v4, v5, ... 식으로 버전관리가 실행된다.
 - 이것이 Git의 시스템이다.
 - 이러한 시스템은 나의 로컬 환경 (나의 컴퓨터)에서 실행 가능하며, 다른 사람의 로컬 환경 혹은 내 컴퓨터의 다른 폴더로 가져가고자 할 때 clone 기능을 쓴다.
 - 그러면, tracked + staged 영역의 현재 버전과 이전의 히스토리까지 전부 복사된다.
 - 복사된 정보들을 다른 로컬 환경에서 수정하면, v6이 생기는데 이 버전은 상위 환경에는 적용되지 않은 상태이다.
 - 그렇기 때문에 v6을 당겨가라고 요청하는 것이 pull request이고, 상위 로컬 환경의 주체가 pull request 를 승인하는 것이 merge 이다.
 - 머지하게 되면, 원격으로 떨어져 있는 로컬 환경들에서 같은 버전을 보게 된다.
 - 우리 실습의 경우 add 등의 과정을 거치지 않았고, Github 서버에서 파일을 생성-수정하는 것이 add 가 실행된 것으로, 보이지 않았을 뿐.
 - fork 는 Git 에는 없는 용어로, Github 에 있는 repository 를 다른 github 서버로 옮겨가는 것이다. clone 의 개념이 github 에 적용된 것이라고 보면 됨.
 - 즉, 우리가 중앙 기구 (중앙 로컬 환경)으로 설정한 것이 daitgirls2 repository 인 것. Github 시스템 하에서의 약속과 같다.
 

![Image of Diagram](https://git-scm.com/figures/18333fig0201-tn.png)

![Image of Diagram](http://images.abizern.org/365git/March10/GitObjects01.png)

![Image of Diagram](http://file.instiz.net/data/file/20121229/8/b/1/8b1c7f28c9d3c548de466dc9b038d254)

 ### (2) 배로 선생님의 수업 관련 보충자료 
 
 - [github-cheat-sheet/README.ko.md](https://github.com/tiimgreen/github-cheat-sheet/blob/master/README.ko.md)
 - [누구나 쉽게 이해할 수 있는 Git 입문! 버전 관리를 완벽하게 이용해보자! Backlog](https://backlog.com/git-tutorial/kr/)
 - [git - 간편 안내서 - 어렵지 않아요!](https://rogerdudler.github.io/git-guide/index.ko.html)
 - [Git - Book](https://git-scm.com/book/ko/v2) 
 - [어떻게 깃을 사용하는지 빠르게 알아봅시다](https://www.pigno.se/barn/tutorial-git/docs/#/) 
 - [Hello World · GitHub Guides](https://guides.github.com/activities/hello-world/) 
 
### (3) Git 이란 무엇이고, Github 은 무엇인가? 

* Git이란?

프로그램 등의 소스 코드관리를 하는 버전 관리 프로그램

* Git을 사용하는 이유?

한마디로 작업의 기록을 남겨서 수정 및 보완 등의 이력을 추적하기 위함이다. 이는 사람들과의 협업을 용이하게 한다.

(ex: 파일의 수정을 여러 번 생성해서 `파일명_최종.txt`, `파일명_진짜_최종.txt’, `파일명_진짜_최종_마지막.txt` 등의 이름을 붙여 사용하지 않아도 된다는 편리함이 있음)

* GitHub이란?

Git이 프로그램이라면 GitHub는 파일의 버전 관리를 다른 사람들이 볼 수 있게 정보 교환이 이루어지는 일종의 서버(홈페이지)라고 볼 수 있다.

* GitHub을 사용하는 이유?

협업을 하고 소스에 대한 이력관리를 하고 소셜코딩을 할 수 있음. 

다른 사람들이 개발한 코드를 볼 수 있고, 진행되고 있는 프로젝트에 함께 참여하며 수정 및 보완 작업을 통해 협업할 수 있음 (위에 설명된 fork,pull request,merge를 통해)

(Git과 GitHub관련 개념 설명 http://jinfactory.tistory.com/187)

