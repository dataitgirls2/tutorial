# 크롤링 3 

## Beautiful Soup 

* 왜 Beautiful Soup를 사용하는가?
  * 매번 웹사이트를 방문해서 데이터를 수집하고, html5lib를 사용해서 크롤링을 해왔는데, html5lib가 나무구조여서 차원이 너무 많아서 원하는 요소를 뽑아오기 쉽지 않았다.
  * Beautiful Soup를 사용하면 원하는 요소를 쉽게 가져올 수 있다.



### 기존 html5lib을 사용해서 Naver의 title 가져오기

```
from urllib import request
import html5lib

url = "https://www.naver.com"
with request.urlopen(url) as f:
  html = f.read().decode('utf-8')

dom = html5lib.parse(html)
head = dom.getchildren()[0]
titles = [
  child for child in head.getchildren()
  if child.tag == '{http://www.w3.org/1999/xhtml}title'
]
title = titles[0].text
print(title)
```

```
>> Naver
```



### Beautiful Soup를 사용해서 Naver의 title 가져오기

```
from urllib import request
from bs4 import BeautifulSoup

url = "https://www.naver.com"
with request.urlopen(url) as f:
  html = f.read().decode('utf-8')

bs = BeautifulSoup(html, 'html5lib')  # html5를 사용해서 dom을 알아서 만들어준다.
# select()를 사용하면 모든 결과를 리스트에 담고, select_one()을 사용하면 하나의 요소만 반환
title = bs.select_one('title').text  # selec_one()안에 인자는 태그이름이 아니라 css 문법이다.
print(title)
```

```
>> NAVER
```

: 훨씬 더 쉽게 웹사이트의 타이틀을 가지고 올 수 있다!





## CSS (**Cascading Style Sheets**)

* 정의
  * 마크업 언어가 웹사이트의 몸체를 담당한다면, CSS는 옷과 액세서리와 같은 꾸미는 역할을 담당한다고 할 수 있다.

## CSS 문법

- 클래스찾기 `.class`

  ```
  .classname {}
  ```



- id찾기 `#id`

  ```
  #idname {}
  ```



- 자식 selector `>`

  ```
  body > .highlight {}  
  ```

  - body의 바로 밑에 자식(직계자식) 중 highlight 클래스인것
  - body의 자식의 자식중 hightlight 클래스인것은 해당 안됨





### 애란이네 책방 실습

```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>애란이네</title>
    <style>
    x {
      background: #AFA;
      outline: 1px solid black;
    }
    </style>
  </head>
  <body>
    <h1>애란이네 책방</h1>
    <p id="welcome">애란이네 책방에 오신 것을 환영합니다.</p>
    <p class="highlight">마음껏 구경하세요.</p>
    <ul class="category">
      <li>소설</li>
      <li class="highlight">만화</li>
      <li>역사</li>
    </ul>
  </body>
</html>
```



**x부분을 다음과 같이 바꿔주세요!**

* highlight 클래스로 바꾸기

  ```
  .highlight {}
  ```

  ```
  >> '마음껏 구경하세요', '만화' >> background 색이 바뀐다.
  ```



- welcome 아이디로 바꾸기

  ```
  #welcome {}
  ```

  ```
  >> '애란이네 책방에 오신 것을 환영합니다.' >> background 색이 바뀐다.
  ```

  

- ul 혹은 ul의 자식이면서 hightlight 클래스인것

  ```
  ul .highlight {}
  ```

  ```
  >> '만화' >> background 색이 바뀐다.
  ```

  

- ul중에 highlight 클래스인것

  ```
  ul.highlight {}
  ```

  ```
  >> 아무것도 변하지 않음. 
  ```

  * 태그이름이 ul 이면서 highlight 클래스인 Element가 없어서



