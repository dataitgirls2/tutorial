
### Tutorial_0813_kaggle Titanic

#### 1. 스프레드시트로 캐글 참여하기

1) 캐글 사이트에서 train.csv와 test.csv를 다운로드 받습니다.

2) 구글 스프레드 시트에 titanic 폴더를 하나 생성하고 파일을 올립니다.

3) train.csv 시트를 열어 봅니다.

4) train.csv 시트에서 피봇테이블로 각 항목별 생존률을 봅니다.

예) 성별, 등급, 가족, 탑승지 등에 따라 생존률을 봅니다.

![img](https://lh5.googleusercontent.com/LfwnMQ6pQZUI2GtL2c7C3-ojjpwGApNzwLLVfZ6oIoqC60qp31eP6Rwz1SA9E6rREQ75sf8H3gmlbzta4l9BXyS2lfC_ffzDRRkjrbfFYZ2L8dtajA2u8Psxt1zvyG-RyCJfo6DT)

![img](https://lh6.googleusercontent.com/A6s5d8YAUkj2ZfTNfX-NQprR3ahGeDlw3HNVSzD34dKpdyKSArJqLJf1aQYMVYty51-lgZxrKB-ApCQ822Lt1nHomdHZR7fbCh3XHSTQCnuH6Kkccg2YnZXFwEYQTVPZ9lRDFvZi)

5) train.csv 의 피봇테이블에서 본 데이터를 바탕으로

6) test.csv 파일에서 스프레드시트의 수식기호를 사용해 생존자를 구해봅니다. 

생존했을 때 1, 그렇지 못했을 때 0으로 표시합니다. 예) =IF(E3="female", 1, 0)전체행에 수식을 적용하는 것은 수식이 있는 첫번째 셀의 작은 네모에 마우스를 가져가면 + 표시가 생깁니다. 이 표시를 더블클릭하면 전체 행에 수식이 적용됩니다. 

![img](https://lh5.googleusercontent.com/CU1FSXUrXH0OjbvJx-v55rHZmI_atQ1GC5vNBk6eAff4XlMZzNz4bTEu-hkW3HpKIkGgGfhIMaMBuD8WPxN3N6i3XniNjNDCiDJjoB3DUWtBWdfQw2o-kv54dgz2VmwnsSHwTdJs)

7) submission 파일을 만들어 제출합니다. 이때, submission 파일의 형식은 캐글 사이트에서 다운로드 받은 것과 같은 형식이어야 합니다. 다음과 같은 2개의 컬럼을 가지며 컬럼명이 일치해야 합니다.PassengerIdSurvived

8) 새로운 시트를 만들어 수식을 제외한 값만 붙여넣기 해서 제출 파일을 만듭니다.![img](https://lh4.googleusercontent.com/MC_00j3ylufe1w5iYSdZqKTheU3XH70jTzRiXpzZK0rb4yk-k5i1IbHwQt3zME5v9FkU2pCr1j39qXoKHmk7hYO2Pdrmfi41OI4-_63l5nOrlF16q7PI2IFUgTuMEevldwG594f0)예) 제출파일 형태로 csv로 저장

![img](https://lh3.googleusercontent.com/JxUyUcUXrO79aSB_1BJNxnch0XaUDid1419Rh0aFDnSjhQYV-ZysgEnoueEYmBljJsy20TMUNPmbL2HQZXOdfzagnYWxXLDDYfHaVFUUyahRsnn-FDYBLInNX_-3mp6xKbgH6fDn)
9) 조별 실습을 통해 데이터를 보고 생존률을 머신러닝이 아닌 집단지성을 통해 해결해 봅니다.

10) 스프레드시트의 수식으로 집단지성을 구현해 보고 캐글에 제출하고 어느 조가 가장 높은 점수를 얻는지 공유해 보도록 해요.


### 2. 파이썬으로 분석하기

엑셀로 분석했던 과정을 똑같이 파이썬으로 해봅니다.

1. train, test.csv 파일불러오기
2. 엑셀에서 했던 것 처럼 pivot 테이블 만들어 분석해 보기
3. 파이썬 코드로 엑셀에서 했던 과정을 똑같이 해보기
4. submission.csv 파일 생성해서 제출해 보기



```python
# 성별에 따른 생존률
# 생존여부가 1과 0으로 되어 있기 때문에 평균을 구하면 생존률이 된다.
# groupby로 구하기train.groupby('Sex')[['Survived']].mean()
# pivot_table로 구하기train.pivot_table(values=['Survived'], index=['Sex'], aggfunc=np.mean)
# 성별, 선실등급별 생존률
train.pivot_table('Survived', ['Sex', 'Pclass'], aggfunc=np.mean)
# 캐글 제출용 파일 만들기submission.to_csv('submissions/submission.csv', index=False)
```

