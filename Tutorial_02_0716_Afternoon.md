## 마크업 언어

마크업 언어란:

태그 등을 이용하여 문서나 데이터의 구조를 명기하는 언어를 지칭한다. (위키백과 출처)

대표적인 예시로는 **마크다운**과 **HTML**이 있다.

(마크다운은 가볍다고 해서 마크'업'을 '다운'으로 바꾼 이름이라고 한다.)

<https://caniuse.com/>

위는 브라우저마다 무엇을 지원하고 있는지 한 눈에 알 수 있는 사이트.



### 실습

다음 기사에 제목, 발행일, 기자, 신문사, 인용 등 문서의 구조와 정보의 성격을 나타내는 정보를 넣기 위해 필요한 마크업 언어를 고안하고 문서에 적용하세요. (기사 출처: 허핑턴포스트 코리아)



~~~
'돌아온' 오늘 MBC 뉴스의 첫 앵커 멘트는 '사과'였다

2017년 12월 08일 15시 27분, 허완 기자, 허핑턴포스트코리아

“저희 MBC는 신임 최승호 사장의 취임에 맞춰, 오늘(8일)부터 뉴스데스크 앵커를 교체하고 당분간 뉴스를 임시체제로 진행합니다. 저희들은 재정비 기간 동안 MBC 보도가 시청자 여러분께 남긴 상처들을 거듭 되새기며, 철저히 반성하는 시간을 갖겠습니다. 치밀한 준비를 거쳐 빠른 시일 안에 정확하고 겸손하고 따뜻한 뉴스데스크로 시청자 여러분께 다시 인사드리겠습니다.”

8일 저녁 8시, MBC 메인뉴스인 '뉴스데스크' 대신 'MBC뉴스'라는 타이틀로 방송된 뉴스에서 임시 앵커를 맡은 김수지 아나운서는 짤막한 사과문을 읽어내려갔다.
~~~



**예시들**

~~~
@제목: '돌아온' 오늘 MBC 뉴스의 첫 앵커 멘트는 '사과'였다

@시간: 2017년 12월 08일 15시 27분, @기자: 허완 기자, @신문사: 허핑턴포스트코리아

@서론: “저희 MBC는 신임 최승호 사장(csh@mbc.com)의 취임에 맞춰, 오늘(8일)부터 뉴스데스크 앵커를 교체하고 당분간 뉴스를 임시체제로 진행합니다. 저희들은 재정비 기간 동안 MBC 보도가 시청자 여러분께 남긴 상처들을 거듭 되새기며, 철저히 반성하는 시간을 갖겠습니다. 치밀한 준비를 거쳐 빠른 시일 안에 정확하고 겸손하고 따뜻한 뉴스데스크로 시청자 여러분께 다시 인사드리겠습니다.”

@본론: 8일 저녁 8시, MBC 메인뉴스인 '뉴스데스크' 대신 'MBC뉴스'라는 타이틀로 방송된 뉴스에서 임시 앵커를 맡은 김수지 아나운서는 짤막한 사과문을 읽어내려갔다.

~~~

위의 예시는 @를 이용해 태그를 달았다. 이런 경우 만약 본문에 @가 들어가는 내용이 나온다면 (최승호 사장 뒤의 이메일 주소처럼) 출력 과정에서 혼란이 발생할 수 있다. 



~~~
$ 기사제목 : 돌아온' 오늘 MBC 뉴스의 첫 앵커 멘트는 '사과'였다

$ 게시날짜 : 2017년 12월 08일 15시 27분

$ 게시자 : 허완 기자 

$ 발행기관 : 허핑턴포스트코리아

$ 기사내용/인용문 : “저희 MBC는 신임 최승호 사장의 취임에 맞춰, 오늘(8일)부터 뉴스데스크 앵커를 교체하고 당분간 뉴스를 임시체제로 진행합니다. 저희들은 재정비 기간 동안 MBC 보도가 시청자 여러분께 남긴 상처들을 거듭 되새기며, 철저히 반성하는 시간을 갖고 $ 5,000을 보상하겠습니다. 겠습니다. 치밀한 준비를 거쳐 빠른 시일 안에 정확하고 겸손하고 따뜻한 뉴스데스크로 시청자 여러분께 다시 인사드리겠습니다.”

$ 기사내용 /본문: 8일 저녁 8시, MBC 메인뉴스인 '뉴스데스크' 대신 'MBC뉴스'라는 타이틀로 방송된 뉴스에서 임시 앵커를 맡은 김수지 아나운서는 짤막한 사과문을 읽어내려갔다.

~~~

이 또한 마찬가지로 돈을 표시하기 위해 본문에서 $를 사용한다면 문제가 발생할 수 있다. 



