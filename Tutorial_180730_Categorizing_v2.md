# 국민청원 카테고리 분류하기

## Mission! 국민청원 데이터 카테고리 분류하기
국민청원 등록 시 분류를 함께 등록함. 분류 텍스트 데이터를 바탕으로 카테고리를 예측함

### 텍스트 데이터 전처리 전략
1. 텍스트 데이터 전처리 하기. 어떤 텍스트를 바꿔줄 것인가!
‘안녕하세요’, ‘안녕하십니까’ → ‘안녕’과 포함된 것은 빼고 필요한 것만 넣는 것. 일종의 불용어 제거. 학습에 도움되지 않는 것은 제거
2. 학습세트와 테스트세트 다시 만들기(단 학습세트와 테스트세트의 비율은 7:3으로 유지합니다.)
3. 텍스트 데이터 벡터화 할 때 파라메터 조정하기
parameter vectorizing: 벡터화 옵션을 바꾸는 것
4. 랜덤 포레스트의 파라미터 조정하기
5. (선택) 랜덤 포레스트 외의 알고리즘 사용해 보기(예. xgboost)
xgb 사용 시 colab에서 설치 후 사용해야 합니다.

~~~
import xgboost as xgb

# XGBoost Parameters http://xgboost.readthedocs.io/en/latest/parameter.html
model = xgb.XGBClassifier(n_estimators=10,
                          max_depth=6,
                          learning_rate=1.0,
                          max_delta_step=1,
                          eta = 1,
                          nthread=-1,
                          seed=2018)

%time score = cross_val_score(model, train_feature_tfidf, y_label, scoring="accuracy").mean()

score = -1.0 * score

print(round(np.mean(score)*100,2))
model.fit(train_feature_tfidf, y_label)

y_pred = model.predict(test_feature_tfidf)

print(y_pred.shape)
df_test['category_pred'] = y_pred
y_pred[:5]
~~~

~~~
불용어 처리 예제 
from sklearn.feature_extraction.text import CountVectorizer

stops = ['and', 'article', 'html', '수', '현', '있는', '있습니다', '그', '년도', '합니다', '하는', '및', '제', '할', '하고', '더', '대한', '한', '그리고', '월', '저는', '없는', '입니다', '등', '일', '많은', '이런', '것은', '왜','같은', '같습니다', '없습니다', '위해', '한다']
vectorizer = CountVectorizer(analyzer = 'word', # 캐릭터 단위로 벡터화 할 수도 있습니다.
                             tokenizer = None, # 토크나이저를 따로 지정해 줄 수도 있습니다.
                             preprocessor = None, # 전처리 도구
                             stop_words = stops, # 불용어 nltk등의 도구를 사용할 수도 있습니다.
                             min_df = 2, # 토큰이 나타날 최소 문서 개수로 오타나 자주 나오지 않는 특수한 전문용어 제거에 좋다. 
                             ngram_range=(1, 3), # BOW의 단위를 1~3개로 지정합니다.
                             max_features = 2000 # 만들 피처의 수, 단어의 수가 된다.
                            )
vectorizer


~~~

 특정 데이터에서는 잘 맞는데, 다른 데이터에서는 안맞을 수 있음. 인권 성평등과 반려동물에 대해서는 다를 것이기 때문 --> overfitting

 현업에서 실제로 분류작업을 많이 함. 사람이 하나하나 하기 힘든 것들
	e.g., 데이팅 앱 사진 분류 작업. 사람인가 아닌가, 여자인가 남자인가 등등. cs문의 들어왔을 때 문의의 카테고리 나누는 것


