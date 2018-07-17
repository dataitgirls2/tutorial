# 크롤링1

## shuffle함수 과제 리뷰

##### [ 기억할 것 ] 

코드 작성은 설명이나 이름을 붙여주지 않아도 의도가 드러나도록 간결하게 짜는게 중요하다 

파이썬 함수 이름은 소문자와 _의 조합으로 쓰는게 좋다 e.g. sort_by_len()

파이썬은 대소문자를 구분하는 언어이다 (=Case Sensitive 언어)



+ rnadom.shuffle()을 이용하는 방법

  ```python
  import random
  
  
  def shuffle(data):
      copied = data[:]
      random.shuffle(copied)
      return copied
  
  
  data = [1, 2, 3, 4, 5]
  copied = shuffle(data)
  copied
  ```

  >여기서 random.shuffle 에 data를 바로 입력하지 않고 copied를 정의한 후 copied를 입력하는 이유는 원본 데이터의 변형을 포함하지 않고 shuffle을 진행하기 위함이다. 
  >
  >따라서 data[:]로 data를 복사하여 copied를 생성한다. 

  

+ random.sample()을 이용한 방법

  비복원 임의추출 방식 활용

  (data를 데이터 갯수만큼 샘플링해서 임의로 가져오는 방식. 한 번 뽑으면 다시 뽑히지 않음)

  ```python
  import random
  
  data = [1, 2, 3, 4, 5, 6]
  random.sample(data, len(data))
  ```

  > 여기서 마지막 코드를 random.sample(date, 6)으로 짤때, 6은 'magic number'가 된다.
  >
  > 만약 어떠한 수정 작업으로 인해 data길이가 수정된다면, random.sample(data,수정된 data길이)로 매번 바꿔줘야 한다. 
  >
  > random.sample(data, len(date))로 작성한다면 magic number로 인한 비효율성을 제거할 수 있다.  

  