- ul 혹은 ul의 자식중 li 이면서 highlight 클래스인것

  ```
  ul li.highlight {}
  ```

  ```
  >> '만화' >> background 색이 변한다.
  ```

  * 공백이 없으면 해당 element들 중 해당 속성들
  * 공백이 있으면 본인과 자식을 포함하는 element들 중 해당 속성들을 불러옴



- body 의 직계자손의 하위항목 중에서 highlight 클래스인 Element

  ```
  body > .highlight {}  
  ```

  ```
  >> '마음껏 구경하세요' >> background 색이 변한다.
  ```

## yes24 파이썬 검색결과 목록 추출하기

### robots.txt 확인
[robots.txt](http://www.yes24.co.kr/robots.txt)
~~~
User-agent: *
Disallow: /templates/
Disallow: /member/
Allow: /
~~~
templates와 member 데이터만 건들지 않으면(그리고 과도한 트래픽을 유발하지 않는다면) 데이터를 수집해도 괜찮은 것 같습니다.

### 필요한 패키지  import
- html5lib: 엉망으로 만들어진 HTML 문서도 적절히 잘 분석해서 DOM 구조로 만들어줌.
- beautifulsoup4: SS Selector를 이용하여 DOM 구조에서 원하는 엘리먼트들을 뽑아내는 기능을 제공


```
# html5lib와 beautifulsoup4를 설치하는 명령어(혹시 안 깔려 있을 때 대비):
# !pip install html5lib beautifulsoup4

from urllib import request
from bs4 import BeautifulSoup
import pandas as pd
```

### HTML 받아오기
- 예스24 서버로 HTTP 요청을 보내서 HTML을 받아온 후 파이썬 문자열(str)로 변환해보겠습니다.


```
url = "http://www.yes24.com/searchcorner/Search?keywordAd=&keyword=&domain=BOOK&qdomain=%B1%B9%B3%BB%B5%B5%BC%AD&query=%C6%C4%C0%CC%BD%E3"
with request.urlopen(url) as f:
  html = f.read().decode('utf-8')
```


    ---------------------------------------------------------------------------

    UnicodeDecodeError                        Traceback (most recent call last)

    <ipython-input-16-8e12c9cf7762> in <module>()
          1 url = "http://www.yes24.com/searchcorner/Search?keywordAd=&keyword=&domain=BOOK&qdomain=%B1%B9%B3%BB%B5%B5%BC%AD&query=%C6%C4%C0%CC%BD%E3"
          2 with request.urlopen(url) as f:
    ----> 3   html = f.read().decode('utf-8')
    

    UnicodeDecodeError: 'utf-8' codec can't decode byte 0xb4 in position 241: invalid start byte


#### DON'T PANIC
####왜 오류가 발생했을까?
- 소스 코드를 살펴보니 아래와 같은 부분이 있습니다.
~~~html
<meta http-equiv="Content-Type" content="text/html;charset=euc-kr" />
~~~
- utf-8이 아닌 **euc-kr**을 써야합니다. euc-kr은 오래 전에 한국에서만 쓰이던 낡은 방식이지만 불행히도 아직도 상당수 한국 웹사이트에서 이 방식을 사용합니다.


```
url = "http://www.yes24.com/searchcorner/Search?keywordAd=&keyword=&domain=BOOK&qdomain=%B1%B9%B3%BB%B5%B5%BC%AD&query=%C6%C4%C0%CC%BD%E3"
with request.urlopen(url) as f:
  html = f.read().decode('euc-kr')
```

- 사이트에 따라 utf-8 또는 euc-kr로 코드를 바꿔주는 반복 작업을 하고 싶지 않습니다. (애란쌤이)구글 검색을 해보니 이렇게 쓰면 된다고 합니다.


```
url = "http://www.yes24.com/searchcorner/Search?keywordAd=&keyword=&domain=BOOK&qdomain=%B1%B9%B3%BB%B5%B5%BC%AD&query=%C6%C4%C0%CC%BD%E3"
with request.urlopen(url) as f:
  charset = f.headers.get_content_charset()
  html = f.read().decode(charset)
```

### HTML 문자열을 분석하여 DOM 구성하기
- html5lib를 이용하여 DOM을 구성한 후 DOM 트리 구조를 탐색하여 원하는 정보를 추출하는 코드를 만들어도 되지만 번거롭습니다.
- beautifulsoup을 이용하면 CSS 셀렉터를 써서 원하는 정보를 쉽게 추출해낼 수 있습니다.

- beautifulsoup은 내부적으로 DOM 트리를 구성하는데, 이 때 어떤 분석기(parser)를 사용할지 지정해줄 수 있습니다. 우리는 html5lib를 쓰도록 하겠습니다.



```
soup = BeautifulSoup(html, 'html5lib')
```

- soup 객체에는 select_one() 함수와 select() 함수가 있습니다. 두 함수 모두 CSS 셀렉터로 원하는 엘리먼트를 찾아주는 기능을 한다는 점은 같지만  
 - select_one() 함수는: 처음으로 발견한 하나의 엘리먼트만 반환합니다 
 - select() 함수는 발견한 모든 엘리먼트를 리스트 형식으로 반환합니다.


```
print(len(soup.select_one('a')))
print(len(soup.select('a')))
print (soup.select("a")[0] == soup.select_one("a"))
```

    1
    659
    True
    

- 먼저 상품 리스트(div 태그, class는 goodsList) 안의 상품명만 추출해보겠습니다.


```
title_elem = soup.select('div.goodsList p.goods_name a strong')
titles = []

for i in title_elem:
  titles.append(i.text)
  
len(titles), titles
```




    (20,
     ['Do it! 점프 투 파이썬',
      '모두의 파이썬',
      '밑바닥부터 시작하는 딥러닝 ',
      '파이썬을 이용한 머신러닝, 딥러닝 실전 개발 입문',
      '파이썬과 케라스를 이용한 딥러닝/강화학습 주식투자',
      '모두의 알고리즘 with 파이썬',
      '파이썬 라이브러리를 활용한 머신러닝 ',
      '파이썬으로 데이터 주무르기',
      '파이썬 자연어 처리의 이론과 실제',
      '파이썬 GUI 프로그래밍 쿡북 2/e',
      '처음 시작하는 파이썬',
      'Hello Coding 한입에 쏙 파이썬',
      '초보자를 위한 파이썬 200제',
      '한 권으로 배우는 파이썬 기초 & 알고리즘 사고법',
      '파이썬과 케라스로 배우는 강화학습',
      '파이썬을 활용한 금융공학 레시피',
      '파이썬을 이용한 웹 크롤링과 스크레이핑',
      '파이썬 라이브러리를 활용한 데이터 분석',
      '파이썬으로 배우는 알고리즘 트레이딩',
      '블록과 함께 하는 파이썬 딥러닝 케라스'])



- 다음으로 상품 가격(할인이 적용된 가격)을 추출해보겠습니다.


```
price_elements = soup.select('div.goodsList p.goods_price strong')
prices = [i.text for i in price_elements]

len(prices), prices
```




    (20,
     ['16,920원',
      '10,800원',
      '21,600원',
      '27,000원',
      '22,500원',
      '14,400원',
      '27,000원',
      '24,750원',
      '31,500원',
      '31,500원',
      '27,000원',
      '13,500원',
      '18,000원',
      '27,000원',
      '24,300원',
      '25,200원',
      '27,000원',
      '29,700원',
      '36,000원',
      '22,500원'])



이런! 사람이 읽기 쉽도록 세 자리수마다 쉼표를 삽입한데다 가격 뒤에 '원'이 붙어있습니다. 또한 가격 데이터의 타입이 숫자(int)가 아니라 문자열입니다. 이대로라면 상품 가격을 통계적으로 분석하는 등, 크롤링한 데이터를 이후에 활용하는 데에 별도의 전처리 과정이 필요해 불편해질 것입니다.   
- 쉼표와 '원'을 제거하고, 데이터 타입을 int로 변환해줍시다.


- 코드 1과 2는 실질적으로 동일한 기능을 하며 동일한 결과물을 생성하나, 2가 보다 깔끔합니다.


```
# 코드 1
prices_tidy = []
for price in prices:
  price_nocomma = price.replace(',', '')
  price_nowon = price_nocomma[:-1]
  prices_tidy.append(price_nowon)
    
prices_tidy
```




    ['16920',
     '10800',
     '21600',
     '27000',
     '22500',
     '14400',
     '27000',
     '24750',
     '31500',
     '31500',
     '27000',
     '13500',
     '18000',
     '27000',
     '24300',
     '25200',
     '27000',
     '29700',
     '36000',
     '22500']




```
# 코드 2
prices_tidy = [int(i.replace(',', '')[:-1]) for i in prices]
prices_tidy
```




    [16920,
     10800,
     21600,
     27000,
     22500,
     14400,
     27000,
     24750,
     31500,
     31500,
     27000,
     13500,
     18000,
     27000,
     24300,
     25200,
     27000,
     29700,
     36000,
     22500]



- titles와 prices_tidy, 두 리스트로 데이터프레임을 만들어봅시다.


```
df = pd.DataFrame({"title":titles, "price":prices_tidy },
                  columns=['title', 'price' ])
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>title</th>
      <th>price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Do it! 점프 투 파이썬</td>
      <td>16920</td>
    </tr>
    <tr>
      <th>1</th>
      <td>모두의 파이썬</td>
      <td>10800</td>
    </tr>
    <tr>
      <th>2</th>
      <td>밑바닥부터 시작하는 딥러닝</td>
      <td>21600</td>
    </tr>
    <tr>
      <th>3</th>
      <td>파이썬을 이용한 머신러닝, 딥러닝 실전 개발 입문</td>
      <td>27000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>파이썬과 케라스를 이용한 딥러닝/강화학습 주식투자</td>
      <td>22500</td>
    </tr>
  </tbody>
</table>
</div>



- 수고하셨습니다!

## yes24 베스트셀러 목록 추출하기
수업에서는 yes24 '파이썬' 키워드 검색 결과창을 대상으로 실습을 했던 것 같은데, 수업자료와 애란쌤이 올려주신 콜랩 노트북에는 베스트셀러 페이지 목록 추출 실습으로 되어있어서 내용을 추가했습니다.  

사실 우리가 수업시간에 배우지 않은 내용이 있을 가능성이 있어 애란쌤이 올려주신 콜랩 노트북 내용을 그대로 복사해왔습니다.


```
# html5lib와 beautifulsoup4를 설치하는 명령어(혹시 안 깔려 있을 때 대비):
# !pip install html5lib beautifulsoup4

from urllib import request
from bs4 import BeautifulSoup
```


f12를 눌러 크롬의 개발자 도구를 통해 문서를 살펴보니 베스트셀러를 담고 있는 영역은 id가 "bestList"인 div 엘리먼트의 자식인 ol 엘리먼트입니다. ol 엘리먼트에 속한 li 엘리먼트 하나하나가 각 책에 대한 정보를 담고 있습니다. 따라서 아래와 같이 쓰면 책 40권에 해당하는 li 엘리먼트 40개가 나와야 합니다.


```
url = "http://www.yes24.com/24/category/bestseller"
with request.urlopen(url) as f:
  charset = f.headers.get_content_charset()
  html = f.read().decode(charset)
    
bs = BeautifulSoup(html, 'html5lib')
```


```
len(bs.select('#bestList > ol > li'))
```




    40





잘되는 것을 확인하였습니다. 각 li 안에는 p 태그가 여러개 있는데 이 중 세번째 p 엘리먼트 안에 책 이름이 담겨 있고, 가격을 담고 있는 p 엘리먼트에는 price 클래스가 붙어 있습니다.
~~~html
<li>
   <p>...</p>
   <p>...</p>
   <p><a href="...">책이름</a></p>
   ...
   <p class="price"><strong>가격</strong></p>
</li>
~~~
책 이름을 뽑아내볼까요?


```
bs.select('#bestList > ol > li p:nth-child(3) a')
```


    ---------------------------------------------------------------------------

    NotImplementedError                       Traceback (most recent call last)

    <ipython-input-29-4dcaccc7a75f> in <module>()
    ----> 1 bs.select('#bestList > ol > li p:nth-child(3) a')
    

    /usr/local/lib/python3.6/dist-packages/bs4/element.py in select(self, selector, _candidate_generator, limit)
       1449                 else:
       1450                     raise NotImplementedError(
    -> 1451                         'Only the following pseudo-classes are implemented: nth-of-type.')
       1452 
       1453             elif token == '*':
    

    NotImplementedError: Only the following pseudo-classes are implemented: nth-of-type.


각 li의 자식 중 세번째 자식인 p를 찾으려고 했으나 해당 셀렉터 문법은 beautifulsoup4에서 아직 구현하지 않았다며 에러가 발생합니다.

아쉽지만 각 책에 해당하는 li 엘리먼트들까지만 찾아서 변수에 담은 후 각 li 엘리먼트에서 원하는 정보를 뽑아내는 코드를 따로 만들어야합니다.


```
books = bs.select('#bestList > ol > li')
titles = []
for book in books:
  # "p:nth-of-type(3)"은 li의 자식 중 세번째 p 엘리먼트를 찾아줍니다.
  title = book.select_one('p:nth-of-type(3) a').text
  titles.append(title)
titles
```




    ['역사의 역사',
     '죽고 싶지만 떡볶이는 먹고 싶어',
     '열두 발자국',
     '설민석의 한국사 대모험 7',
     '돌이킬 수 없는 약속',
     '나는 오늘도 경제적 자유를 꿈꾼다',
     '모든 순간이 너였다',
     '언어의 온도 (100만부 돌파 기념 양장 특별판)',
     '곰돌이 푸, 행복한 일은 매일 있어',
     '사피엔스',
     '원피스 ONE PIECE 89',
     '나는 나로 살기로 했다',
     '아몬드',
     '고양이 1',
     '한때 소중했던 것들',
     '개인주의자 선언',
     '나미야 잡화점의 기적 (100만 부 기념 특별 한정판)',
     '고양이 2',
     '에듀윌 한국사능력검정시험 2주끝장 고급 개정판 3.0',
     '혼자공부법',
     '해커스 토익 실전 1000제 READING 1 문제집',
     '앨리스, 너만의 길을 그려봐',
     '2019 전한길 한국사 필기노트+빵꾸노트',
     '설민석의 한국사 대모험 6',
     '행복해지는 연습을 해요',
     '해커스 토익 기출 보카',
     '설민석의 한국사 대모험 1',
     '82년생 김지영',
     '하마터면 열심히 살 뻔했다',
     '어디서 살 것인가',
     '해커스 토익 실전 1000제 LISTENING 1 문제집',
     '해커스 토익 Reading (2018)',
     '어떻게 살 것인가',
     '2019 선재국어 세트',
     '곰돌이 푸, 서두르지 않아도 괜찮아',
     '열혈강호 76',
     '있으려나 서점',
     '내게 무해한 사람',
     '마법천자문 42',
     '대한민국 아파트 부의 지도']



비슷한 방법으로 가격도 뽑아냅시다.


```
books = bs.select('#bestList > ol > li')

titles = []
prices = []
for book in books:
  # "p:nth-of-type(3)"은 li의 자식 중 세번째 p 엘리먼트를 찾아줍니다.
  title = book.select_one('p:nth-of-type(3) a').text
  titles.append(title)

  price = book.select_one('p.price').text
  prices.append(price)

prices
```




    ['14,400원(10%+5%)',
     '12,420원(10%+5%)',
     '15,120원(10%+5%)',
     '9,450원(10%+5%)',
     '13,500원(10%+5%)',
     '15,120원(10%+5%)',
     '12,420원(10%+5%)',
     '12,420원(10%+5%)',
     '10,800원(10%+5%)',
     '19,800원(10%+5%)',
     '4,500원(10%+5%)',
     '12,420원(10%+5%)',
     '10,800원(10%+5%)',
     '11,520원(10%+5%)',
     '12,600원(10%+5%)',
     '12,150원(10%+5%)',
     '13,320원(10%+5%)',
     '11,520원(10%+5%)',
     '18,900원(10%+5%)',
     '12,600원(10%+5%)',
     '10,710원(10%+5%)',
     '12,420원(10%+5%)',
     '18,900원(10%)',
     '9,450원(10%+5%)',
     '13,050원(10%+5%)',
     '11,610원(10%+5%)',
     '8,820원(10%+5%)',
     '11,700원(10%+5%)',
     '13,500원(10%+5%)',
     '14,400원(10%+5%)',
     '10,710원(10%+5%)',
     '16,920원(10%+5%)',
     '13,500원(10%+5%)',
     '46,800원(10%)',
     '12,420원(10%+5%)',
     '4,050원(10%+5%)',
     '11,520원(10%+5%)',
     '12,150원(10%+5%)',
     '8,820원(10%+5%)',
     '15,120원(10%+5%)']



가격을 정수로 바꿔주면 좋겠습니다. 우선 괄호 안에 담긴 내용을 제거해볼까요? 파이썬 문자열 객체에는 split() 함수가 있습니다. 이 함수를 써서 여는 괄호 "(" 문자를 기준으로 문자열을 둘로 나눈 뒤 앞 부분(0번째 조각)을 취하면 괄호 뒷 부분을 제거할 수 있습니다.


```
"14,000원(10%+5%)".split("(")
```




    ['14,000원', '10%+5%)']




```
"14,000원(10%+5%)".split("(")[0]
```




    '14,000원'



"원"이라는 글자와 쉼표를 제거하면 숫자만 남습니다.


```
"14,000원(10%+5%)".split("(")[0].replace('원', '').replace(',', '')
```




    '14000'



이제 숫자만 남은 문자열들을 정수로 바꿔줍시다.


```
int("14,000원(10%+5%)".split("(")[0].replace('원', '').replace(',', ''))
```




    14000



해당 코드를 함수로 만들어볼까요?


```
def to_int(raw):
  nums = raw.split("(")[0].replace('원', '').replace(',', '')
  return int(nums)

to_int("14,000원(10%+5%)")
```




    14000



이제 원래 코드에 적용해봅시다.


```
books = bs.select('#bestList > ol > li')

titles = []
prices = []
for book in books:
  # "p:nth-of-type(3)"은 li의 자식 중 세번째 p 엘리먼트를 찾아줍니다.
  title = book.select_one('p:nth-of-type(3) a').text
  titles.append(title)
  price = book.select_one('p.price').text
  prices.append(to_int(price))

prices
```




    [14400,
     12420,
     15120,
     9450,
     13500,
     15120,
     12420,
     12420,
     10800,
     19800,
     4500,
     12420,
     10800,
     11520,
     12600,
     12150,
     13320,
     11520,
     18900,
     12600,
     10710,
     12420,
     18900,
     9450,
     13050,
     11610,
     8820,
     11700,
     13500,
     14400,
     10710,
     16920,
     13500,
     46800,
     12420,
     4050,
     11520,
     12150,
     8820,
     15120]



리스트 컴프리헨션을 써서 코드를 줄여볼까요?


```
books = bs.select('#bestList > ol > li')
titles = [b.select_one('p:nth-of-type(3) a').text for b in books]
prices = [to_int(b.select_one('p.price').text) for b in books]
```

DataFrame에 넣어봅시다.


```
import pandas as pd

df = pd.DataFrame(
    {'title': titles, 'price': prices},
    columns=['title', 'price']
)
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>title</th>
      <th>price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>역사의 역사</td>
      <td>14400</td>
    </tr>
    <tr>
      <th>1</th>
      <td>죽고 싶지만 떡볶이는 먹고 싶어</td>
      <td>12420</td>
    </tr>
    <tr>
      <th>2</th>
      <td>열두 발자국</td>
      <td>15120</td>
    </tr>
    <tr>
      <th>3</th>
      <td>설민석의 한국사 대모험 7</td>
      <td>9450</td>
    </tr>
    <tr>
      <th>4</th>
      <td>돌이킬 수 없는 약속</td>
      <td>13500</td>
    </tr>
  </tbody>
</table>
</div>



전체 코드를 한 번에 모아볼까요?


```
from urllib import request
import pandas as pd
from bs4 import BeautifulSoup

url = "http://www.yes24.com/24/category/bestseller"
with request.urlopen(url) as f:
  charset = f.headers.get_content_charset()
  html = f.read().decode(charset)

def to_int(raw):
  nums = raw.split("(")[0].replace('원', '').replace(',', '')
  return int(nums)

bs = BeautifulSoup(html, 'html5lib')
books = bs.select('#bestList > ol > li')
titles = [b.select_one('p:nth-of-type(3) a').text for b in books]
prices = [to_int(b.select_one('p.price').text) for b in books]

df = pd.DataFrame(
    {'title': titles, 'price': prices},
    columns=['title', 'price']
)
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>title</th>
      <th>price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>역사의 역사</td>
      <td>14400</td>
    </tr>
    <tr>
      <th>1</th>
      <td>죽고 싶지만 떡볶이는 먹고 싶어</td>
      <td>12420</td>
    </tr>
    <tr>
      <th>2</th>
      <td>열두 발자국</td>
      <td>15120</td>
    </tr>
    <tr>
      <th>3</th>
      <td>설민석의 한국사 대모험 7</td>
      <td>9450</td>
    </tr>
    <tr>
      <th>4</th>
      <td>돌이킬 수 없는 약속</td>
      <td>13500</td>
    </tr>
  </tbody>
</table>
</div>



URL만 넣으면 BeautifulSoup 객체를 만들어주는 코드도 함수로 만들면 좋겠습니다


```
from urllib import request
import pandas as pd
from bs4 import BeautifulSoup

def load_url(url):
  """URL의 HTML 문서를 받아와서 BeautifulSoup 객체 생성"""
  with request.urlopen(url) as f:
    charset = f.headers.get_content_charset()
    html = f.read().decode(charset)
  return BeautifulSoup(html, 'html5lib')

def to_int(raw):
  """Yes24의 책 가격 문자열을 정수로 변환"""
  nums = raw.split("(")[0].replace('원', '').replace(',', '')
  return int(nums)

bestseller_url = "http://www.yes24.com/24/category/bestseller"
bs = load_url(bestseller_url)
books = bs.select('#bestList > ol > li')
titles = [b.select_one('p:nth-of-type(3) a').text for b in books]
prices = [to_int(b.select_one('p.price').text) for b in books]

df = pd.DataFrame(
    {'title': titles, 'price': prices},
    columns=['title', 'price']
)
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>title</th>
      <th>price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>역사의 역사</td>
      <td>14400</td>
    </tr>
    <tr>
      <th>1</th>
      <td>죽고 싶지만 떡볶이는 먹고 싶어</td>
      <td>12420</td>
    </tr>
    <tr>
      <th>2</th>
      <td>열두 발자국</td>
      <td>15120</td>
    </tr>
    <tr>
      <th>3</th>
      <td>설민석의 한국사 대모험 7</td>
      <td>9450</td>
    </tr>
    <tr>
      <th>4</th>
      <td>돌이킬 수 없는 약속</td>
      <td>13500</td>
    </tr>
  </tbody>

  
