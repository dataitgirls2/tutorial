
# Pandas로 국민청원 데이터 분석하기

## Pandas와 NumPy를 import해 옵니다.


```python
import pandas as pd
import numpy as np
```

## csv 데이터를 불러 옵니다.


```python
# AWS 서버에 파일이 있기에 계속 클라우드로 사용 가능. csv : ,로 값들이 구분된 데이터 파일
df = pd.read_csv('https://s3.ap-northeast-2.amazonaws.com/data10902/petition/petition.csv', parse_dates=['start', 'end'])
```

## 읽어온 데이터가 몇 행 몇 열인지 봅니다.


```python
df.shape
```




    (211108, 8)



## 일부 데이터 미리 보기
* 상단 5개의 데이터를 불러옵니다.


```python
# article_id가 1-20까지는 개발자가 테스트용도로 쓰다가 데이터베이스 복구를 하지 않아서 첫 글이 21이 됨
df.head(5)
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
      <th>article_id</th>
      <th>start</th>
      <th>end</th>
      <th>answered</th>
      <th>votes</th>
      <th>category</th>
      <th>title</th>
      <th>content</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>21</td>
      <td>2017-08-19</td>
      <td>2017-11-17</td>
      <td>0</td>
      <td>9</td>
      <td>안전/환경</td>
      <td>스텔라 데이지호에 대한 제안입니다.</td>
      <td>스텔라 데이지호에 대한 제안입니다.\n3월31일 스텔라 데이지호가 침몰하고 5달째가...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>22</td>
      <td>2017-08-19</td>
      <td>2017-11-17</td>
      <td>0</td>
      <td>17</td>
      <td>기타</td>
      <td>비리제보처를 만들어주세요.</td>
      <td>현 정부에 국민들이 가장 원하는 것은 부패척결입니다.  우리 사회에 각종 비리들이 ...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>23</td>
      <td>2017-08-19</td>
      <td>2017-09-03</td>
      <td>0</td>
      <td>0</td>
      <td>미래</td>
      <td>제2의 개성공단</td>
      <td>만일 하시는 대통령님 및 각 부처 장관님,주무관님들 안녕하세요!!\n전남 목포에서 ...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>24</td>
      <td>2017-08-19</td>
      <td>2017-08-26</td>
      <td>0</td>
      <td>53</td>
      <td>일자리</td>
      <td>공공기관 무조건적인 정규직전환을 반대합니다.</td>
      <td>현정부에서 정규직 일자리를 늘리는 것에 찬성합니다. 그런데 공공기관 비정규직들은 인...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25</td>
      <td>2017-08-19</td>
      <td>2017-09-03</td>
      <td>0</td>
      <td>0</td>
      <td>미래</td>
      <td>제2의 개성공단</td>
      <td>만일 하시는 대통령님 및 각 부처 장관님,주무관님들 안녕하세요!!\n전남 목포에서 ...</td>
    </tr>
  </tbody>
</table>
</div>



* 하단 3개의 데이터를 불러옵니다.


```python
df.tail(3)
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
      <th>article_id</th>
      <th>start</th>
      <th>end</th>
      <th>answered</th>
      <th>votes</th>
      <th>category</th>
      <th>title</th>
      <th>content</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>211105</th>
      <td>272626</td>
      <td>2018-06-16</td>
      <td>2018-07-16</td>
      <td>0</td>
      <td>2</td>
      <td>일자리</td>
      <td>선거참여원  70000원 노동법 위반아닌가요</td>
      <td>최저임금 올려주시고 선거지원 아르바이트 사원은 식대 빼고 70000원 말이 되는건가...</td>
    </tr>
    <tr>
      <th>211106</th>
      <td>272627</td>
      <td>2018-06-16</td>
      <td>2018-07-16</td>
      <td>0</td>
      <td>12</td>
      <td>기타</td>
      <td>우체국 집배원 도 대한민국 국민입니다</td>
      <td>우체국 직원분들도 대한민국 국민입니다\n글을 보며 읽고 읽는데 말도 안되는 소리 하...</td>
    </tr>
    <tr>
      <th>211107</th>
      <td>272628</td>
      <td>2018-06-16</td>
      <td>2018-07-16</td>
      <td>0</td>
      <td>5</td>
      <td>정치개혁</td>
      <td>역적 최순실의 모든 재산을 몰수할 것이며, 역적 박근혜를 즉각 사사(죽일 죄인을 예...</td>
      <td>이 청원자는 천주교인이며, 세례명은 "남종삼세례자요한"입니다.\n일전에도 수많은 국...</td>
    </tr>
  </tbody>
</table>
</div>



## 결측치가 있는지 확인해 봅니다.


```python
# null값이 있는 경우를 count 시켜줌. 현재는 크롤링을 잘해서 0이 나옴
df.isnull().sum()
```




    article_id    0
    start         0
    end           0
    answered      0
    votes         0
    category      0
    title         0
    content       1
    dtype: int64



## 데이터 요약하기
* 어떤 컬럼이 있고 어떤 타입인지 출력해 봅니다.


```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 211108 entries, 0 to 211107
    Data columns (total 8 columns):
    article_id    211108 non-null int64
    start         211108 non-null datetime64[ns]
    end           211108 non-null datetime64[ns]
    answered      211108 non-null int64
    votes         211108 non-null int64
    category      211108 non-null object
    title         211108 non-null object
    content       211107 non-null object
    dtypes: datetime64[ns](2), int64(3), object(3)
    memory usage: 12.9+ MB
    

* 데이터 타입만 따로 뽑아 봅니다.


```python
df.dtypes
```




    article_id             int64
    start         datetime64[ns]
    end           datetime64[ns]
    answered               int64
    votes                  int64
    category              object
    title                 object
    content               object
    dtype: object



* 컬럼명만 따로 추출해 봅니다.


```python
df.columns
```




    Index(['article_id', 'start', 'end', 'answered', 'votes', 'category', 'title',
           'content'],
          dtype='object')



* 수치형 데이터에 대한 요약을 봅니다.


```python
# 수치형 데이터에 대해서만 보여줌
# df.describe? 하면, 도움말 기능이 나오므로 활용함
df.describe()
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
      <th>article_id</th>
      <th>answered</th>
      <th>votes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>211108.000000</td>
      <td>211108.000000</td>
      <td>211108.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>126829.174299</td>
      <td>0.000128</td>
      <td>146.589082</td>
    </tr>
    <tr>
      <th>std</th>
      <td>79425.907385</td>
      <td>0.011308</td>
      <td>4587.667181</td>
    </tr>
    <tr>
      <th>min</th>
      <td>21.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>54803.750000</td>
      <td>0.000000</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>126518.500000</td>
      <td>0.000000</td>
      <td>3.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>193946.250000</td>
      <td>0.000000</td>
      <td>10.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>272628.000000</td>
      <td>1.000000</td>
      <td>714875.000000</td>
    </tr>
  </tbody>
</table>
</div>



* 카테고리(object) 형태의 데이터에 대한 요약을 봅니다.


```python
# object 중 가장 많이 나오는 데이터를 보여줌
# count와 unique가 일치하지 않는 것은 도배글이 많다는 것을 의미함
df.describe(include=np.object)
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
      <th>category</th>
      <th>title</th>
      <th>content</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>211108</td>
      <td>211108</td>
      <td>211107</td>
    </tr>
    <tr>
      <th>unique</th>
      <td>17</td>
      <td>176185</td>
      <td>196019</td>
    </tr>
    <tr>
      <th>top</th>
      <td>정치개혁</td>
      <td>이명박 출국금지</td>
      <td>이명박 출국금지</td>
    </tr>
    <tr>
      <th>freq</th>
      <td>38909</td>
      <td>3018</td>
      <td>597</td>
    </tr>
  </tbody>
</table>
</div>



## 답변대상 청원 보기
20만건 이상 투표를 받으면 답변 대상 청원이 됩니다.<br/>20만건 이상 투표를 받은 청원의 갯수를 세어보세요.


```python
df_20 = df.loc[df['votes'] > 200000]
df_20.shape
```




    (43, 14)




```python
df_20.category.value_counts()
```




    인권/성평등         11
    안전/환경           5
    문화/예술/체육/언론     5
    기타              5
    외교/통일/국방        3
    정치개혁            3
    성장동력            2
    경제민주화           2
    보건복지            2
    행정              1
    반려동물            1
    교통/건축/국토        1
    미래              1
    육아/교육           1
    Name: category, dtype: int64




```python
df_20[['title', 'content']].head(3)
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
      <th>content</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1752</th>
      <td>청소년이란 이유로 보호법을 악용하는 잔인무도한 청소년들이 늘어나고있습니다. 반드시 ...</td>
      <td>안녕하십니까. 청소년보호법이란 명목하에 나쁜짓을 일삼는 청소년들이 너무나 많아지고 ...</td>
    </tr>
    <tr>
      <th>10894</th>
      <td>조두순 출소반대</td>
      <td>제발 조두순 재심다시해서 무기징역으로 해야됩니다!!!</td>
    </tr>
    <tr>
      <th>18111</th>
      <td>낙태죄 폐지와 자연유산 유도약(미프진) 합법화 및 도입을 부탁드립니다.</td>
      <td>안녕하세요. 존경하는 대통령님 의원님\n낙태죄 폐지를 청원합니다.\n현재 대한민국은...</td>
    </tr>
  </tbody>
</table>
</div>



* 20만건 이상 투표를 받은 상위 5개의 청원을 head()를 통해 출력해 보세요.


```python
df_20_loc = df.loc[df_20]
df_20_loc.sort_values(by='votes', ascending=False).head()
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
      <th>article_id</th>
      <th>start</th>
      <th>end</th>
      <th>answered</th>
      <th>votes</th>
      <th>category</th>
      <th>title</th>
      <th>content</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>208597</th>
      <td>269548</td>
      <td>2018-06-13</td>
      <td>2018-07-13</td>
      <td>0</td>
      <td>714875</td>
      <td>외교/통일/국방</td>
      <td>제주도 불법 난민 신청 문제에 따른 난민법, 무사증 입국, 난민신청허가 폐지/개헌 ...</td>
      <td>2012년 난민법 제정으로 인해 외국인은 한달 무비자로 입국할 수 있으나 난민신청자...</td>
    </tr>
    <tr>
      <th>10894</th>
      <td>10949</td>
      <td>2017-09-06</td>
      <td>2017-12-05</td>
      <td>1</td>
      <td>615354</td>
      <td>미래</td>
      <td>조두순 출소반대</td>
      <td>제발 조두순 재심다시해서 무기징역으로 해야됩니다!!!</td>
    </tr>
    <tr>
      <th>118970</th>
      <td>142600</td>
      <td>2018-02-19</td>
      <td>2018-03-21</td>
      <td>1</td>
      <td>614127</td>
      <td>문화/예술/체육/언론</td>
      <td>김보름, 박지우 선수의 자격박탈과 적폐 빙상연맹의 엄중 처벌을 청원합니다</td>
      <td>오늘 여자 단체전 팀추월에서 김보름, 박지우 선수는 팀전인데도 불구하고 개인의 영달...</td>
    </tr>
    <tr>
      <th>183791</th>
      <td>230552</td>
      <td>2018-05-11</td>
      <td>2018-06-10</td>
      <td>1</td>
      <td>419006</td>
      <td>인권/성평등</td>
      <td>여성도 대한민국 국민입니다. 성별 관계없는 국가의 보호를 요청합니다.</td>
      <td>최근 홍대 누드크로키 모델의 불법촬영 사건이 있었습니다.\n사건은 굉장히 빠르게 처...</td>
    </tr>
    <tr>
      <th>91882</th>
      <td>105105</td>
      <td>2018-01-20</td>
      <td>2018-02-19</td>
      <td>1</td>
      <td>360905</td>
      <td>외교/통일/국방</td>
      <td>나경원 의원 평창올림픽 위원직을 파면시켜주세요</td>
      <td>안녕하세요. 청와대에 청원은 처음해 보는 경험인지라 조금은 어색하고 뭐라 말을 시작...</td>
    </tr>
  </tbody>
</table>
</div>



* 20만건 이상 투표를 받은 청원을 별도의 컬럼을 만들어 줍니다. 컬럼 이름은 `answer`로 합니다.


```python
df['answer'] = (df['votes'] > 200000) == 1
```

* df 데이터프레임의 크기를 다시 찍어 보세요. 컬럼 하나가 늘었나요?


```python
df.shape
```




    (211108, 9)




```python
df.dtypes
```




    article_id             int64
    start         datetime64[ns]
    end           datetime64[ns]
    answered               int64
    votes                  int64
    category              object
    title                 object
    content               object
    answer                  bool
    dtype: object



* 새로 생성해 준 answer의 타입은 boolean 타입입니다. int로 변경해 보세요.


```python
df['answer'] = df['answer'].astype('int')
```

* 답변대상 청원중 아직 답변되지 않은 청원의 수를 계산해 보세요.


```python
df['answer_diff'] = df['answer'] - df['answered']
df['answer_diff'].sum()
```




    16



## 답변 대상 청원 중 투표를 가장 많이 받은 것


```python
answered_df = df.loc[df['answer'] == 1]
answered_df.sort_values('votes', ascending=False).head(5)
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
      <th>article_id</th>
      <th>start</th>
      <th>end</th>
      <th>answered</th>
      <th>votes</th>
      <th>category</th>
      <th>title</th>
      <th>content</th>
      <th>answer</th>
      <th>answer_diff</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>208597</th>
      <td>269548</td>
      <td>2018-06-13</td>
      <td>2018-07-13</td>
      <td>0</td>
      <td>714875</td>
      <td>외교/통일/국방</td>
      <td>제주도 불법 난민 신청 문제에 따른 난민법, 무사증 입국, 난민신청허가 폐지/개헌 ...</td>
      <td>2012년 난민법 제정으로 인해 외국인은 한달 무비자로 입국할 수 있으나 난민신청자...</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>10894</th>
      <td>10949</td>
      <td>2017-09-06</td>
      <td>2017-12-05</td>
      <td>1</td>
      <td>615354</td>
      <td>미래</td>
      <td>조두순 출소반대</td>
      <td>제발 조두순 재심다시해서 무기징역으로 해야됩니다!!!</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>118970</th>
      <td>142600</td>
      <td>2018-02-19</td>
      <td>2018-03-21</td>
      <td>1</td>
      <td>614127</td>
      <td>문화/예술/체육/언론</td>
      <td>김보름, 박지우 선수의 자격박탈과 적폐 빙상연맹의 엄중 처벌을 청원합니다</td>
      <td>오늘 여자 단체전 팀추월에서 김보름, 박지우 선수는 팀전인데도 불구하고 개인의 영달...</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>183791</th>
      <td>230552</td>
      <td>2018-05-11</td>
      <td>2018-06-10</td>
      <td>1</td>
      <td>419006</td>
      <td>인권/성평등</td>
      <td>여성도 대한민국 국민입니다. 성별 관계없는 국가의 보호를 요청합니다.</td>
      <td>최근 홍대 누드크로키 모델의 불법촬영 사건이 있었습니다.\n사건은 굉장히 빠르게 처...</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>91882</th>
      <td>105105</td>
      <td>2018-01-20</td>
      <td>2018-02-19</td>
      <td>1</td>
      <td>360905</td>
      <td>외교/통일/국방</td>
      <td>나경원 의원 평창올림픽 위원직을 파면시켜주세요</td>
      <td>안녕하세요. 청와대에 청원은 처음해 보는 경험인지라 조금은 어색하고 뭐라 말을 시작...</td>
      <td>1</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>



## 어느 분야의 청원이 가장 많이 들어왔는지?
pandas의 value_counts로 특정 컬럼의 데이터를 그룹화하여 카운된 숫자를 볼 수 있습니다.<br/>
어느 분야의 청원이 가장 많이 들어왔는지 찾아보세요.


```python
category = pd.DataFrame(df['category'].value_counts()).reset_index()
category.columns = ['category', 'counts']
category
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
      <th>category</th>
      <th>counts</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>정치개혁</td>
      <td>38909</td>
    </tr>
    <tr>
      <th>1</th>
      <td>기타</td>
      <td>26101</td>
    </tr>
    <tr>
      <th>2</th>
      <td>인권/성평등</td>
      <td>21156</td>
    </tr>
    <tr>
      <th>3</th>
      <td>안전/환경</td>
      <td>16326</td>
    </tr>
    <tr>
      <th>4</th>
      <td>육아/교육</td>
      <td>14415</td>
    </tr>
    <tr>
      <th>5</th>
      <td>외교/통일/국방</td>
      <td>13960</td>
    </tr>
    <tr>
      <th>6</th>
      <td>보건복지</td>
      <td>11656</td>
    </tr>
    <tr>
      <th>7</th>
      <td>행정</td>
      <td>10957</td>
    </tr>
    <tr>
      <th>8</th>
      <td>일자리</td>
      <td>10566</td>
    </tr>
    <tr>
      <th>9</th>
      <td>문화/예술/체육/언론</td>
      <td>10464</td>
    </tr>
    <tr>
      <th>10</th>
      <td>교통/건축/국토</td>
      <td>9936</td>
    </tr>
    <tr>
      <th>11</th>
      <td>미래</td>
      <td>9427</td>
    </tr>
    <tr>
      <th>12</th>
      <td>경제민주화</td>
      <td>8427</td>
    </tr>
    <tr>
      <th>13</th>
      <td>성장동력</td>
      <td>4006</td>
    </tr>
    <tr>
      <th>14</th>
      <td>반려동물</td>
      <td>2121</td>
    </tr>
    <tr>
      <th>15</th>
      <td>저출산/고령화대책</td>
      <td>1767</td>
    </tr>
    <tr>
      <th>16</th>
      <td>농산어촌</td>
      <td>914</td>
    </tr>
  </tbody>
</table>
</div>



## 청원이 가장 많이 들어 온 날은 언제인지 정렬해 보세요.


```python
start_df = pd.DataFrame(df['start'].value_counts()).reset_index()
start_df.columns = ['start', 'counts']
start_df = start_df.sort_values('counts', ascending=False)
print('청원 집계: {}일'.format(start_df.shape[0]))
start_df.head()
```

    청원 집계: 302일
    




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
      <th>start</th>
      <th>counts</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2017-11-11</td>
      <td>9623</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2017-09-05</td>
      <td>5952</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2018-01-11</td>
      <td>3368</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2018-02-06</td>
      <td>2631</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2017-11-09</td>
      <td>2487</td>
    </tr>
  </tbody>
</table>
</div>



## 피봇 테이블로 투표를 가장 많이 받은 분야를 찾아보세요.


```python
petitions_unique = pd.pivot_table(df, index=['category'], aggfunc=np.sum)
petitions_best = petitions_unique.sort_values(by='votes', \
                                              ascending=False).reset_index()
petitions_best
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
      <th>category</th>
      <th>answer</th>
      <th>answer_diff</th>
      <th>answered</th>
      <th>article_id</th>
      <th>votes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>인권/성평등</td>
      <td>11</td>
      <td>2</td>
      <td>9</td>
      <td>2493639392</td>
      <td>5845308</td>
    </tr>
    <tr>
      <th>1</th>
      <td>정치개혁</td>
      <td>3</td>
      <td>2</td>
      <td>1</td>
      <td>4919346825</td>
      <td>3056164</td>
    </tr>
    <tr>
      <th>2</th>
      <td>문화/예술/체육/언론</td>
      <td>5</td>
      <td>1</td>
      <td>4</td>
      <td>1468972986</td>
      <td>3045253</td>
    </tr>
    <tr>
      <th>3</th>
      <td>기타</td>
      <td>5</td>
      <td>4</td>
      <td>1</td>
      <td>3301112938</td>
      <td>2925659</td>
    </tr>
    <tr>
      <th>4</th>
      <td>안전/환경</td>
      <td>5</td>
      <td>3</td>
      <td>2</td>
      <td>1962647358</td>
      <td>2582819</td>
    </tr>
    <tr>
      <th>5</th>
      <td>보건복지</td>
      <td>2</td>
      <td>0</td>
      <td>2</td>
      <td>1443526799</td>
      <td>2520214</td>
    </tr>
    <tr>
      <th>6</th>
      <td>외교/통일/국방</td>
      <td>3</td>
      <td>2</td>
      <td>1</td>
      <td>1995048554</td>
      <td>2333560</td>
    </tr>
    <tr>
      <th>7</th>
      <td>육아/교육</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1496759705</td>
      <td>2045960</td>
    </tr>
    <tr>
      <th>8</th>
      <td>행정</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1462132268</td>
      <td>1160841</td>
    </tr>
    <tr>
      <th>9</th>
      <td>경제민주화</td>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>1158820895</td>
      <td>1108587</td>
    </tr>
    <tr>
      <th>10</th>
      <td>교통/건축/국토</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1351506721</td>
      <td>1097841</td>
    </tr>
    <tr>
      <th>11</th>
      <td>반려동물</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>287424420</td>
      <td>937316</td>
    </tr>
    <tr>
      <th>12</th>
      <td>미래</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1098639377</td>
      <td>854037</td>
    </tr>
    <tr>
      <th>13</th>
      <td>성장동력</td>
      <td>2</td>
      <td>0</td>
      <td>2</td>
      <td>502705526</td>
      <td>673795</td>
    </tr>
    <tr>
      <th>14</th>
      <td>일자리</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1503640375</td>
      <td>590816</td>
    </tr>
    <tr>
      <th>15</th>
      <td>저출산/고령화대책</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>204606590</td>
      <td>86210</td>
    </tr>
    <tr>
      <th>16</th>
      <td>농산어촌</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>124122599</td>
      <td>81748</td>
    </tr>
  </tbody>
</table>
</div>



## 투표를 가장 많이 받은 날은 언제일까요?


```python
petitions_start = pd.pivot_table(df, index=['start'], aggfunc=np.sum)
votes_df = petitions_start.sort_values(by='votes', ascending=False)
votes_df.loc[petitions_start['votes'] > 350000]
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
      <th>answer</th>
      <th>answer_diff</th>
      <th>answered</th>
      <th>article_id</th>
      <th>votes</th>
    </tr>
    <tr>
      <th>start</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-06-13</th>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>146187973</td>
      <td>786157</td>
    </tr>
    <tr>
      <th>2018-02-19</th>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>99332898</td>
      <td>701520</td>
    </tr>
    <tr>
      <th>2017-09-06</th>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>22268570</td>
      <td>648209</td>
    </tr>
    <tr>
      <th>2018-02-23</th>
      <td>2</td>
      <td>0</td>
      <td>2</td>
      <td>168561151</td>
      <td>608530</td>
    </tr>
    <tr>
      <th>2018-05-18</th>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>190599564</td>
      <td>574483</td>
    </tr>
    <tr>
      <th>2018-05-11</th>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>119082098</td>
      <td>556549</td>
    </tr>
    <tr>
      <th>2018-05-25</th>
      <td>2</td>
      <td>2</td>
      <td>0</td>
      <td>217699031</td>
      <td>514253</td>
    </tr>
    <tr>
      <th>2018-04-17</th>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>232499699</td>
      <td>446950</td>
    </tr>
    <tr>
      <th>2018-05-02</th>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>204023320</td>
      <td>445493</td>
    </tr>
    <tr>
      <th>2017-09-03</th>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>404415</td>
      <td>433356</td>
    </tr>
    <tr>
      <th>2018-06-14</th>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>204240095</td>
      <td>403351</td>
    </tr>
    <tr>
      <th>2018-01-20</th>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>99071361</td>
      <td>399683</td>
    </tr>
    <tr>
      <th>2017-11-17</th>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>23752225</td>
      <td>393348</td>
    </tr>
    <tr>
      <th>2017-11-24</th>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>80814983</td>
      <td>392782</td>
    </tr>
    <tr>
      <th>2018-03-24</th>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>96422371</td>
      <td>385480</td>
    </tr>
    <tr>
      <th>2018-03-03</th>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>94454042</td>
      <td>380016</td>
    </tr>
    <tr>
      <th>2018-01-15</th>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>106053634</td>
      <td>376187</td>
    </tr>
    <tr>
      <th>2018-04-16</th>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>168625159</td>
      <td>369318</td>
    </tr>
    <tr>
      <th>2018-01-25</th>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>129153668</td>
      <td>364926</td>
    </tr>
  </tbody>
</table>
</div>



## 청원을 많이 받은 날 VS 투표를 많이 받은 날에 대해 각각 상위 5개 목록을 추출해 봅니다. 
이때, title, content는 안 나와도 됩니다.


```python
# 두 개의 데이터프레임을 합치기 위해 인덱스를 생성한다.
votes_df = votes_df.reset_index()
hottest_day_df = start_df.merge(votes_df, on='start', how='left')
hottest_day_df.sort_values('counts', ascending=False)[:5]
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
      <th>start</th>
      <th>counts</th>
      <th>answer</th>
      <th>answer_diff</th>
      <th>answered</th>
      <th>article_id</th>
      <th>votes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2017-11-11</td>
      <td>9623</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>348559310</td>
      <td>85074</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2017-09-05</td>
      <td>5952</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>38414241</td>
      <td>48808</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2018-01-11</td>
      <td>3368</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>291069195</td>
      <td>44570</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2018-02-06</td>
      <td>2631</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>342371897</td>
      <td>83038</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2017-11-09</td>
      <td>2487</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>73459579</td>
      <td>34774</td>
    </tr>
  </tbody>
</table>
</div>




```python
hottest_day_df.sort_values('votes', ascending=False)[:5]
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
      <th>start</th>
      <th>counts</th>
      <th>answer</th>
      <th>answer_diff</th>
      <th>answered</th>
      <th>article_id</th>
      <th>votes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>181</th>
      <td>2018-06-13</td>
      <td>542</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>146187973</td>
      <td>786157</td>
    </tr>
    <tr>
      <th>119</th>
      <td>2018-02-19</td>
      <td>698</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>99332898</td>
      <td>701520</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2017-09-06</td>
      <td>2121</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>22268570</td>
      <td>648209</td>
    </tr>
    <tr>
      <th>30</th>
      <td>2018-02-23</td>
      <td>1135</td>
      <td>2</td>
      <td>0</td>
      <td>2</td>
      <td>168561151</td>
      <td>608530</td>
    </tr>
    <tr>
      <th>81</th>
      <td>2018-05-18</td>
      <td>806</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>190599564</td>
      <td>574483</td>
    </tr>
  </tbody>
</table>
</div>



## 시계열 데이터 보기
* 월별 청원수를 집계해 보세요.


```python
df['start_month'] = df['start'].dt.month
df['start_day'] = df['start'].dt.day
df['start_hour'] = df['start'].dt.hour
df['start_dow'] = df['start'].dt.dayofweek
df.shape
```




    (211108, 14)



* 청원이 가장 많이 들어온 달은 언제인가요?
* 요일별 청원 수는 어떻게 되나요?


```python
crypto = df[( df.title.str.find('가상화폐') != -1 ) | ( df.content.str.find('가상화폐') != -1  )]
crypto.shape
```




    (7773, 14)




```python
crypto.head()
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
      <th>article_id</th>
      <th>start</th>
      <th>end</th>
      <th>answered</th>
      <th>votes</th>
      <th>category</th>
      <th>title</th>
      <th>content</th>
      <th>answer</th>
      <th>answer_diff</th>
      <th>start_month</th>
      <th>start_day</th>
      <th>start_hour</th>
      <th>start_dow</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>12781</th>
      <td>12841</td>
      <td>2017-09-08</td>
      <td>2017-12-07</td>
      <td>0</td>
      <td>3</td>
      <td>성장동력</td>
      <td>가상전자화폐를 인정하고 규제해야합니다</td>
      <td>가상전자화폐\n흔히 코인이라 불리는 비생산적이고 소모적이며\n시장을 혼란케 하고 산...</td>
      <td>0</td>
      <td>0</td>
      <td>9</td>
      <td>8</td>
      <td>0</td>
      <td>4</td>
    </tr>
    <tr>
      <th>19325</th>
      <td>19575</td>
      <td>2017-10-06</td>
      <td>2017-11-05</td>
      <td>0</td>
      <td>5</td>
      <td>성장동력</td>
      <td>ICO 전면금지에 대한 입장</td>
      <td>정부는 9월 29일 김용범 금융위원회 부위원장 주재로 &lt;가상통화 관계기관 합동TF&gt;...</td>
      <td>0</td>
      <td>0</td>
      <td>10</td>
      <td>6</td>
      <td>0</td>
      <td>4</td>
    </tr>
    <tr>
      <th>20874</th>
      <td>21277</td>
      <td>2017-10-15</td>
      <td>2017-11-14</td>
      <td>0</td>
      <td>3906</td>
      <td>미래</td>
      <td>대통령님에게 전하는 지부상소(持斧上疏)입니다.   -블록체인 기술에 대한 이야기-</td>
      <td>지부상소(持斧上疏)를 이야기할 만큼 간절하게 원합니다.\n이 글이 문재인 대통령님께...</td>
      <td>0</td>
      <td>0</td>
      <td>10</td>
      <td>15</td>
      <td>0</td>
      <td>6</td>
    </tr>
    <tr>
      <th>20911</th>
      <td>21327</td>
      <td>2017-10-15</td>
      <td>2017-11-14</td>
      <td>0</td>
      <td>3</td>
      <td>경제민주화</td>
      <td>가상화폐 투기 광풍을 막아주세요</td>
      <td>가상화폐 규제 어떻게 해야 하나 ?\n이제 우리 앞에 놓여진 사회적 이슈가 되어\n...</td>
      <td>0</td>
      <td>0</td>
      <td>10</td>
      <td>15</td>
      <td>0</td>
      <td>6</td>
    </tr>
    <tr>
      <th>26541</th>
      <td>27765</td>
      <td>2017-11-08</td>
      <td>2017-12-08</td>
      <td>0</td>
      <td>1</td>
      <td>경제민주화</td>
      <td>가상화폐 투자대행회사의 무분별한 수수료 바로잡아주세요</td>
      <td>가상화폐 ico로 대리업무를 대행해주고 5-30% 수수료를 책정하고 계약서나 기타 ...</td>
      <td>0</td>
      <td>0</td>
      <td>11</td>
      <td>8</td>
      <td>0</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>




```python
crypto['category'].value_counts()
```




    경제민주화          1945
    미래             1879
    성장동력           1398
    기타              984
    정치개혁            870
    행정              338
    일자리             108
    인권/성평등           65
    안전/환경            52
    외교/통일/국방         42
    교통/건축/국토         31
    문화/예술/체육/언론      25
    보건복지             13
    저출산/고령화대책         8
    육아/교육             8
    반려동물              5
    농산어촌              2
    Name: category, dtype: int64




```python
import re
p = r'.*(돌봄|아이|초등|보육).*'
care = df[df['title'].str.match(p) |
           df['content'].str.match(p, flags=re.MULTILINE)]
care.shape
```




    (25735, 14)



## 위 분석 외에 각자 해보고 싶은 분석을 해보세요.


```python
from plotnine import *

(ggplot(df)
 + aes('category')
 + geom_bar(fill='green')
 + theme(text=element_text(family='NanumBarunGothic'),
        axis_text_x=element_text(rotation=60))
)
```

    /Users/corazzon/codes/jupyter/lib/python3.6/site-packages/statsmodels/compat/pandas.py:56: FutureWarning: The pandas.core.datetools module is deprecated and will be removed in a future version. Please use the pandas.tseries module instead.
      from pandas.core import datetools
    


![png](output_59_1.png)





    <ggplot: (298888168)>




```python
!pip install plotnine
```