### 3. 실습 내용 정리


```python
import pandas as pd
import numpy as np
```

#### 데이터를 불러오기


```python
train = pd.read_csv('data/train.csv')
test = pd.read_csv('data/test.csv')
print(train.shape)
print(test.shape)
```

#### 데이터 요약하기 (describe과 info)


```python
train.describe()
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
      <th>PassengerId</th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Fare</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>891.000000</td>
      <td>891.000000</td>
      <td>891.000000</td>
      <td>714.000000</td>
      <td>891.000000</td>
      <td>891.000000</td>
      <td>891.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>446.000000</td>
      <td>0.383838</td>
      <td>2.308642</td>
      <td>29.699118</td>
      <td>0.523008</td>
      <td>0.381594</td>
      <td>32.204208</td>
    </tr>
    <tr>
      <th>std</th>
      <td>257.353842</td>
      <td>0.486592</td>
      <td>0.836071</td>
      <td>14.526497</td>
      <td>1.102743</td>
      <td>0.806057</td>
      <td>49.693429</td>
    </tr>
    <tr>
      <th>min</th>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>0.420000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>223.500000</td>
      <td>0.000000</td>
      <td>2.000000</td>
      <td>20.125000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>7.910400</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>446.000000</td>
      <td>0.000000</td>
      <td>3.000000</td>
      <td>28.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>14.454200</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>668.500000</td>
      <td>1.000000</td>
      <td>3.000000</td>
      <td>38.000000</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>31.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>891.000000</td>
      <td>1.000000</td>
      <td>3.000000</td>
      <td>80.000000</td>
      <td>8.000000</td>
      <td>6.000000</td>
      <td>512.329200</td>
    </tr>
  </tbody>
</table>
</div>




```python
train.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 891 entries, 0 to 890
    Data columns (total 12 columns):
    PassengerId    891 non-null int64
    Survived       891 non-null int64
    Pclass         891 non-null int64
    Name           891 non-null object
    Sex            891 non-null object
    Age            714 non-null float64
    SibSp          891 non-null int64
    Parch          891 non-null int64
    Ticket         891 non-null object
    Fare           891 non-null float64
    Cabin          204 non-null object
    Embarked       889 non-null object
    dtypes: float64(2), int64(5), object(5)
    memory usage: 83.6+ KB
    

#### 성별에 따른 생존률
생존여부가 1과 0으로 되어 있기 때문에 평균을 구하면 생존률이 됩니다.


```python
train.groupby('Sex')[['Survived']].mean()
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
      <th>Survived</th>
    </tr>
    <tr>
      <th>Sex</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>female</th>
      <td>0.742038</td>
    </tr>
    <tr>
      <th>male</th>
      <td>0.188908</td>
    </tr>
  </tbody>
</table>
</div>




```python
train.pivot_table(values=['Survived'], index=['Sex'], aggfunc=np.mean)
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
      <th>Survived</th>
    </tr>
    <tr>
      <th>Sex</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>female</th>
      <td>0.742038</td>
    </tr>
    <tr>
      <th>male</th>
      <td>0.188908</td>
    </tr>
  </tbody>
</table>
</div>




```python
train.pivot_table(index=['Sex'])
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
      <th>Age</th>
      <th>Fare</th>
      <th>Parch</th>
      <th>PassengerId</th>
      <th>Pclass</th>
      <th>SibSp</th>
      <th>Survived</th>
    </tr>
    <tr>
      <th>Sex</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>female</th>
      <td>27.915709</td>
      <td>44.479818</td>
      <td>0.649682</td>
      <td>431.028662</td>
      <td>2.159236</td>
      <td>0.694268</td>
      <td>0.742038</td>
    </tr>
    <tr>
      <th>male</th>
      <td>30.726645</td>
      <td>25.523893</td>
      <td>0.235702</td>
      <td>454.147314</td>
      <td>2.389948</td>
      <td>0.429809</td>
      <td>0.188908</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 성별의 4분위수를 보는것은 의미는 없습니다. 다만, describe를 써서 다음과 같은 형태의 분석도 가능하다는 예시입니다.
train.groupby('Sex')[['Survived']].describe()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="8" halign="left">Survived</th>
    </tr>
    <tr>
      <th></th>
      <th>count</th>
      <th>mean</th>
      <th>std</th>
      <th>min</th>
      <th>25%</th>
      <th>50%</th>
      <th>75%</th>
      <th>max</th>
    </tr>
    <tr>
      <th>Sex</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>female</th>
      <td>314.0</td>
      <td>0.742038</td>
      <td>0.438211</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>male</th>
      <td>577.0</td>
      <td>0.188908</td>
      <td>0.391775</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 성별, 선실등급별 생존률
train.pivot_table('Survived', ['Sex', 'Pclass'], aggfunc=np.mean)
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
      <th></th>
      <th>Survived</th>
    </tr>
    <tr>
      <th>Sex</th>
      <th>Pclass</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="3" valign="top">female</th>
      <th>1</th>
      <td>0.968085</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.921053</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.500000</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">male</th>
      <th>1</th>
      <td>0.368852</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.157407</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.135447</td>
    </tr>
  </tbody>
</table>
</div>




```python
train.groupby('Sex')[['Survived']].mean()
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
      <th>Survived</th>
    </tr>
    <tr>
      <th>Sex</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>female</th>
      <td>0.742038</td>
    </tr>
    <tr>
      <th>male</th>
      <td>0.188908</td>
    </tr>
  </tbody>
