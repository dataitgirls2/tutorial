
## 프로젝트 설정하기 

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