+ Fisher-Yates sampling의 방식

  Ronald Fisher와 Frank Yates가 1938에 <Statistical tables for biological, agricultural and medical research>에서 소개한 절차. “난수표"랑 종이와 연필이 필요.
  >
  > **[Fisher-Yates sampling 참고 페이지](https://exceptionnotfound.net/understanding-the-fisher-yates-card-shuffling-algorithm/) 'Visualizing the Original Method' 에서 시각적으로 어떤 과정을 통해  sampling이 이뤄지는지 알 수 있음**

  ```python
  from random import randint
  
  def shuffle3(data):
    new_list = data.copy()
    result = []
    x = 0
    for x in range(len(data)):
      index = (randint(0, len(new_list) - 1))
      result.append(new_list[index])
      del new_list[index]
    print(result)
    
  shuffle3([1, 2, 3, 4, 5])
  ```

  

+ 랜덤 요소를 끌어와서 적용시키는 방식

  실제 세상으로부터 노이즈(현재 시간, 마우스 위치, 베터리 잔량, 키보드 입력 패턴 등등)를 끌어와서 랜덤 요소로 쓰는 시도가 많이 있음

  ```python
  # 현재 시간을 이용한 랜덤
  import time
  data = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
   
  def shuffle1(data):
    now = int(time.time())
    random = now % 10
    result = data.copy()
    length = len(data)-1
    for num in range(length) :
      temp = result[num]
      result[num] = result[length - random]
      result[length-random] = temp
    return result
    
  print('shuffle ', shuffle1(data))
  print('원본 ', data)
  ```

  

## 인터넷, 웹, 웹브라우저, HTML 개념알기

**개념정리**

+ 인터넷 : 컴퓨터 네트워크들 간의 네트워크(**inter-net**work)

+ 웹(WWW) : HTTP;hypertext transfer protocol(하이퍼텍스트를 전송하는 프로토콜)로 통신하는 컴퓨터들의네트워크 

  > [참고 : 인터넷과 웹, 웹 브라우저](https://www.youtube.com/watch?v=J8hzJxb0rpc)

  + URL(Uniform Resource Locator): protocol://user@host:port/path?query#fragment 형식 

    ```http
    https://www.google.com/search?q=test
    ```

  + Hyperlink : 링크가 걸린 텍스트

  + Hypertext : 하이퍼링크가 담겨져 있는 텍스트 (ex. 구글 검색화면) 

  + HTML (HyperText Markup Language) : 하이퍼텍스트를 작성하기 위한 언어 중 하나 

+ 웹브라우저 : "사용자 대리인(user agent)"의 일종

  인간이 컴퓨터말로 직접 다 말을 걸 수 없기 때문에 사람들이 입력하는 내용(아마도 구현된 웹 인터페이스 상에서 클릭을 한다거나 텍스트를 입력한다거나...)을 받아 컴퓨터의 HTTP응답으로 바꾸고 그를 해석하여 인간에게 보여주는 역할을 함.

+ DOS 공격
  흔히 도스 공격이라고 하는 얘기를 뉴스에서 가끔 들을 수 있는데 이는 서버가 처리할 수 있는 양 이상을 보내서 서버가 과부화되는 현상을 의미한다. 예를 들면, 은행 업무를 마비시키기 위해 10000원을 10원 단위로 수백명이 인출하려고 한다고 생각해보자. 이렇게 되면 한번에 처리할 수 있는 업무량을 월등히 초월해버리기 때문에 시스템이 마비된다. 이런 원리를 서버에 적용한다고 볼 수 있다. 

+ 아스키코드와 utf-8
  아스키(ASCII)는 영문 알파벳을 사용하는 대표적인 문자 인코딩이다. 아스키는 컴퓨터와 통신 장비를 비롯한 문자를 사용하는 많은 장치에서 사용되며, 대부분의 문자 인코딩이 아스키에 기초를 두고 있다. 
  알파벳에 기초하고 있기 때문에 그보다 많은 양의 문자를 필요로 하는 한글은 아스키만으로는 표현하기 어렵다. 한글을 출력하기 위해선 utf-8인코딩 방식이 필요하다. UTF-8은 Universal Coded Character Set + Transformation Format – 8-bit 의 약자로 말 그대로 라틴계열의 문자 이외의 수많은 언어를 표현하기 위해 1바이트만 사용하는 아스키와는 다르게 1바이트에서 4바이트까지 사용한다. 



# 데이터 가져오기

```python
from urllib import request 
#request라는 파이썬 오픈 함수중에 urllib라는 함수를 호출하는 것
#url라이브러리에서 리퀘스트를 import하겠다
#import : 다른사람들이 만들어놓은 python 코드를 불러오는 것

url = "http://www.naver.com"
with request.urlopen(url) as f:
#with request.urlopen(url) as f :  request.urlopen(url)에서 만든 자원을 f에 할당하고 다 쓴 다음에는 자원을 해제하기 위해 쓰인다.
#f는 file의 약자.
  html = f.read().decode('utf-8')
#read() : http 리퀘스트를 보내고 응답으로 받은것을 읽어온다. 그 응답은 바이트로 온다.
#뭐.뭐.뭐 의 형식을 chaining이라고 함 
#바이트를 스트링으로 디코딩해주는 것은 decode()
  print(html)
```

+ 위계 : 라이브러리 > 패키지 >  모듈 > 함수

  >  urllib = 패키지
  >
  > request = urllib 패키지 안에있는 모듈
  >
  > urlopen() = urllib package 안에 있는 request module 안에 있는 함수

  > 경로로 표현해 보면 위계는 다음과 같다 
  >
  >  **urllib/request/urlopen()** 

  > 파이썬라이브러리는 패키지들을 모아둔 것 
  >
  > (파이썬 표준 라이브러리는 파이썬 설치할 때 들어있음. )

  

# 저작권과 직업윤리 

**직업윤리**

- 부당한 차별 : 차별적 발언을 한 의도는 중요하지 않고 결과가 중요하다.(?) 동일한 발언이라 하더라도 사회역사적 맥락이 중요하다. 같은 발언이라도 어떤사회에 어떤역사의 어떤 맥락에서 하면 부당한 차별이 되는지. --> when is discrimination wrong?

**저작권**

- 우리가 만드는 코드에도 저작권이 있고, 코드 실행결과 나오는 데이터, 프로그램으로 가공해서 파생된 데이터의 저작권도 중요하다.

- 별도로 라이선스에 대한 설명이 없으면 저작자에게 물어보아야 한다. 이 데이터를 이러이러한 용도로 쓰려고 하는데 써도 되겠는가 허락을 맡아야 한다.

- 거의 모든 컨텐츠에는 어딘가 보면 저작권 관련 문구가 있다.

- 저작권표시 참고 <http://cckorea.org/xe/elements>

- 로봇배제프로토콜  : 누군가 크롤러를 만들어서 데이터를 긁어가려고 하면 여기를 참고하세요라는 의도로 만들어진것

  ```
  User-agent: *  # 모든 유저에이전트는
  Disallow: /  # 루트디렉토리부터 모두 불허용
  ```

  청와대 사이트는 허용가능하게 해놓았음



