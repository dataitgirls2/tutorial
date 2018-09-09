
# Tutorial_20180723_Morning 

### 분석 Pandas 🔽
   - 엑셀보다 불러올 수 있는 파일의 사이즈가 크고, 더 다양하게 분석할 수 있는 tool

### 수치계산 Numpy 🔽

  - 데이터 구조외에도 수치계산을 위해 효율적으로 구현 된 기능을 제공

### 시각화 🔽

    Matplolib
      - plotline
      - seaborn
---



###  <관련 개념 정리> 

### (1) scikit learn (싸이킷 런)

- 파이썬에 있는 대표적인 Machine Learning Library.
- data mining, data analysis를 위한 간결하고 효과적인 툴.
- Numpy, scipy, matplotlib으로 쓰여졌다.
- 오픈 소스이자 상업적으로 사용 가능하다. (BSD license)

### (2) classification(분류)

* 속성에 따라 분류해준다.

### (3) regression(회귀)

* 수요 분석할 때 많이 사용한다.

### (4) clustering(군집화) 

* 비슷한 아이들끼리 묶어준다.

### (5) dimensionality reduction(차원축소)

- 압축해서 본다.
- wordcloud로 단어의 유사도를 체크하고, 유사도에 기초하여 군집화한다.
- 3차원의 경우 2차원으로 줄인다.

---


### <기계학습 기초>

> **Andread Muller's Machine Learning with Scikit-Learn**
>
> Classification, Regression, Clustering, Semi-Supervised Learning, Feature Selection, Feature > Extraction, Manifold Learning, Dimensionality Reduction, Kernel Approximation, 
> Hyperparameter Optimization, Evaluation Metrics, Out-of-core learning, ...




  ### Supervised Machine Learning (지도학습) 🔎

- Traning data를 넣어서 어떤 모델을 만들고, Test Data에 있는 Training Labels를 예측하는 것이 Supervised Machine Learning이다. 
  Coursera에서 강의를 들어볼 수 있다. 보스턴의 집 값을 예측하는 머신 러닝 알고리즘. 통계 시간에 측정 기법들을 배우게 될 것이다.
- Traning (훈련)과 Generalization (일반화). 특정 데이터에만 맞는 데이터가 아니라, 어떤 데이터도 예측 가능하도록 결측치를 제거하거나, 
  하는 등의 과정을 Traning. 이후 테스트하고 평가하는 과정을 Generalization이라고 한다.
- 분류와 회귀의 경우 거의 지도학습에 해당한다. 비지도 학습으로도 수행할 수 있으나, labels를 가지고 분류하는 경우 supervised. 회귀의 경우 
  집 값 예측이나 배송 물건 예측, 배송 시간 예측 등은 기존의 데이터를 기계에게 알려주어 그것을 바탕으로 예측하도록 한다. 


>  #### clf.fit(X_train, y_train)

```
X는 대문자를 사용하고, y는 소문자를 사용하는 이유는 
X = 행렬   y는 벡터이기 때문이다.
```
```
X_train은 train데이터의 행렬을 뜻한다.
y_train은 train데이터의 벡터를 뜻한다.
```

>  #### clf.score(X_test, y_test)

```
train을 통해 알고싶은 것이나, 확인한 결과가 맞는지, test를 통해 알아본다.   
(예측 결과가 얼마나 정확한지 평가하는 단계)
```

#### 단 네 줄로 기계학습을 실행할 수 있다!  🔻



```python
clf = RandomForestClassifier()
clf.fit(X_train, y_train)
y_pred = clf.predict(X_test)
clf.score(X_test, y_texst)
```

### Unsupervised Machine Learning (비지도학습) ☂️

#### ❔ 지도학습과 차이점 ❔

Training Data를 넣고, 바로 Test 한다. Unsupervised 같은 경우는, labels가 없다.



```python
 pca = PCA()
 pca.fit(X_train)
 X_new = pca.transform(X_test)
```

> 기준O = 지도학습 
>
> 기준X = 비지도학습
>
> 분류할 때 clustering을 하면 Unsupervised Machine Learning 이다.

**Labels, Features ?**

- e.g.) Labels에 고양이와 개. 몸무게, 키 등의 기준(속성)들이 Features. 지도 학습에서는 Labels를 주고 이것을 바탕으로 Classify 한다. 비지도 학습에서는 Labels가 없음. 분류가 아니라 회귀의 경우, Labels에 집 값이 들어간다.

#### 몸무게와 키를 features라고 하고 분류할 때 labels이 개/고양이 중 무엇인지 찾는 것

```
몸무게     키      label
30kg      20cm      개
20kg      15cm    고양이
```
(by_정지은님 설명 :girl:)



#### TfidVertorizer 

- 검색 엔진에서 자주 사용하는 알고리즘. 단어에 가중치를 준다. Bag of Word의 단점을 보완하는 도구로 사용되고 있다.



----

### Overfitting(과대적합)과 Underfitting(과소적합)

