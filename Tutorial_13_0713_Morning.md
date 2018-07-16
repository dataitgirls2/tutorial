## Pandas 기초
### 데이터 불러오기
pd.read_csv

### 데이터 요약하기
- info()
- describe()

### 데이터 프레임과 시리즈 객체 이해
- 데이터 프레임 : 행렬('조선왕' 과 같이 칼럼으로 된 인덱스가 있는 것)
- 시리즈 객체 : 벡터('혈액형' 과 같이 칼럼으로 된 인덱스가 없는 것)

### 데이터 시각화 하기

### 자료의 요약 과제를 통한 실습
- 자료의 요약 시트 불러오기 : df  함수로 만들어놓고 불러오도록 만듬
~~~python
!pip install --upgrade -q gspread

import pandas as pd

from google.colab import auth

auth.authenticate_user()

import gspread
from oauth2client.client import GoogleCredentials


def get_sheet(title, sheet_name):
  gc = gspread.authorize(GoogleCredentials.get_application_default())
  return gc.open(title).worksheet(sheet_name)
~~~
~~~python
# 자료의 요약에 있는 특정 시트를 불러옵니다.
# 1번 row를 0번 인덱스로 읽어오는 데, 0번 인덱스를 컬럼으로 지정해 주도록 했습니다.
# 그러면 스프레드시트에서 봤던 것 처럼 데이터프레임이 생성됩니다.
# def get_df(sheet_name):
#   sheet = get_sheet('자료의 요약', sheet_name)

#   # Create dataframe from the sheet
#   rows = sheet.get_all_values()
#   df = pd.DataFrame.from_records(rows)    

#   df.columns = df.iloc[0]    # 0번째 행은 열 이름
#   df = df.reindex(df.index.drop(0))
#   return df
~~~
~~~python
!pip install --upgrade -q gspread
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt 
import seaborn as sns
~~~
~~~python
def get_df(sheet_name, index=None):
    gc = pd.read_excel('자료의 요약.xlsx', sheet_name=sheet_name, header=0, index_col=index )
    df = pd.DataFrame(gc)
    return df
~~~
#### 혈액형
~~~python
df_blood = get_df('혈액형')
# 상위 5개의 데이터를 가져옵니다.
print(df_blood.shape)
df_blood.head()
~~~
- df.iloc[0] : 0번째컬럼을 가져오고
- 데이터 프레임의 맨 위에 0번째 컬럼은 데이터가 아니라 제목으로 지정해줌(그냥 불러오면 0 혈액형 , 1 A, 2 O, ..식으로 뜸)
~~~python
df = df.reindex(df.index.drop(0))
~~~
- df reindex : 인덱스 새로만들기
- df index drop : 기존 인덱스 0번은 버리고
- df_blood.shape : 행,열 표기
- df_blood.tail(5) : 끝에서 5개만 가져옴
- df_blood.info() : 정보를 보여줌



#### 조선왕

~~~python
# 데이터 타입을 int로 변경해 준다.
df_king['life'] = df_king['life'].astype(int)
df_king['period'] = df_king['period'].astype(int)
# 위와 describe() 했을 때의 정보가 다르다. 
# 수치형 데이터 일 때 count, mean, std, min/max, 사분위수를 보여준다.
df_king.describe()
~~~

~~~python
# 결측치를 보고 싶을 때 널값을 구해 본다.# 결측치를 보고 
df_king.isnull().sum()
~~~

~~~python
# 평균값만 본다.
df_king.mean()
~~~

~~~python
# 표준편차만 본다.# 표준편차만 본 
df_king.std()
~~~

~~~python
# 최대값만 본다. 효종이 나온 이유는 한글 중에 가장 뒤에 있기 때문
# life, period도 각 컬럼에서 최대값
df_king.max()
df_king['period'].max()
~~~

~~~python
df_king['life'].hist()
~~~



#### 타이타닉

~~~python
# 어떤 컬럼이 있는지 보여줍니다.
df_titanic.columns
~~~

~~~python
df_titanic['Class'].value_counts()
~~~




## 10  Minutes to pandas 한글번역 

### 목적

- 해당 문서를 번역함으로서 판다스를 더 잘 이해하기 위함입니다.
- 전체 문서를 함께 번역하는 작업을 통해 협업을 경험해 보고 깃험을 좀 더 잘 활용해 보도록 합니다. 
- 다른 조의 문서를 리뷰하면서 익혀봅니다. 이 때 오타나 문법오류 추가하면 좋을만한 내용이 있다면 개선해 봅니다.
- 깃헙 페이지로 공개해서 판다스를 공부하는 사람들에게도 도움을 주도록 해요.
- 오픈소스에 기여하는 방법을 간접적으로 체험해 봅니다.


### 실습 및 과제 실습용 저장소 : https://github.com/dataitgirls2/10minutes2pandas0

1. 10minutes2pandas 리포를 포크합니다. 포크한 저장소를 클론합니다.
   - git clone git@github.com:본인의깃헙ID/10minutes2pandas.git
   - cd 10minutes2pandas 로 클론 받은 폴더로 이동합니다
2. git checkout 조별브랜치명 각자의 조별 브랜치로 이동합니다. 
3. 해당 브래치에 마스터 브랜치의 최신 내용을 가져와서 작업하도록 합니다.

- git pull --rebase origin master

4. index.inpynb 파일을 열어 각자 조에서 맡은 부분을 코딩 및 번역하고 서령을 추가 합니다. 

- 해당셀에서 a 를 누르면 위에추가 /  b를 누르면 아래로 추가 
- 쉬프트 + 엔터 : 해당 내용생성된다. 
- 엔터 : 해당내용을 수정한다

4. 조별로 번역과정이 끝나면 각자의 브랜치에 push 하고 pull request를 보냅니다. 
5. 변경된 조에서 변경 내용을 확인하고 merge 합니다. 