</table>
</div>



#### 엑셀에서 했던것과 동일하게 여성일 때 생존했다고 가정하고 Survived 데이터를 채워줍니다.


```python
test['Survived'] = (test.Sex == 'female') & (test.Age > 0) & (test.Embarked )
```


```python
test.head()
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
      <th>PassengerId</th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>892</td>
      <td>False</td>
      <td>3</td>
      <td>Kelly, Mr. James</td>
      <td>male</td>
      <td>34.5</td>
      <td>0</td>
      <td>0</td>
      <td>330911</td>
      <td>7.8292</td>
      <td>NaN</td>
      <td>Q</td>
    </tr>
    <tr>
      <th>1</th>
      <td>893</td>
      <td>True</td>
      <td>3</td>
      <td>Wilkes, Mrs. James (Ellen Needs)</td>
      <td>female</td>
      <td>47.0</td>
      <td>1</td>
      <td>0</td>
      <td>363272</td>
      <td>7.0000</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
    <tr>
      <th>2</th>
      <td>894</td>
      <td>False</td>
      <td>2</td>
      <td>Myles, Mr. Thomas Francis</td>
      <td>male</td>
      <td>62.0</td>
      <td>0</td>
      <td>0</td>
      <td>240276</td>
      <td>9.6875</td>
      <td>NaN</td>
      <td>Q</td>
    </tr>
    <tr>
      <th>3</th>
      <td>895</td>
      <td>False</td>
      <td>3</td>
      <td>Wirz, Mr. Albert</td>
      <td>male</td>
      <td>27.0</td>
      <td>0</td>
      <td>0</td>
      <td>315154</td>
      <td>8.6625</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
    <tr>
      <th>4</th>
      <td>896</td>
      <td>True</td>
      <td>3</td>
      <td>Hirvonen, Mrs. Alexander (Helga E Lindqvist)</td>
      <td>female</td>
      <td>22.0</td>
      <td>1</td>
      <td>1</td>
      <td>3101298</td>
      <td>12.2875</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
  </tbody>
</table>
</div>




```python
test.isnull().sum()
```




    PassengerId      0
    Survived         0
    Pclass           0
    Name             0
    Sex              0
    Age             86
    SibSp            0
    Parch            0
    Ticket           0
    Fare             1
    Cabin          327
    Embarked         0
    dtype: int64




```python
test['Survived'].value_counts()
```




    False    291
    True     127
    Name: Survived, dtype: int64



#### pandas의 데이터프레임 복사에 대해 이해합니다.
참고 Understanding SettingwithCopyWarning in pandas


```python
submission = test[['PassengerId', 'Survived']].copy()
submission.head()
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
      <th>PassengerId</th>
      <th>Survived</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>892</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>893</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2</th>
      <td>894</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>895</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>896</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>



#### 제출형태에 맞는 데이터 타입으로 변경해 줍니다.


```python
submission['Survived'] = submission['Survived'].astype(int)
```


```python
submission.head()
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
      <th>PassengerId</th>
      <th>Survived</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>892</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>893</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>894</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>895</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>896</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>



#### csv 형태로 파일을 만듭니다.


```python
# %mkdir submissions
```


```python
submission.to_csv('submissions/submission.csv', index=False)
```

#### 탐색기 혹은 Finder에서 제출파일을 얻어 제출하기 위해 경로를 얻어옵니다.


```python
%pwd
```