> Training과 Heneralization의 격차가 적은 구간이 정확도의 측면에서 최적화된 지점 (Sweet spot)이다. Underfitting의 경우 모수가 적은 경우. 데이터를 적게 부여하고 학습을 시킨 경우, 제대로 학습되어 있지 않다고 하여 underfitting 이라고 한다. 

> 반대로 너무 학습이 잘 되어 Outlier나 결측치에 대해서도 학습을 하는 경우를 overfitting이라고 한다.

> e.g.) 어떤 학습 결과가 육아 관련 데이터를 잘 예측하지만 반려동물 데이터에 대해서는 > 잘 예측하지 못한다면, 이 학습 결과는 육아 관련 데이터에 overfitting 되었다고 
> 한다.


#### (1) Overfitting :chart_with_upwards_trend:  

```
Model이 Train Data에 너무 잘 맞지만 일반성이 떨어진다는 의미
-> 너무 훈련데이터에 맞춰져 있어서 Test Data에서는 높은 성능을 보여줄 확률이 낮다.
-> 모델의 복잡도가 필요이상으로 높기 때문이다.
```

   ####               해결방법

> ```
> - 훈련 데이터를 더 많이 모은다.
> - 정규화
> - 오류 수정과 이상치 제거
> ```



#### (2) Underfitting :chart_with_downwards_trend:

```
Mddel이 너무 단순해서 Data의 내재된 구조를 학습하지 못할 때 발생.
-> 모수가 너무 작아서 발생
```

#####             해결방법

>```
> - 파라미터가 더 많은 복잡한 모델을 선택
> - 모델의 제약을 줄이기(규제 하이퍼파라미터 값 줄이기)
>```



#### Decision Trees 

- True / False 로 구분되는 Data. 어떤 기준을 바탕으로 점점 True/False로 Depth를 더해가며 그래프를 그린다.
- 이것이 정확도가 떨어져서, 이 부분을 보완한 것이 RandomForests이다. 이러한 Decision Trees 를 Random하게 매우 많이 그린다. depth를 너무 깊게 내려가도 overfitting이 되어 정확도가 떨어지고, depth가 너무 낮아도 underfitting 되어 정확도가 떨어진다. 데이터에 맞게 적절한 지점을 찾는 것이 중요하다.

-----

### <자연어 처리 실습>

**(1) 정규표현식을 사용해서 지난 시간 soynlp 실습 결과 wordcloud 개선하기**

- 불용어 제거하기

  - preprocessing (전처리)


```python
    def preprocessing(text):
        text = re.sub('- ', ' ', text)
        text = re.sub('같습니다', ' ', text)
        text = re.sub('좋았습니다', '좋았어요', text)
        text = re.sub('지영님의', '지영님', text)
        return text
```

 - remove_stopwords (불용어 제거)


```python
def remove_stopwords(text):
        stops = ['수', '있는', '있습니다', '그', '년도', '에', '합니다', '하는', '및', '제', '할', '하고', '더', '대한', '한', '그리고', '월', '저는', '없는', '것입니다', '등', '일', '많은', '이런', '것은', '왜', '같은', '없습니다', '위해', '한다']
        # Stopwords 불용어 제거
        meaningful_words = [word for word in text if not word in stops]
        return ' '.join(meaningful_words)
    
    %time tokens_remove_stopwords = 토큰으로만든단어들.apply(remove_stopwords)
```

**(2) 정규표현식 불러오기**

- `import re`
- 정규표현식은 모든 언어에 다 있다.
- 데이터 전처리 preprocessing에 필수 요소이다.


> text = re.sub('\\\\n', ' ', text)에서 공백을 설정해주는 이유는 단어끼리 붙는 것을 방지하기 위해서 이다.


> %time을 입력하면 해당 코드를 실행할 때 걸리는 시간을 출력해준다.
> %%time = 해당줄이 여러개일 때 사용한다.


```python
def preprocessing(text):
    # 개행문자 제거
    text = re.sub('\\\\n', ' ', text)
    # 특수문자 제거
    # 특수문자나 이모티콘 등은 때로는 의미를 갖기도 하지만 여기에서는 제거했습니다.
    # text = re.sub('[?.,;:|\)*~`’!^\-_+<>@\#$%&-=#}※]', '', text)
    # text = re.sub('[0-9]', '', text)
    # 한글, 영문, 숫자만 남기고 모두 제거하도록 합니다.
    # text = re.sub('[^가-힣ㄱ-ㅎㅏ-ㅣa-zA-Z0-9]', ' ', text)
    # 한글, 영문만 남기고 모두 제거하도록 합니다.
    text = re.sub('[^가-힣ㄱ-ㅎㅏ-ㅣa-zA-Z]', ' ', text)
    return text
```

#### 만약 워드클라우드 안에 원하는 단어수만 출력하고 싶다면 ❔
>  row데이터에서 '상위 몇 %' 이런식으로 전처리를 해줘야 된다.

