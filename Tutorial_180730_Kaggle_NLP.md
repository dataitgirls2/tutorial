## 스테밍(어간추출, 형태소 분석)

- 어간 추출(stemming)은 어형이 변형된 단어로부터 접사 등을 제거하고 그 단어의 어간을 분리해 내는 것
- "message", "messages", "messaging"과 같이 복수형, 진행형 등의 문자를 같은 의미의 단어로 다룰 수 있도록 도와준다.
- stemming : 여기에서는 NLTK에서 제공하는 stemming 도구를 사용한다. 어간을 분리하며 변형된 단어를 추출하기도 한다.

출처 : [어간 추출 - 위키백과, 우리 모두의 백과사전][https://ko.wikipedia.org/wiki/%EC%96%B4%EA%B0%84_%EC%B6%94%EC%B6%9C]



### PorterStemmer

~~~python
import nltk
stemmer = nltk.stem.PorterStemmer()

print("The stemmed form of studying is: {}".format(stemmer.stem("studying")))
print("The stemmed form of studies is: {}".format(stemmer.stem("studies")))
print("The stemmed form of study is: {}".format(stemmer.stem("study")))

>>>The stemmed form of studying is: studi
>>>The stemmed form of studies is: studi
>>>The stemmed form of study is: studi
~~~



### LancasterStemmer

~~~python
from nltk.stem.lancaster import LancasterStemmer
lancaster_stemmer = LancasterStemmer()

print("The stemmed form of studying is: {}".format(lancaster_stemmer.stem("studying")))
print("The stemmed form of studies is: {}".format(lancaster_stemmer.stem("studies")))
print("The stemmed form of study is: {}".format(lancaster_stemmer.stem("study")))

>>>The stemmed form of studying is: study
>>>The stemmed form of studies is: study
>>>The stemmed form of study is: study
~~~



### SnowballStemmer

~~~python
from nltk.stem.snowball import SnowballStemmer
stemmer = SnowballStemmer('english')

print("The stemmed form of studying is: {}".format(stemmer.stem("studying")))
print("The stemmed form of studies is: {}".format(stemmer.stem("studies")))
print("The stemmed form of study is: {}".format(stemmer.stem("study")))

>>>The stemmed form of studying is: studi
>>>The stemmed form of studies is: studi
>>>The stemmed form of study is: studi
~~~



### kaggle 실습에서 스테밍 활용 - 문자열 처리

~~~python
def review_to_words( raw_review ):
    # 1. HTML 제거
    review_text = BeautifulSoup(raw_review, 'html.parser').get_text()
    # 2. 영문자가 아닌 문자는 공백으로 변환
    letters_only = re.sub('[^a-zA-Z]', ' ', review_text)
    # 3. 소문자 변환
    words = letters_only.lower().split()
    # 4. 파이썬에서는 리스트보다 세트로 찾는게 훨씬 빠르다.
    # stopwords 를 세트로 변환한다.
    stops = set(stopwords.words('english'))
    # 5. Stopwords 불용어 제거
    meaningful_words = [w for w in words if not w in stops]
    # 6. 어간추출
    stemming_words = [stemmer.stem(w) for w in meaningful_words]
    # 7. 공백으로 구분된 문자열로 결합하여 결과를 반환
    return( ' '.join(stemming_words) )
~~~



## 예측률 높이기 실습

### 기존 예측률 : 0.85024

~~~python
from sklearn.feature_extraction.text import CountVectorizer
from sklearn.feature_extraction.text import TfidfTransformer
from sklearn.pipeline import Pipeline

# 튜토리얼과 다르게 파라메터 값을 수정
# 파라메터 값만 수정해도 캐글 스코어 차이가 많이 남
vectorizer = CountVectorizer(analyzer = 'word', 
                             tokenizer = None,
                             preprocessor = None, 
                             stop_words = None, 
                             min_df = 1, # 토큰이 나타날 최소 문서 개수
                             ngram_range=(1, 2),
                             max_features = 10000
                            )
vectorizer
~~~



1. min_df =3, ngram_range(1,4) : 0.85420

2. min_df = 2, ngram_range(1,4), max_features = 15000 : 0.85032
=======


## Lemmatizing

- 정의 : 앞/뒤 문맥을 보고 단어의 의미를 식별하는 것

- 예시 : 세 가지 배를 구분하는 것. 

  - `배`가 맛있다
  - `배`가 아프다
  - `배`를 타러가자

- 코드

  ```python
  from nltk.stem import WordNetLemmatizer
  wordnet_lemmatizer = WordNetLemmatizer()
  
  print(wordnet_lemmatizer.lemmatize('fly'))
  print(wordnet_lemmatizer.lemmatize('flies'))
  ```

  > fly
  >
  > fly

  

## ROC 커브

### 1. 민감도와 특이도

- 민감도(TPR : True Positive Rate) 
  - True인 케이스를 True로 예측한 비율
  - 예 : 암 환자를 진찰해서 암이라고 진단
- FPR (False Positive Rate)
  - False인 케이스를 True로 예측한 비율
  - 암환자가 아닌데 암이라고 진단.
- 특이도
  - False인 케이스를 False로 예측한 비율
  - 1 - FRR
  - 예 : 암환자가 아닌데 암이 아니라고 진단
- 특이도와 민감도는 반비례적인 관계가 있음. 성급한 의사의 경우, 약간의 징후만으로도 암으로 진단하기 때문에 특이도가 높다. 하지만 암이 아닌 경우에도 암이라고 하기 때문에 특이도는 낮다. 반대로 돌팔이 의사의 경우, 모든 환자를 암이 아니라고 하기 때문에 특이도가 높지만, 암 환자를 알아보지 못하기 때문에 민감도가 낮아진다. 
- 분석하려는 케이스에 따라 민감도와 특이도 중 어느 쪽에 강조를 둘지를 정할 수 있다. 
  - 확률은 낮지만 치사율이 극히 높은 병 : 민감도가 높아야 함. 
  - 감기처럼 확률은 낮지만 위험성이 별로 없는 병 : 민감도가 낮아도 됨. 



### 2. ROC 커브

- 민감도와 특이도의 관계를 그래프로 표현하여 어느 지점을 기준으로 잡을 지 결정하기 쉽도록 시각화 한 것
- ![262E8E3F544837AD27](https://github.com/dataitgirls2/tutorial/262E8E3F544837AD27.png)
- X축 : 특이도
- Y축 : 민감도
- ROC 커브의 면적이 1에 가까울 수록(=왼쪽 위 꼭지점에 다가갈 수록) 좋은 성능이며, 면적은 0.5~1의 범위를 갖는다. 



## 참고자료

- http://newsight.tistory.com/53

