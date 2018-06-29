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

### (4) full request (풀 리퀘스트 a.k.a 풀리퀘)와 merge (머지) 

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

- 

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

### (2) 배로 선생님의 수업 관련 보충자료 

### (3) Git 이란 무엇이고, Github 은 무엇인가? 

