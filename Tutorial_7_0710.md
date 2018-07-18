# Jekyll 과 루비 

Jekyll은 루비로 만들어졌어요. 블로깅 때문에 루비를 설치해야하는 것이 조금 부담일 수도 있지만, 
설치해서 사용하면 더 다양한 기능을 사용할 수 있어요. 


__루비와 파이썬__  
루비는 인터프리터 형식으로 실행되는 고기능 스크립트 언어이자 뛰어난 객체 지향적 언어이다. 이러한 특성을 가지면서 루비와 같이 가독성이 뛰어난 대표적인 스크립트 언어는 파이썬이다. 이런 유사함은 각각의 언어 사용자 간에 '어떤 언어가 더 뛰어난가?' 라는 논쟁을 일으켰다. 그러나 그런 논쟁은 대체적으로 기술적으로 너무 세부적인 곳에 집착한 의미 없는 논쟁이었다.

파이썬이 정형화된 들여쓰기를 요구하는 반면 루비는 정형화된 서식을 요구하지는 않는다.

사용자 수와 구현 시스템의 수와 질 등을 비교해 보면, 세계적으로 파이썬이 인기가 더 많다. 한편, 루비의 개발자가 일본 사람이기 때문에 일본에서는 루비의 인기가 높고 서적 등도 많이 출판되고 있다. 2004년까지는 루비로 작성된 킬러 애플리케이션이 없었다. 하지만, 2004년 말에 발표된 루비 온 레일즈가 2005년에 폭발적인 인기를 모으면서 루비는 큰 주목을 받게 되었다.

출처 : [루비 (프로그래밍 언어) - 위키백과, 우리 모두의 백과사전](https://ko.wikipedia.org/wiki/%EB%A3%A8%EB%B9%84_(%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D_%EC%96%B8%EC%96%B4)#%ED%8C%8C%EC%9D%B4%EC%8D%AC%EA%B3%BC%EC%9D%98_%EB%B9%84%EA%B5%90) 
설치하기


1. 루비
Install Jekyll on Windows 10
지킬은 유닉스(Unix), 리눅스(Linux), 맥(OS X)을 지원한다고 나와 있습니다.
윈도우는 빠져있죠. 그래서 윈도우에 지킬을 설치해 보도록 하겠습니다.
설치는 Ruby 그리고 Ruby DevKit으로 충분합니다.

1) 윈도우
루비를 설치한다.
 
1. Ruby+Devkit 2.4.4-2 (x64) 를 다음의 사이트에서 다운로드 받아 설치합니다. https://rubyinstaller.org/downloads/ 

1-1. 중간에 ‘PATH에 추가하시겠습니까?’ 부분은 반드시 체크해 주시기 바랍니다.

2. Devkit을 설치합니다.

 2-1. 다운로드 사이트에서 아래로 내려오면 DevKit-mingw64-64-4.7.2-20130224-1432-sfx.exe이 있습니다.
본인의 윈도우 환경에 맞는 파일을 받는다. 

 2-2. 실행하면 어디에 압축을 풀지 물어봅니다. C:\devkit 에 풀어줍니다.
 
3. jekyll 및 부가기능 설치하기 

3-1. 윈도우 + R을 눌러 실행을 연 다음 cmd를 입력하고 확인을 누릅니다. 

3-2. cd C:\devkit으로 devkit 폴더로 이동해줍니다. 

3-3. ruby dk.rb init 

3-4. ruby dk.rb install ruby devkit을 설치해주세요.

3-5. 이제 준비과정이 끝났습니다. jekyll을 설치해보겠습니다. 
```cd c:\ ```
```mkdir jekyll_test  ```
```cd jekyll_test```
```gem install jekyll```

3-6. 무언가 쭉 뜨면서 설치가 진행됩니다.
 
3-7.``` jekyll new . ```로 새로운 사이트를 생성해 봅니다.
 
```jekyll serve --watch```로 서버를 확인해봅니다. 
 
3-8. 웹브라우저를 하나 실행하여 주소창에 127.0.0.1:4000을 입력해줍니다.

4. 블로그 완성! 


## 루비 설치이후 블로그 제작까지 : 맥과 윈도우 사용자 공통. 

Github에 블로그 만들기 (by Jekyll)
Jekyll(이하 지킬)을 통해 Github에 정적 블로그(HTML 웹사이트)를 만들어보자. 지킬은 루비 스크립트로 만들어져 있으나, 블로그를 만드는데에 있어 루비를 알 필요는 없다. 다음 과정은 Mac OS를 기준으로 진행된다.