카테고리 정확도 높이기를 위한 도구
[Amazon Mechanical Turk](https://www.mturk.com/)
[[미국에서 스타트업 하기 (14)] 글로벌 고객 조사를 위한 유용한 도구 Mechanical Turk (MTurk)](http://www.venturesquare.net/3045)


## 실습 노트 코드 요약
1. 청원 카테고리 분류
~~~
# 나눔글꼴 설치
!apt install fonts-nanum

# Plotnine 패키지 설치
!pip install plotnine

# 기본 글꼴 변경
import matplotlib as mpl
mpl.font_manager._rebuild()
mpl.pyplot.rc('font', family='NanumBarunGothic')

# 레티나 디스플레이 지원
%config InlineBackend.figure_format = 'retina'

import pandas as pd
import numpy as np
import re
print(pd.__version__)
print(np.__version__)
~~~

2. 데이터 로드하기
~~~
# 크롤링해 온 국민청원 데이터를 판다스를 통해 읽어옵니다.
petitions = pd.read_csv('https://s3.ap-northeast-2.amazonaws.com/data10902/petition/petition.csv', parse_dates=['start', 'end'])
# 데이터의 크기가 어느정도인지 봅니다.
petitions.shape
# 전체 데이터 중 투표가 1000건 이상인 데이터를 기준으로 가져옵니다. 아웃라이어 데이터 제거를 위해 10만건 이상 데이터도 제거합니다.
df = petitions.loc[(petitions['votes'] > 1000) & (petitions['votes'] < 100000)].copy()
df.shape
/category_count = df['category'].value_counts()
category_count
%matplotlib inline 
category_count.plot(kind='bar')
# 예측값과 실제값 비교를 위해 컬럼을 하나 더 생성합니다.
df['category_pred'] = df['category'].copy()
# 첫 번째 인덱스를 가져와 봅니다.
sample_index = df.iloc[0][0]
sample_index
~~~

3. 전처리 하기
~~~
def preprocessing(text):
    # 개행문자 제거
   text= str(text)
   text = re.sub('\\\\n', ' ', text)
    # 특수문자 제거
    # 특수문자나 이모티콘 등은 때로는 의미를 갖기도 하지만 여기에서는 제거했습니다.
    # text = re.sub('[?.,;:|\)*~`’!^\-_+<>@\#$%&-=#}※]', '', text)
    # 한글, 영문, 숫자만 남기고 모두 제거하도록 합니다.
    # text = re.sub('[^가-힣ㄱ-ㅎㅏ-ㅣa-zA-Z0-9]', ' ', text)
    # 한글, 영문만 남기고 모두 제거하도록 합니다.
    text = re.sub('[^가-힣ㄱ-ㅎㅏ-ㅣa-zA-Z]', ' ', text)
    return text
# 불용어 제거
def remove_stopwords(text):
    tokens = text.split(' ')
    stops = ['수', '현', '있는', '있습니다', '그', '년도', '합니다', '하는', '및', '제', '할', '하고', '더', '대한', '한', '그리고', '월', '저는', '없는', '입니다', '등', '일', '많은', '이런', '것은', '왜','같은', '같습니다', '없습니다', '위해', '한다']
    meaningful_words = [w for w in tokens if not w in stops]
    return ' '.join(meaningful_words)
# 샘플데이터에 적용
pre_sample_content = preprocessing(sample_content)
pre_sample_content = remove_stopwords(pre_sample_content)
~~~

4. 학습세트와 테스트세트 만들기
~~~
#학습세트와 테스트세트를 7:3의 비율로 나눠 줍니다.
split_count = int(df.shape[0] * 0.7)
split_count
#카테고리
df_train_category_value = pd.DataFrame(df_train['category'].value_counts())
df_train_category_percent = pd.DataFrame(df_train['category'].value_counts(normalize=True))
df_train_category_value.merge(df_train_category_percent, left_index=True, right_index=True)
df_test_category_value = pd.DataFrame(df_test['category'].value_counts())
df_test_category_percent = pd.DataFrame(df_test['category'].value_counts(normalize=True))
df_test_category_value.merge(df_test_category_percent, left_index=True, right_index=True)
df_train_category_value.plot(kind='bar')
df_test_category_value.plot(kind='bar')
~~~

5. 단어 벡터화 하기
~~~
from sklearn.feature_extraction.text import CountVectorizer

vectorizer = CountVectorizer(analyzer = 'word', # 캐릭터 단위로 벡터화 할 수도 있습니다.
                             tokenizer = None, # 토크나이저를 따로 지정해 줄 수도 있습니다.
                             preprocessor = None, # 전처리 도구
                             stop_words = None, # 불용어 nltk등의 도구를 사용할 수도 있습니다.
                             min_df = 2, # 토큰이 나타날 최소 문서 개수로 오타나 자주 나오지 않는 특수한 전문용어 제거에 좋다. 
                             ngram_range=(1, 3), # BOW의 단위를 1~3개로 지정합니다.
                             max_features = 2000 # 만들 피처의 수, 단어의 수가 된다.
                            )
vectorizer
~~~

6. 랜덤 포레스트로 학습시키기


[랜덤 포레스트  공식문서](http://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html)
~~~
# 학습에 사용할 y_label 을 넣어줍니다.
# 어떤 분야의 청원인지 예측할 것이기 때문에 category를 넣어줍니다.
y_label = df_train['category']
~~~

7. 학습이 잘 되었는지 평가하기
~~~
from sklearn.model_selection import KFold
from sklearn.model_selection import cross_val_score
k_fold = KFold(n_splits=5, shuffle=True, random_state=0)

scoring = 'accuracy'
%time score = cross_val_score(forest, train_feature_vector, y_label, cv=k_fold, n_jobs=-1, scoring=scoring)
score

round(np.mean(score)*100,2)
~~~

8. 예측
~~~
# 테스트 데이터를 넣고 예측합니다.
y_pred = forest.predict(test_feature_vector)
y_pred[:3]

# 예측 결과를 저장하기 위해 데이터프레임에 담아 줍니다.
output = pd.DataFrame(data={'category_pred':y_pred})
output.head()

# 0과 1이 어떻게 집계 되었는지 확인합니다.
# 실제 데이터에는 답변 대상 건이 있는데 없는 것으로 예측되었
output['category_pred'].value_counts()

df_test['category_pred'] = y_pred

df_test['pred_diff'] = 0
df_test['pred_diff'] = (df_test['category'] == df_test['category_pred'] ) == 1
df_test['pred_diff'] = df_test['pred_diff'].astype(int)
df_test.head()

# 맞게 예측한 청원은 1, 틀린 예측은 0으로 표기되었습니다.
pred_diff = df_test['pred_diff'].value_counts()
pred_diff

print('전체 {}건의 데이터 중 {}건 예측'.format(y_pred.shape[0], pred_diff[1])) 

acc = ( pred_diff[1] / y_pred.shape[0] )*100 
print('예측 비율 {}'.format(acc))

# 제대로 예측한 카테고리 데이터를 봅니다.
predict_correct = df_test.loc[df_test['pred_diff'] == 1]
predict_correct.head()

predict_incorrect = df_test.loc[df_test['pred_diff'] == 0].copy()
predict_incorrect.head()

predict_incorrect_value = predict_incorrect['category'].value_counts()
predict_incorrect_value

# 잘못 예측한 카테고리 중 인권/성평등 카테고리가 가장 많습니다.
predict_incorrect_value.plot(kind='bar')
~~~
