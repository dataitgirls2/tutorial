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

