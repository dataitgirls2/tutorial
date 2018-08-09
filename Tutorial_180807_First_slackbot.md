
## 프로젝트 설정하기 

## 슬랙봇 뼈대 만들기
#### 슬랙봇 기초 만들기
1. https://api.slack.com 로 이동하기
2. `Start Building` > `App Name` 설정, `Development Slack Workspace`에 dataitgirls2018 선택하여 앱 생성해주기
3. https://daitgirls.slack.com/messages/CC2DJPQ01/ 에서 왼쪽상단 사람모양 클릭 > `invite more people`클릭 > 자신의 봇이름 검색해서 추가해주기
4. Anaconda Prompt(MAC은 그냥 git에서 해도 됨)에서 다음 명령어 입력
```
$ pipenv install rtmbot
```
rtmbot을 깔아주는 작업 실행! (real time bot이라고 이미 누군가가 만들어 놓은 실시간 봇)

5. `main.py` 파일에 다음 코드를 입력하기
```
from rtmbot import RtmBot

config = {
    "SLACK_TOKEN": "xoxb-...",
    "ACTIVE_PLUGINS": []
}
# 봇이 작동하기 위한 코딩들이 딕셔너리 형태로 들어있음. 봇이 내부에서 정보를 연결해서 슬랙에 연결됨.

bot = RtmBot(config)
bot.start()
```
6. https://api.slack.com 접속 > 우상단 your apps > Install App에 Bot User OAuth Acceess Token 을 복사
7. SLACK_TOKEN 부분에 복사한 키 붙여넣기

#### 슬랙봇 실행시키고 끄기 (Anaconda Prompt에서 작업)
* 봇 실행시키기 : `$ pipenv run python main.py`
* 봇 끄기: `crtl + c`

-> 봇 실행을 시켜서 봇에 불이 들어오는지 확인해 주세요!!

#### 채팅방에서 특정 단어를 포함하는 챗이 올라왔을때, 슬랙봇이 반응하도록 하기
다음 코드를 `main.py`의 3번째줄에 추가하기
```
class HelloPlugin(Plugin):
    def process_message(self, data):
        if "애란" in data["text"]:  # 채팅창에서 '애란'을 포함하는 채팅이 있으면
        self.outputs.append([data["channel"], "불렀어?"])  # 불렀어? 라고 응답해주기
```

따라서 `main.py`는 다음과 같은 코드가 되어야 한다.
```
from rtmbot import RtmBot
from rtmbot.core import Plugin


class HelloPlugin(Plugin):
    def process_message(self, data):
      if "애란" in data["text"]:
        self.outputs.append([data["channel"], "불렀어?"])


config = {
    "SLACK_TOKEN": "xoxb-411114726947-412995853687-B2xV60txIzYNNge7pRDXo6PR",
    "ACTIVE_PLUGINS": ["main.HelloPlugin"]
}
bot = RtmBot(config)
bot.start()
```



## 깃헙에 올릴 준비

### 챗봇 깃에 올려보기 ( git ignore 해서 )

- Piffle, pipfile.lock : pipenv의 버전 정보(=개발 환경 정보)의 전달/공유를 위해 GitHub 업로드 필요 

  - `pipfile` 과 `pipfile.lock` 은 항상 버전 관리를 해서 다른 개발자가 클론해갔을 때 나와 똑같은 환경에서 사용할 수 있다. 따라서 이 2개의 파일도 깃허브에 올립니다.

  ```
  git add pip* (pip으로 시작하는 거는 모두 에드하겠다는 뜻 )
  ```

  

- ` SLACK_TOKEN` 으로 챗봇의 토큰을 저장하는 변수를 만듭니다. 
  - slack API의 비밀번호(=OAut Token)에 해당하는 부분 : GitHub에 업로드 금지
  - 별도의 파일(secret.py)로 분리해서 해당 파일은 GitHub에 올리지 않도록 합니다.

  1.  새파일 만들어서 secret.py 이름으로 저장합니다. 
  2.  slack token을  secret.py 에 복사해서 저장합니다.
  3.  Slack token을 import 해준다. 

  

  Import 해주는 방법은 아래의 2개 중에 하나를 사용합니다.
  ~~~
  from secret import SLACK_TOKEN 
  
  import secret 
  => 호출 시에 secret.SLACK_TOKEN 
  ~~~

  

- 깃허브에 업로드 시 `.git ingnore` 파일을 새로 만들어서 업로드 되면 안되는 것들(rtmbot.log, secret.py) 을 등록 해줍니다. 

  - 다른 개발자도 무시할 수 있도록 gitignore도 함께 깃허브에 올려줍니다. 

  ~~~
  git add .gitignore 
  ~~~



올릴 내용이 모두 add 되었으면 commit 하고 push해서 해당 저장소로 업로드합니다. 
