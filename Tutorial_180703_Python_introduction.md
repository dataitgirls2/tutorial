# 파이썬 기초 1

---

## 수업의 목표

- 파이썬 소개  
- 기본 문법과 개념 익히기  
- 파이썬 프로그래밍 환경 Colab 익히기  

### Python

- 범용적 프로그래밍 언어. 데이터 분석, 과학 계산, 웹 프로그래밍 등에 주로 쓰임  
  a list of Programming languages : <https://en.wikipedia.org/wiki/List_of_programming_languages>  
  Python? :  <https://en.wikipedia.org/wiki/Python_(programming_language)>
- 1991년 프로그래머 귀도 반 로섬이 크리스마스 휴가 때 취미로 만들었으며 영국 코미디언 그룹 몬티 파이선에서 이름을 따왔다. 
- 장점
  1) 데이터 수집, 분석, 웹 서비스 적용까지 모든 과정을 한 언어로 끝낼 수 있음.
  2) 문법 & 성능이 괜찮음
  3) 다양한 패러다임 지원(ex: 1부터 10까지 더하는 서로 다른 방식) 
  4) 훌륭한 개발자 커뮤니티 (한국 포함)
  5) 풍부한 참고자료

- 괜찮은 문법, 괜찮은 성능이라고 얘기할 때의 기준? 
  - 괜찮은 문법 : 학습/사용이 간결하고 직관적. 문법에 대한 설명이 간결함.
  - 괜찮은 성능 : 명령 수행 속도가 느리지 않음.

- 접착제 언어 : 다른 다양한 언어와 결합하여 사용 가능 (C, Java 등)
  - 외워야하는 문법 30개 정도. 영어 자연어를 닮게 만들기 위해 키워드가 많아짐. 문법이 너무 간소하면 비직관적. 사용할 때 짧은 문법들을 조합 해야함.
  - 위키의 List of programming languages 에 나오는 프로그래밍 언어의 리스트에서, 컴퓨터가 읽을 수 있도록 코드를 짜서 개별 이름들을 데이터로 뽑아낼 수 있다. 
  - 예시는 selector 문법으로, HTML 문서에서 원하는 부분만 뽑아내는 문법이다. 파이썬에서도 활용할 수 있다.

- 개발자를 미치게 하는 10가지 언어 : http://www.itworld.co.kr/slideshow/90954
- 서버 호텔=ICT

### 파이썬 실습 1 - 다양한 실습 도구 활용