~~~
[제목:
'돌아온' 오늘 MBC 뉴스의 첫 앵커 멘트는 '사과'였다
]
[+:]
[날짜:
2017년 12월 08일 15시 27분
]
[+:]
[작성자:
허완 기자
]
[+:]
[매체:
허핑턴포스트코리아
]
[+:]
[인용:
“저희 MBC는 신임 최승호 사장의 취임에 맞춰, 오늘(8일)부터 뉴스데스크 앵커를 교체하고 당분간 뉴스를 임시체제로 진행합니다. 저희들은 재정비 기간 동안 MBC 보도가 시청자 여러분께 남긴 상처들을 거듭 되새기며, 철저히 반성하는 시간을 갖겠습니다. 치밀한 준비를 거쳐 빠른 시일 안에 정확하고 겸손하고 따뜻한 뉴스데스크로 시청자 여러분께 다시 인사드리겠습니다.”
]
[+:]
8일 저녁 8시, MBC 메인뉴스인 '뉴스데스크' 대신 'MBC뉴스'라는 타이틀로 방송된 뉴스에서 임시 앵커를 맡은 김수지 아나운서는 짤막한 사과문을 읽어내려갔다.

~~~

이 예시의 경우 태그를 열고 닫는 과정이 있다. 



이처럼 마크업 언어는 본문과 태그, 즉 이것이 어떤 내용인지를 안내하는 코드는 본문과 확실히 구분될 수 있어야 한다. 그런 이유로 html은 항상 여는 태그와 닫는 태그가 존재한다. 이 실습은 이를 알아보기 위한 실습이었다. 





## 파이썬으로 크롤링 하기



#### 1. HTML 받아오기 (request)

python 표준 라이브러리 중 urllib 패키지의 request 모듈을 이용하여 웹 사이트의 콘텐츠를 받아올 수 있습니다.  네이버의 HTML을 받아와 보겠습니다. 

```python
from urllib import request

url = "https://www.naver.com"

# urlopen 함수의 결과를 f에 담기
with request.urlopen(url) as f:
    # 읽어온 결과를 utf-8로 인코딩
    html = f.read().decode('utf-8')
    # html 변수의 앞/끝 16글자씩 출력하기
    print(html[:16], html[-16:])
```

위의 코드를 실행하면 아래의 결과를 볼 수 있습니다. 

> <!doctype html> 
>
> </body> 
>
> </html> 



#### 2. HTML DOM 트리 구성하기 (html5lib) 

위의 코드에서 html이라는 변수에 담긴 문자열을 분석하여 트리 구조로 만들면 원하는 내용을 쉽게 추출할 수 있습니다. html5lib는 HTML 문서를 트리구조로 분석해주는 라이브러리입니다. 

```python
# html5lib는 표준라이브러리가 아니기 때문에 설치 필요
!pip install html5lib

from urllib import request
import html5lib

url = "https://www.naver.com"
with request.urlopen(url) as f:
  html = f.read().decode('utf-8')

# html 변수에 담긴 HTML 문서를 분석(parse)하여 DOM 트리를 만들기
# 그 결과를 dom 변수에 담기
dom = html5lib.parse(html)

# dom 변수의 자식 엘리먼트 구하기
children = dom.getchildren()
```

위의 코드의 실행 결과는 아래와 같습니다. 

> [<Element '{http://www.w3.org/1999/xhtml}head' at 0x7fddc36f7d18>,
>  <Element '{http://www.w3.org/1999/xhtml}body' at 0x7fddc3710228>] 



dom은 head와 body라는 Element를 자식으로 가지고 있습니다. HTML 표준에 의하면 head 엘리먼트는 title이라는 자식 엘리먼트를 가지고 있습니다. 이 타이틀 태그를 추출해 봅시다. 먼저 head의 자식들이 어떻게 생겼는지 봅니다. 

```python
head = children[0]
head_children = head.getchildren()

for e in head_children:
  print(e)
```

> <Element '{[http://www.w3.org/1999/xhtml}meta'](http://www.w3.org/1999/xhtml%7Dmeta') at 0x7fd040e4b728> <Element '{[http://www.w3.org/1999/xhtml}meta'](http://www.w3.org/1999/xhtml%7Dmeta') at 0x7fd040e4b7c8> <Element '{[http://www.w3.org/1999/xhtml}title'](http://www.w3.org/1999/xhtml%7Dtitle') at 0x7fd040e4b9f8> <Element '{[http://www.w3.org/1999/xhtml}script'](http://www.w3.org/1999/xhtml%7Dscript') at 0x7fd040e4bae8> <Element '{[http://www.w3.org/1999/xhtml}style'](http://www.w3.org/1999/xhtml%7Dstyle') at 0x7fd040e4bc78> <Element '{[http://www.w3.org/1999/xhtml}link'](http://www.w3.org/1999/xhtml%7Dlink') at 0x7fd040e4bea8> 

head는 meta, title, script, style, link와 같은 자식들을 가지고 있음을 알 수 있습니다. 이제 원하는 자식의 이름은 엘리먼트의 끝의 글자라는 것을 알게 되었습니다. title로 끝나는 자식의 ``text``를 출력하는 ``get_title`` 함수를 만들어 보겠습니다.

```python
def get_title(head):
  # head의 자식들을 돌면서
  for x in range(len(head)):
    # 자식이 'title'로 끝나는지 확인
    val = head_children[x].tag.endswith('title')
    # 만약 자식이 'title'로 끝난다면
    if val:
      # 자식의 text 요소를 가지고 와서 출력
      title = head_children[x].text
      print(title)
    
get_title(head)
```

> Naver



## 참고자료

[애란쌤의 수업자료](https://colab.research.google.com/drive/1zQbsUgsV3ZlV7W49IapnQIJz_sGkXrXU#scrollTo=FDZksPm-jHkr)

