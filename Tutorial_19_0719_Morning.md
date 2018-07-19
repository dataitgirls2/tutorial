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

  