- Scratch -> Python 실습 : Blockly (https://blockly-demo.appspot.com/static/demos/code/index.html)  
  블럭이 각 언어로 어떻게 변환되는지 살펴보기(언어로 바로 쓰는 것보다 복잡할 수 있음)
- Python 실습 : Google Colaboratory 
  - https://colab.research.google.com/notebooks/welcome.ipynb#recent=true
  - 마크다운(.md) 문법 사용 가능
  - '범죄통계' 파일 @데잇걸즈2 수업자료 폴더 : 향후 데이터를 다루는 방법을 preview 
- Python 실습 2 : Pythontutor. 
  - 소스 코드를 단계별로 실행하면서 작동 원리/오류 원인을 확인 가능. 
  - http://www.pythontutor.com

### 파이썬 문법

- 대입문 : '변수(variable) = 수식(expression)' 형식 (순서가 바뀌어 수식 = 변수가 되면 안됨)
  '='는 대입 연산자(assignment operator). literal, integer, floating도 수식.
  짙은 파란색 : expression
  옅은 파란색 : keyword *(개발 환경이나 개인 설정에 따라 다를 수 있음)*
  ~~~python
  >>> a = 3 * 4
  >>> print (type(a))
  <class 'int'>
  >>> b = float(a)
  >>> print (type(b))
  <class 'float'>
  ~~~
  
- keyword : 언어 구현을 위해 개발 환경에서 기능이 예약된 문자열, 변수 이름으로 사용 불가
- for 변수 in iterable : 반복문. iterative한 변수(예-list)를 차례대로 돌면서 작동을 반복함.

- 정수 : Integer (int) / 실수 : Floating point (float).  
  
- 모든 literal은 수식
-  대입문 오른쪽에는 무조건 수식(expression)이 와야 함
- 파이썬 들여쓰기(indentation) convetion : 스페이스 4번. 2칸도, 8칸도, tab도 아닌 **스페이스 4칸**
- 파이썬에서 2(integer; 정수), 2.0(floating point; 부동 소수)과 '2'(string; 문자열)은 서로 다르다!
  - int + float = float로 출력됨.
  ~~~python
  >>> a = 2 + 2.0
  >>> print (type(a))
  <class 'float'>
  ~~~
- 파이썬에서 숫자는 0부터 세기 때문에 첫 번째 칸은 '0'번 칸임. 즉, 두 번째 칸이 '1'번 칸임.
- 컴퓨터 정수 바운더리 : -21억~+21억  
  - 자릿수나 정밀도를 제한해서 숫자를 표현함. 

- 대입문
  ~~~python
  n = 0	# 대입문
  total = 0
  nums = [90, 95, 92, 100]	
  for i in nums:		  	# for i in range(5): 로 면 결과가 어떻게 달라지는지는 다음 코드블럭 참조.
      total = total + i
      n = n + 1 
      average = total / n
  print(average) # 결과값: 94.25
  ~~~
  ~~~python
  n = 0
  total = 0
  for i in range(5):        #for i in [0, 1, 2, 3, 4]: 로 대체해도 결과는 같음
      total = total + i
      n = n + 1 
      average = total / n
  print(average) # 결과값: 2.0
  ~~~
- 변수 등을 통해 호출될 수 있는 연결 관계가 모두 끊어진 object(메모리에 저장된 임시 값)는 자동 삭제됨

- print와 return의 차이 : 
  print: 출력장치에 전송하는 것(화면에 출력)  
  return: 값을 메모리에 저장만 할 뿐(아무것도 출력되지 않음)  
  

### 파이썬 실습 2 - 짝 프로그래밍

- 총점과 평균 구하기
    ~~~python
    # Q. 70, 55, 90, 85, 100, 77의 합계와 평균 구하기
    score = [70, 55, 90, 85, 100, 77]
    num = 0
    total = 0
    for i in score:
        total = total + i
        num = num + 1 
    average = total / num 
    print('총점: ', total, ' 평균: ', average)
    ~~~

- 함수 정의(def)
  - 함수 - def 함수이름():  
  - def calc_sum()  
  - Define calculate_summation()
  - def calc_sum()  //서로다른 단어 연결시 언더바(_)사용  
  
~~~python
    # 합계 구하기 실습
    
    def calc_sum(numbs):			 #함수 정의('def')는 동사형, 변수 정의는 명사형을 주로 사용
        result = 0				    #결과값을 저장하는 변수
        for num in numbs:
            result = result + num
        return result				 #함수의 결과값을 반환
        
    def calc_len(numbs):  
        result = 0  
        for num in nums:  
            result = result + 1  
        return result  
        
    def calc_average(numbs):  
        total = calc_sum(numbs)  
        length = calc_len(numbs)  
        return total / length  
        
    scores = [50, 60, 70]  
    total = calc_sum(scores)		#함수를 호출
    avg = calc_average(scores)  
    print(total, avg)  
~~~
-  참고 : $$ 수학/공학 수식을 입력할 때에는 앞/뒤로 '$$'를 붙이면 됩니다. $$  
  
  - Library : 블럭을 쌓아서 압축하는 개념  
  - 블럭이 시작되기 전에는 :을! (콜론;은 실행의 의미!)  
  - Stack : 함수를 쌓는것(함수가 함수 호출)  
  	이게 너무 많아지면 stack overflow 오류 발생  
  - 이름 공간 namespace - 함수 안 이름은 함수 밖 세상에 영향 주지 않음 
    > *Namespaces are one honking great idea—let's do more of those!* (Tim Peters - Zen of Python에서 발췌)
  
  
  - Literal 0과 objects 0은 다름  
  - 모든 Expression을 evaluation평가해서 나오는 0은 evaluated value=objects 0  
    ex: a = 3 일 경우, a에 들어있는 값을 평가했더니 상수 0과 같은 것 (즉 a = 1+2, a = 0+3 일 경우에도 그 값을 평가하면 상수 3과 같다)  