지킬 설치
```Mac OS는 루비가 이미 설치되어 있다.```


# ruby 버전 확인

```ruby -v```
지킬 설치를 위해 Xcode의 설치가 필요하다. (이미 설치되어 있다면 생략)

# Xcode 설치
```xcode-select --install```
지킬을 설치한다.
이 과정에서 permission error가 발생하면 sudo를 앞에 붙여 입력한다.

# jekyll 설치
```gem install jekyll```
새로운 페이지 생성하기
(주의) 페이지 생성시에 주소는 반드시 나의깃허브아이디.github.com 이어야 한다.

- 계정 주소에 알맞는 페이지를 생성한다.
다음 입력을 통해 나의깃허브아이디.github.com 디렉토리가 만들어진다.

jekyll new 나의깃허브아이디.github.com
 디렉토리로 이동한다

cd ~/나의깃허브아이디.github.com
- 서버를 구동시킨다.
만약 could not locate Gemfile 과 같은 Gemfile Error가 발생하면 (sudo) bundle install 입력하여 bundler을 install하고 bundle로 서버를 구동시켜준다.

# 테마 설치를 한번도 안했을 때
```jekyll serve --watch```
# 테마 설치를 해봤을 때
```bundle exec jekyll serve```
- 서버에서 페이지가 제대로 구동되는지 확인한다.
웹브라우저 주소창에 localhost:4000 을 입력해보면 디폴트로 생성된 블로그를 볼 수 있다.



# 내 깃허브에 연동시키기
(주의) repository 생성시에 주소는 반드시 나의깃허브아이디.github.com 이어야 한다.

깃허브에서 나의깃허브아이디.github.com 이라는 이름으로 New repository를 생성한다.


1. repository URL을 복사한다.!



- 터미널로 돌아가서, repository를 연결하고 push 해준다.
터미널에서 현재 위치는 ~/나의깃허브아이디.github.com 이여야 한다.


# connect repository
```
git init
git remote add origin *복사한 repository URL*
git remote -v
```

# commit and push
```
git add .
git commit -m "Create blog"
git push -u origin master
```


- 깃허브에서 commit 이 잘 되었는지 확인하고 블로그 생성을 확인한다.
나의깃허브아이디.github.io 에서 내 블로그를 볼 수 있다. 연동에는 5분 이상의 시간이 걸릴 수 있다. (조금 기다려보자 꼭!!!!!)

# 지킬 테마 설정하기
테마를 사용하기 위해서는 bundler 의 설치가 필요하다. 테마는 다음 사이트에서 선택할 수 있다.

Jekyll Themes : http://jekyllthemes.org

bundler를 설치한다.

```gem install bundler```
내가 원하는 테마를 사이트에서 고르고 파일을 다운로드 한다.



- 압축된 파일을 풀고, 내 나의깃허브아이디.github.com 디렉토리에 모두 붙여넣는다.
- 테마를 여러번 바꾸다 보면 실수로 불필요한 파일이 남거나 덮어씌어지지 않을 수 있으니, 디렉토리를 비우고 붙여넣는 것을 추천한다.

- 터미널로 돌아가서 빌드를 진행한다.
터미널에서 현재 위치는 ~/나의깃허브아이디.github.com 이여야 한다.

# 둘 중 하나를 이용
```bundle exec jekyll serve```
```jekyll serve```


(참고 1) 만약 could not locate Gemfile 과 같은 Gemfile Error가 발생하면 (sudo) bundle install 를 입력하여 bundler을 install하고 bundle로 서버를 구동시켜준다.

(참고 2) 루비의 버전이 문제라면 bundle update 를 입력하여 업데이트 해주면 된다.

- 서버에서 페이지가 제대로 구동되는지 확인한다.
웹브라우저 주소창에 ```localhost:4000``` 을 입력해보면 테마가 바뀐 블로그를 볼 수 있다.



(참고)``` localhost:4000``` 을 입력했는데 404 와 같이 빈 창이 나온다면,``` _config.yml ```파일을 확인해봐야 한다.



여기서 baseurl이 ““로 비어있지 않다면 쌍따옴표 사이를 비우고 저장한 후 다시 빌드하면 된다. 혹은 “/blog”라고 되어 있다면 localhost:4000/blog 라고 주소를 입력해보면 정상적으로 볼 수 있다.

