
## 프로젝트 설정하기 

1. 적당한 위치에 프로젝트 폴더 만들기-조건

   ●    프로젝트 관련 폴더를 생성하여 관리하는 것이 좋음

   ●    공백, 특수문자, 한글 사용하지 않기

   ●    영문자 소문자, 숫자, 하이픈(-), 언더바(_)만 쓰기

   ●    좋은 예시:

   ​	○    C:\Users\aeran\projects\slackbot

   ​	○    C:\Users\aeran\projects\slack-bot

   ●    나쁜 예시:

   ​	○    C:\Users\aeran\projects\slack bot (띄어쓰기)

   ​	○    C:\Users\aeran\projects\슬랙봇 (한글)

   

2. 아나콘다 프롬프트 실행 후 프로젝트 폴더로 이동

   ```cd C:\Users\aeran\projects\slackbot```

   * 원하는 위치로 이동 → ```cd 위치 ```

   * 현재 디렉토리 확인 → ```pwd```

     

3. 프로젝트 위한 가상환경 만들기

   * 한 대의 컴퓨터에서 여러 프로젝트를 동시에 진행하면, 각 프로젝트별 설치가 필요한 라이브러리가 모두 다르고 각 라이브러리 사이에 충돌이 있을 수 있음

   * 각 프로젝트별 격리된 환경 필요 → **가상환경 만들기**

     1) 컴퓨터에 아나콘다 설치 후,**<u>Anaconda Prompt</u>**에서 ```pip install pipenv``` 실행 

     2) **프로젝트 디렉토리 생성 → 디렉토리 이동 후** ```pipenv --python=3.6``` 으로 가상환경 만들어주기

     참고) 다른 사람의 프로젝트를 복제해서 시작할때는 **git clone → 프로젝트 디렉토리로 이동** **→** ```pipenv install``` 로 가상환경 생성 





## 슬랙봇 뼈대 만들기
#### 슬랙봇 기초 만들기
1. https://api.slack.com 로 이동하기
2. Start Building > App Name 설정, Development Slack Workspace에 dataitgirls2018 선택하여 앱 생성해주기
3. Anaconda Prompt(MAC은 그냥 git에서 해도 됨)에서 다음 명령어 입력
```
$ pipenv install rtmbot
```
rtmbot을 깔아주는 작업 실행! (real time bot이라고 이미 누군가가 만들어 놓은 실시간 봇)
4. `main.py` 파일에 다음 코드를 입력하기
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
5. https://api.slack.com 접속 > 우상단 your apps > Install App에 Bot User OAuth Acceess Token 을 복사
6. SLACK_TOKEN 부분에 복사한 키 붙여넣기

#### 슬랙봇 실행시키고 끄기 (Anaconda Prompt에서 작업)
* 봇 실행시키기 : `$ pipenv run python main.py~ 
* 봇 끄기: `crtl + c`

#### 
다음 코드를 `main.py`의 3번째줄에 추가하기
```
class HelloPlugin(Plugin):
    def process_message(self, data):
        if "애란" in data["text"]:
        self.outputs.append([data["channel"], "불렀어?"])
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