터미널로 돌아가서 내 repository로 테마 파일을 푸시해준다.
터미널에서 현재 위치는 ~/나의깃허브아이디.github.com 이여야 한다.

# commit and push
```
git add .
git commit -m "Change Theme"
git push -u origin master
```
- 깃허브에서 commit 이 잘 되었는지 확인하고 블로그 생성을 확인한다.
나의깃허브아이디.github.io 에서 내 블로그를 볼 수 있다. 연동에는 5분 이상의 시간이 걸릴 수 있다. *(조금 기다려보자 꼭!!!!!222)

- 테마 내 것으로 만들기
블로그에 테마 설정까지 끝났다면, 세부 사항을 내 것으로 업데이트 해주어야 한다. README.md 파일을 참고하면 된다. ```_config.yml ```파일에서 블로그의 타이틀 등을 변경할 수 있고, 이미지 파일 변경을 통해 프로필 사진도 등록할 수 있다!


# 깃허브에서 지킬 테마 적용하여 블로그생성. 

- Jekyll 테마 포크해오기(Jekyll Themes 사이트에서 Homepage 버튼->Fork)
- 포크해온 테마(레파지토리)에 gh-pages 브랜치 생성
- Settings-Github pages에서 Sourse 를 gh-pages 브랜치로 설정
- 내 블로그 레파지토리를 삭제하고 포크해온 테마의 주소를 https://내깃헙아이디.github.io 로 바꾸면 블로그에 테마 적용
- ```_config.yml``` 파일에서 블로그의 타이틀 등을 변경할 수 있고, 이미지 파일 변경을 통해 프로필 사진도 등록할 수 있다.

#### Kaggle 소개

 - Kaggle : 개발자에게 GitHub이 있다면 데이터 사이언티스트에게는 Kaggle이 있음

 - Titanic : Kaggle 입문용 경진대회. 타이타닉호 생존여부 통계 분석.

 - Kaggle Tutorial, Kernel을 참조해서 데이터 분석 방법을 익히자.

 - 1일 1 Commit 할 소재가 없다면 Kaggle Competition의 다른 사람 것을 따라해보자.

 - 캐글러의 관심사는 무엇일까?

   - Kaggle Survey 2017 결과를 파이썬으로 분석한 커널 확인

     ~~~
     Survey : https://www.kaggle.com/kaggle/kaggle-survey-2017
     Survey Kernel : https://www.kaggle.com/ash316/novice-to-grandmaster
     Python 분석 : https://colab.research.google.com/drive/10SuqOyUNbDDlYOQQqueMTlkNqrX7BjlS
     ~~~

   - 앞으로 크게 주목받을 것은? TensorFlow. Deep Learning.

   - 데이터 사이언스를 어디서 공부하는가? Kaggle. 온라인 강의. Stack Overflow 등.

   - 어떻게 학습하는 것이 유용한가? Project. 코스 수강. Stack Overflow. Kaggle 등.

   - 좋은 컴퓨터가 필요한가? 그렇지는 않음. 딥러닝은 Cloud service 사용하면 됨.

   - 블로그 / 팟캐스트 추천 : KDnuggets Blog. Becoming a Data Scientist. Siraj Raval.

   - 인터넷 강의 사이트 추천 : Coursera, Udacity, Edwith(Coursera Machine Learning 분석 중!)

   - 어떤 기술이 필요할까? 파이썬. 통계 지식. 시각화. SQL.

   - Data Science로 Job을 구할 때 고려 요소는? 배울수 있는 직장인지, 사용하는 언어가 무엇인지 등.

   - Job을 구할 때 필요 요소는? 관련 직무 경험, Kaggle 참여 경험, GitHub 포트폴리오 등.

 - 참고

~~~
- 지도학습 : 특정 상황별로 결과값이 분류된 데이터를 가지고 진행하는 방법
- 비지도학습 : 분류되지 않은 데이터를 가지고 진행. 클러스터링 등을 통해 직접 분류해야 함.
~~~

~~~
- [2017 캐글 설문조사 분석](https://colab.research.google.com/drive/10SuqOyUNbDDlYOQQqueMTlkNqrX7BjlS#scrollTo=01yrTtpiUMWl)
- 캐글을 통해 관심있는 데이터셋을 보고 직접 분석해보거나 따라해보는 것이 도움됨!
~~~


