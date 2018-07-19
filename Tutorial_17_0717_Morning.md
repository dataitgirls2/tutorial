
# Pandas 10분 완성

이 소개서는 주로 신규 사용자를 대상으로 한 판다스에 대한 간략한 소개입니다. 더 복잡한 방법은 [Cookbook](https://pandas.pydata.org/pandas-docs/stable/cookbook.html#cookbook) 에서 볼 수 있습니다.


일반적으로 다음과 같이 가져옵니다.


```python
# pd가 아니어도 편한 이름으로 pandas의 별칭 만들기
import pandas as pd
```


```python
# as = alias.
import numpy as np
```


```python
# Pandas에 내장된 기능들은 Pandas의 것이 아니라, matplotlib의 것. 
# 한글 폰트, 속성(색깔 등)를 사용하기 위해서도 matplotlib이 필요. matplotlib은 matlab 기반으로 제작.
# matplotlib.org 굉장히 복잡함. 그것을 더 쓰기 쉽게 한번 더 맵핑해 둔 것이 seaborn.seaborn이 matplotlib 기반으로 만들어짐
# 캐글러 설문조사 결과는 대부분 seaborn으로 수행한 것. 
# plotnine : ggplot 문법 기반으로 만들어짐
import matplotlib.pyplot as plt
```


```python
!pip install plotnine
```

    Collecting plotnine
    [?25l  Downloading https://files.pythonhosted.org/packages/3a/68/cf39dfde4e9fd886703621e3393cd8103cb48d5ecc95b8f048ec148e53a6/plotnine-0.3.0-py2.py3-none-any.whl (3.4MB)
    [K    100% |████████████████████████████████| 3.4MB 6.2MB/s 
    [?25hRequirement already satisfied: pandas>=0.21.0 in /usr/local/lib/python3.6/dist-packages (from plotnine) (0.22.0)
    Requirement already satisfied: patsy>=0.4.1 in /usr/local/lib/python3.6/dist-packages (from plotnine) (0.5.0)
    Requirement already satisfied: matplotlib>=2.1.0 in /usr/local/lib/python3.6/dist-packages (from plotnine) (2.1.2)
    Collecting scipy>=1.0.0 (from plotnine)
    [?25l  Downloading https://files.pythonhosted.org/packages/a8/0b/f163da98d3a01b3e0ef1cab8dd2123c34aee2bafbb1c5bffa354cc8a1730/scipy-1.1.0-cp36-cp36m-manylinux1_x86_64.whl (31.2MB)
    [K    100% |████████████████████████████████| 31.2MB 962kB/s 
    [?25hRequirement already satisfied: six in /usr/local/lib/python3.6/dist-packages (from plotnine) (1.11.0)
    Collecting mizani>=0.4.1 (from plotnine)
    [?25l  Downloading https://files.pythonhosted.org/packages/52/01/8a3b4c6e45749674a1e5241174b4b63cd6435125e124bec275f3e02c96ac/mizani-0.4.6-py2.py3-none-any.whl (65kB)
    [K    100% |████████████████████████████████| 71kB 13.3MB/s 
    [?25hRequirement already satisfied: numpy in /usr/local/lib/python3.6/dist-packages (from plotnine) (1.14.5)
    Requirement already satisfied: statsmodels>=0.8.0 in /usr/local/lib/python3.6/dist-packages (from plotnine) (0.8.0)
    Requirement already satisfied: pytz>=2011k in /usr/local/lib/python3.6/dist-packages (from pandas>=0.21.0->plotnine) (2018.5)
    Requirement already satisfied: python-dateutil>=2 in /usr/local/lib/python3.6/dist-packages (from pandas>=0.21.0->plotnine) (2.5.3)
    Requirement already satisfied: cycler>=0.10 in /usr/local/lib/python3.6/dist-packages (from matplotlib>=2.1.0->plotnine) (0.10.0)
    Requirement already satisfied: pyparsing!=2.0.4,!=2.1.2,!=2.1.6,>=2.0.1 in /usr/local/lib/python3.6/dist-packages (from matplotlib>=2.1.0->plotnine) (2.2.0)
    Collecting palettable (from mizani>=0.4.1->plotnine)
    [?25l  Downloading https://files.pythonhosted.org/packages/56/8a/84537c0354f0d1f03bf644b71bf8e0a50db9c1294181905721a5f3efbf66/palettable-3.1.1-py2.py3-none-any.whl (77kB)
    [K    100% |████████████████████████████████| 81kB 6.2MB/s 
    [?25hInstalling collected packages: scipy, palettable, mizani, plotnine
      Found existing installation: scipy 0.19.1
        Uninstalling scipy-0.19.1:
          Successfully uninstalled scipy-0.19.1
    Successfully installed mizani-0.4.6 palettable-3.1.1 plotnine-0.3.0 scipy-1.1.0
    

# Object Creation (객체 생성)

[데이터 구조 소개 섹션](https://pandas.pydata.org/pandas-docs/stable/dsintro.html#dsintro)을 참조하십시오.

판다스는 값을 가지고 있는 리스트를 통해 [시리즈](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.Series.html#pandas.Series)를 만들고, 인덱스를 기본값으로 불러올 것입니다.


```python
# np.nan은 null값(공백값)을 numpy로 생성한다는 뜻.
# pd는 임포트에서 선언한 것을 반복한 것.
s = pd.Series([1,3,5,np.nan,6,8])
```


```python
# 각 인덱스에 vector data로 불러온다
s
```




    0    1.0
    1    3.0
    2    5.0
    3    NaN
    4    6.0
    5    8.0
    dtype: float64



datetime 인덱스와 레이블이 있는 열이있는 NumPy 배열을 전달하여 데이터 프레임 만들기 :


```python
# date_range는 인자값을 6으로 하여 6개의 날짜를 생성
dates = pd.date_range('20130101', periods=6)
```


```python
dates
```




    DatetimeIndex(['2013-01-01', '2013-01-02', '2013-01-03', '2013-01-04',
                   '2013-01-05', '2013-01-06'],
                  dtype='datetime64[ns]', freq='D')




```python
# np.random.randn(6,4)는 numpy에서 랜덤하게 숫자를 생성하라는 뜻. 
# 랜덤한 숫자를 6,4로 행렬 지정하여 6개의 행에 4개의 컬럼 들어가게 테이블을 만들기
# 벡터와 행렬의 raw 값이 항상 맞아야 한다. 인자값 6개 해줬고, column 4개. 6x4=24.
df = pd.DataFrame(np.random.randn(6,4), index=dates, columns=list('ABCD'))
```


```python
# 데이터를 불러오고 shage를 찍어서 데이터를 확인할 수 있음
df
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>0.112723</td>
      <td>-0.405223</td>
      <td>0.609430</td>
      <td>-0.922518</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>0.172926</td>
      <td>1.258247</td>
      <td>-0.503618</td>
      <td>-1.444750</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>-0.349227</td>
      <td>-0.251152</td>
      <td>-0.271460</td>
      <td>-1.325293</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>0.829756</td>
      <td>-1.406244</td>
      <td>-0.458275</td>
      <td>1.680711</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>1.004529</td>
      <td>0.611415</td>
      <td>-0.751275</td>
      <td>-1.133753</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>0.624723</td>
      <td>0.580754</td>
      <td>-0.006615</td>
      <td>-0.215584</td>
    </tr>
  </tbody>
</table>
</div>



시리즈와 같은 것으로 바뀔 수 있는 객체의 dict로 구성된 dataframe을 만듭니다.


```python
# pd에 Timestamp = 날짜 형식으로 넣어주라는 뜻
# 하나하나의 raw들이 다 시리즈 데이터.
# C열 같은 경우, 데이터타입이 float으로 지정되어 있다. 만약 int로 했으면 소수점 안 붙었을 것. 
# 다음 줄은 int로 지정.
# E는 카테고리컬 데이터.
# foo. 데이터타입까지 다 지정. A는 1하고 .을찍었으니 float으로 자동 적용되어 있음.
# 데이터 프레임 생성. 각각의 컬럼 A~F는 시리즈 데이터이다.
df2 = pd.DataFrame({'A' : 1.,
                    'B' : pd.Timestamp('20130102'),
                    'C' : pd.Series(1,index=list(range(4)),dtype='float32'),
                    'D' : np.array([3] * 4,dtype='int32'),
                    'E' : pd.Categorical(["test","train","test","train"]),
                    'F' : 'foo' })
```


```python
df2
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>E</th>
      <th>F</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.0</td>
      <td>2013-01-02</td>
      <td>1.0</td>
      <td>3</td>
      <td>test</td>
      <td>foo</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1.0</td>
      <td>2013-01-02</td>
      <td>1.0</td>
      <td>3</td>
      <td>train</td>
      <td>foo</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1.0</td>
      <td>2013-01-02</td>
      <td>1.0</td>
      <td>3</td>
      <td>test</td>
      <td>foo</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1.0</td>
      <td>2013-01-02</td>
      <td>1.0</td>
      <td>3</td>
      <td>train</td>
      <td>foo</td>
    </tr>
  </tbody>
</table>
</div>



 DataFrame 결과의 행은 다양한 데이터타입(dtypes)으로 구성됩니다.  


```python
# 데이터 타입에 따라 요약값을 다르게 찍어주므로 데이터 타입을 확인하는 것이 매우 중요
df2.dtypes
```




    A           float64
    B    datetime64[ns]
    C           float32
    D             int32
    E          category
    F            object
    dtype: object



IPython을 이용하고 계시다면, 열 이름에 대한(공용속성은 물론) tap완성 기능(tap completion)이 자동으로 활성화됩니다. 다음은 완성될 속성에 대한 부분집합(subset)입니다. 


```python
# df2.describe?를 사용하면 사용할 수 있는 명령어 볼 수 있음
df2.<TAB>
```


      File "<ipython-input-16-915637deb483>", line 1
        df2.<TAB>
            ^
    SyntaxError: invalid syntax
    


**IPython에서 실행하면 다음과 같은 결과값이 나온다.**
```
df2.A                  df2.bool
df2.abs                df2.boxplot
df2.add                df2.C
df2.add_prefix         df2.clip
df2.add_suffix         df2.clip_lower
df2.align              df2.clip_upper
df2.all                df2.columns
df2.any                df2.combine
df2.append             df2.combine_first
df2.apply              df2.compound
df2.applymap           df2.consolidate
df2.D
```



보시다시피, A,B,C그리고 D 열이 탭 자동완성기능으로 실행됩니다. 물론 E도 있습니다. 나머지 속성들은 간결하게 잘라버렸습니다. 


# Viewing Data(데이터 확인하기)

**Viewing Data 데이터 확인하기**

[Basic Section](https://pandas.pydata.org/pandas-docs/stable/basics.html#basics)을 봅니다.

데이터프레임의 맨 윗 줄과 마지막 줄을 확인하고 싶을 때 .head()와 .tail()을 입력합니다. 

괄호()안에는 숫자가 들어갈 수도 있고 안 들어갈 수도 있습니다. 
숫자가 들어간다면, 윗/마지막 줄의 특정 줄을 불러올 수 있습니다. 
숫자가 들어가지 않다면, 기본값인 5로 처리됩니다.

(예시) 
df.tail(3) - 끝에서 마지막 3줄을 불러옴
df.tail() - 끝에서 마지막 5줄 불러옴


```python
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>-0.414296</td>
      <td>-0.197622</td>
      <td>-1.085198</td>
      <td>-0.023086</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>1.310316</td>
      <td>-1.236729</td>
      <td>2.279797</td>
      <td>-1.959987</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>0.723715</td>
      <td>0.573125</td>
      <td>-1.069190</td>
      <td>1.555839</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>0.371333</td>
      <td>-0.613136</td>
      <td>-0.128201</td>
      <td>0.211691</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>-1.711670</td>
      <td>-1.473291</td>
      <td>0.996679</td>
      <td>0.299594</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.tail(3)
```

인덱스(Index), 열(Column) 그리고 NumPy 데이터에 대한 세부 정보를 보려면 .index, .columns, .values를 입력합니다. 



```python
# index 값을 볼 수 있음
df.index
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-1-08c554537916> in <module>()
    ----> 1 df.index
    

    NameError: name 'df' is not defined



```python
# column을 찍어보고 싶을 때. 엑셀 파일을 보면 첫번째 column에 제목같은 것이 써있거나 한 경우가 있음
# 그럴 때 자료가 시작되는 column부터를 적용시킬 수 있음
# 자료의 요약 수업때도 맨 윗 줄을 drop 시키고 가져왔었는데 그 부분 생각해 보기.
df.columns
```




    Index(['A', 'B', 'C', 'D'], dtype='object')




```python
# 각 열이 의미하는 것은 series
df.values
```




    array([[-0.41429646, -0.19762242, -1.08519754, -0.02308603],
           [ 1.31031598, -1.23672901,  2.27979739, -1.95998692],
           [ 0.72371532,  0.5731255 , -1.06918956,  1.55583868],
           [ 0.37133325, -0.61313642, -0.12820145,  0.21169111],
           [-1.71166962, -1.47329121,  0.99667917,  0.29959364],
           [ 0.64706968, -0.05617486, -1.39994375, -0.4958439 ]])



데이터의 대략적인 통계적 정보를 보려면 [describe() ](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.describe.html#pandas.DataFrame.describe)를 입력합니다.  



```python
# 개요를 살펴볼 수 있음
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>6.000000</td>
      <td>6.000000</td>
      <td>6.000000</td>
      <td>6.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>0.154411</td>
      <td>-0.500638</td>
      <td>-0.067676</td>
      <td>-0.068632</td>
    </tr>
    <tr>
      <th>std</th>
      <td>1.072910</td>
      <td>0.767186</td>
      <td>1.446407</td>
      <td>1.150207</td>
    </tr>
    <tr>
      <th>min</th>
      <td>-1.711670</td>
      <td>-1.473291</td>
      <td>-1.399944</td>
      <td>-1.959987</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>-0.217889</td>
      <td>-1.080831</td>
      <td>-1.081196</td>
      <td>-0.377654</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>0.509201</td>
      <td>-0.405379</td>
      <td>-0.598696</td>
      <td>0.094303</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>0.704554</td>
      <td>-0.091537</td>
      <td>0.715459</td>
      <td>0.277618</td>
    </tr>
    <tr>
      <th>max</th>
      <td>1.310316</td>
      <td>0.573125</td>
      <td>2.279797</td>
      <td>1.555839</td>
    </tr>
  </tbody>
</table>
</div>



데이터를 전치합니다.


```python
# #column과 row를 바꿈
df.T
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
      <th>2013-01-01 00:00:00</th>
      <th>2013-01-02 00:00:00</th>
      <th>2013-01-03 00:00:00</th>
      <th>2013-01-04 00:00:00</th>
      <th>2013-01-05 00:00:00</th>
      <th>2013-01-06 00:00:00</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>-0.016348</td>
      <td>0.923949</td>
      <td>-0.740104</td>
      <td>1.509731</td>
      <td>0.149121</td>
      <td>0.337573</td>
    </tr>
    <tr>
      <th>B</th>
      <td>-1.039512</td>
      <td>-0.600859</td>
      <td>0.415755</td>
      <td>-1.800477</td>
      <td>0.466604</td>
      <td>0.828969</td>
    </tr>
    <tr>
      <th>C</th>
      <td>2.217217</td>
      <td>-0.046872</td>
      <td>0.952118</td>
      <td>-1.223772</td>
      <td>-1.467452</td>
      <td>1.369278</td>
    </tr>
    <tr>
      <th>D</th>
      <td>0.349947</td>
      <td>-1.890090</td>
      <td>-0.591175</td>
      <td>-0.272443</td>
      <td>0.739277</td>
      <td>-0.305797</td>
    </tr>
  </tbody>
</table>
</div>



축 별로 정렬합니다.


```python
# ascending=False 역순으로 보여주는 뜻
# axis=0으로 하면, 행(Row)을 기준으로 정렬된다. 0은 행(Row), 1은 열(Column). 
# ascending 순차적으로 정렬. descending 역순으로 정렬. 
# ascending=False 는 D->C->B->A
df.sort_index(axis=1, ascending=False)
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
      <th>D</th>
      <th>C</th>
      <th>B</th>
      <th>A</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>0.095868</td>
      <td>2.642896</td>
      <td>0.416627</td>
      <td>1.163115</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>0.525729</td>
      <td>-0.679141</td>
      <td>-0.879822</td>
      <td>0.587121</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>0.642380</td>
      <td>0.461575</td>
      <td>0.284343</td>
      <td>0.436873</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>0.206035</td>
      <td>1.956695</td>
      <td>-0.546474</td>
      <td>-0.947212</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>-0.115390</td>
      <td>0.580832</td>
      <td>-1.763954</td>
      <td>0.352037</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>2.257174</td>
      <td>1.528186</td>
      <td>-0.828983</td>
      <td>-0.171705</td>
    </tr>
  </tbody>
</table>
</div>



값 별로 정렬합니다.


```python
# 'B' column의 값을 중심으로 정렬
df.sort_values(by='B')
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-05</th>
      <td>0.352037</td>
      <td>-1.763954</td>
      <td>0.580832</td>
      <td>-0.115390</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>0.587121</td>
      <td>-0.879822</td>
      <td>-0.679141</td>
      <td>0.525729</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>-0.171705</td>
      <td>-0.828983</td>
      <td>1.528186</td>
      <td>2.257174</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>-0.947212</td>
      <td>-0.546474</td>
      <td>1.956695</td>
      <td>0.206035</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>0.436873</td>
      <td>0.284343</td>
      <td>0.461575</td>
      <td>0.642380</td>
    </tr>
    <tr>
      <th>2013-01-01</th>
      <td>1.163115</td>
      <td>0.416627</td>
      <td>2.642896</td>
      <td>0.095868</td>
    </tr>
  </tbody>
</table>
</div>



# Selection (선택)


주석(Note) : 선택과 설정을 위한 Python, Numpy의 표준화된 표현들이 직관적이며, 코드 작성을 위한 양방향 작업에 유용하지만 우리는 Pandas에 최적화된 데이터 접근 방법인 .at, .iat, .loc 및 .iloc 을 추천합니다. 

[데이터 인덱싱 및 선택](https://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing) 문서와 [다중 인덱싱 / 심화 인덱싱](https://pandas.pydata.org/pandas-docs/stable/advanced.html#advanced) 문서를 확인하십시오.

## Getting (데이터 얻기)

df.A 와 동일한 Series를 생성하는 단일 열을 선택합니다.


```python
# df Column 에서 A만 얻을 수 있음.
# 여러 개의 Columns 을 뽑고 싶을 경우에는 df [[‘A’,‘B’]]로 꺾쇠괄호로 한번 더 감싸줌. (pandas only)
df['A']
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-1-c31f9b0c4302> in <module>()
    ----> 1 df['A']
    

    NameError: name 'df' is not defined


행을 분할하는 [] 를 통해 선택합니다


```python
# index 0부터 시작하여, 3 전까지를 말함. 0, 1, 2를 포함. 
# df[:]를 하면 전체를 다 불러옴.
# df[3:] 3부터 끝까지 불러옴.
df[0:3]
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>0.395799</td>
      <td>1.324341</td>
      <td>0.153554</td>
      <td>-0.672920</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-0.303496</td>
      <td>-1.596556</td>
      <td>-0.920610</td>
      <td>-0.840386</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>0.677687</td>
      <td>0.204407</td>
      <td>0.256671</td>
      <td>-1.094652</td>
    </tr>
  </tbody>
</table>
</div>




```python
# index가 날짜로 되어 있을 경우 위와 같이 숫자로 뽑아올 수 있음
# 국민 청원 데이터는 index를 날짜로 지정할 수 없을 것. 고유값으로만 구성되어 있지 않기 때문. (날짜 중복 문제)
df['20130102':'20130104']
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-02</th>
      <td>-0.303496</td>
      <td>-1.596556</td>
      <td>-0.920610</td>
      <td>-0.840386</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>0.677687</td>
      <td>0.204407</td>
      <td>0.256671</td>
      <td>-1.094652</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>-1.109111</td>
      <td>-0.770913</td>
      <td>-0.330677</td>
      <td>-0.570009</td>
    </tr>
  </tbody>
</table>
</div>



## Selection by Label (Label 을 통한 선택)

[Label을 통한 선택](https://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-label)에서 더 많은 내용을 확인하세요.

라벨을 사용하여 횡단면을 얻는 방법입니다.


```python
df.loc[dates[0]]
```




    A    0.395799
    B    1.324341
    C    0.153554
    D   -0.672920
    Name: 2013-01-01 00:00:00, dtype: float64



라벨을 사용하여 여러 축(의 데이터)을 얻는 방법입니다.


```python
# :는 전체 데이터 중에서 A B 데이터만 추출
df.loc[:,['A','B']]
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
      <th>A</th>
      <th>B</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>0.395799</td>
      <td>1.324341</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-0.303496</td>
      <td>-1.596556</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>0.677687</td>
      <td>0.204407</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>-1.109111</td>
      <td>-0.770913</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>-0.223322</td>
      <td>0.305182</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>0.623582</td>
      <td>0.705459</td>
    </tr>
  </tbody>
</table>
</div>



양쪽 종단점을 포함한 라벨 슬라이싱을 봅시다.


```python
df.loc['20130102':'20130104', ['A','B']]
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
      <th>A</th>
      <th>B</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-02</th>
      <td>-0.303496</td>
      <td>-1.596556</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>0.677687</td>
      <td>0.204407</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>-1.109111</td>
      <td>-0.770913</td>
    </tr>
  </tbody>
</table>
</div>



반환되는 객체의 크기를 줄입니다.


```python
df.loc['20130102',['A','B']]
```




    A   -0.303496
    B   -1.596556
    Name: 2013-01-02 00:00:00, dtype: float64



스칼라 값을 얻습니다.


```python

df.loc[dates[0],'A']

```




    0.11272306638579893



스칼라 값을 더 빠르게 구하는 방법입니다. (앞선 method와 동일합니다)


```python
df.at[dates[0],'A']
```




    0.39579879602076895



## Selection by Position (위치로 선택하기)

자세한 내용은 [위치로 선택하기](https://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-integer)를 참고해주세요.

넘겨받은 정수의 위치로 선택하기:


```python
df.iloc[3]
```

넘파이/파이썬 작동 방식처럼 정수로 표기된 슬라이스로 선택하기:


```python
df.iloc[3:5,0:2]
```

넘파이/파이썬 작동 방식처럼 정수로 표기된 위치값을 기반으로 선택하기:


```python
df.iloc[[1,2,4],[0,2]]
```

행만 나누고 싶을 때:


```python
df.iloc[1:3,:]
```

열만 나누고 싶을 때:


```python
df.iloc[:,1:3]
```

값만 얻고 싶을 때:


```python
df.iloc[1,1]
```

스칼라 값을 빨리 얻고 싶을 때(위 방식과 동일):


```python
df.iat[1,1]
```

## Boolean Indexing (부울인덱싱)

선택한 데이터에 단일 열의 값을 사용합니다.


```python
df[df.A > 0]
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-1-4c1bb2a68b7c> in <module>()
    ----> 1 df[df.A > 0]
    

    NameError: name 'df' is not defined


부울 조건에 충족되는 데이터프레임에서 변수를 선택합니다.


```python
df[df > 0]
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-2-3990d321393d> in <module>()
    ----> 1 df[df > 0]
    

    NameError: name 'df' is not defined


필터링 방법인 [isin()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.Series.isin.html#pandas.Series.isin)을 사용합니다.


```python
df2 = df.copy()
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-3-5239123e9f27> in <module>()
    ----> 1 df2 = df.copy()
    

    NameError: name 'df' is not defined



```python
df2['E'] = ['one', 'one','two','three','four','three']
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-6-c2648a571dfc> in <module>()
    ----> 1 df2['E'] = ['one', 'one','two','three','four','three']
    

    NameError: name 'df2' is not defined



```python
df2
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-7-2068723f1203> in <module>()
    ----> 1 df2
    

    NameError: name 'df2' is not defined



```python
df2[df2['E'].isin(['two','four'])]
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-8-bdde5e490798> in <module>()
    ----> 1 df2[df2['E'].isin(['two','four'])]
    

    NameError: name 'df2' is not defined


## Setting (설정)
새로운 열을 날짜와 인덱스에 따라 자동적으로 줄이 맞춰지도록 설정합니다. 


```python
s1 = pd.Series([1,2,3,4,5,6], index=pd.date_range('20130102', periods=6))
```


```python
s1
```


```python
df['F'] = s1
```


라벨에 따라 값을 설정하고 싶다면 :


```python
df.at[dates[0],'A'] = 0
```




    DatetimeIndex(['2013-01-01', '2013-01-02', '2013-01-03', '2013-01-04',
                   '2013-01-05', '2013-01-06'],
                  dtype='datetime64[ns]', freq='D')



위치에 따라 값을 설정하고 싶다면 :


```python
df.iat[0,1] = 0
```

Numpy 배열로 할당하고 싶다면  :


```python
df.loc[:,'D'] = np.array([5] * len(df))
```

위 설정대로 작동한 결과입니다.


```python
df
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>-1.479995</td>
      <td>0.361202</td>
      <td>1.486119</td>
      <td>0.115256</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-0.221067</td>
      <td>0.487654</td>
      <td>0.938039</td>
      <td>-0.741746</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>0.729247</td>
      <td>-0.215760</td>
      <td>0.337932</td>
      <td>-1.177466</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>0.847000</td>
      <td>-0.118338</td>
      <td>0.038752</td>
      <td>-0.727101</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>-0.239768</td>
      <td>-0.581571</td>
      <td>0.884636</td>
      <td>0.134043</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>0.204809</td>
      <td>-0.082419</td>
      <td>0.846424</td>
      <td>-0.720843</td>
    </tr>
  </tbody>
</table>
</div>



설정된 where 작업입니다.


```python
df2 = df.copy()
```


```python
df2[df2 > 0] = -df2
```


```python
df2
```

# Missing Data(결측치)

pandas는 missing data(결측치)를 표현하기 위해 주로 np.nan 값을 사용합니다. 이 방법은 default(기본 설정)이지만 계산에는 포함되지 않습니다. [Missing Data section](https://pandas.pydata.org/pandas-docs/stable/missing_data.html#missing-data)을 참조하십시오.




Reindexing으로 지정된 축을 변경/추가/삭제할 수 있습니다. Reindexing은 데이터 복사본을 반환합니다.


```python
df1 = df.reindex(index=dates[0:4], columns=list(df.columns) + ['E'])
```


```python
df1.loc[dates[0]:dates[1],'E'] = 1
```


```python
df1
```

missing data(결측치)를 갖고 있는 행들을 지웁니다.


```python
df1.dropna(how='any')
```

missing data(결측치)를 채웁니다.


```python
df1.fillna(value=5)
```

값이 nan인 boolean mask 얻습니다.


```python
pd.isna(df1)
```

# Operation (연산)

[바이너리 작업의 기본 섹션](https://pandas.pydata.org/pandas-docs/stable/basics.html#basics-binop)을 참조하십시오.

## Stats(통계)

일반적으로 연산은 missing data(결측치)를 제외합니다.

서술적인 통계를 수행합니다.


```python
df.mean()
```

다른 축에서 동일한 작업을 수행합니다.


```python
df.mean(1)
```

차원이 다르고 정렬이 필요한 객체로 작업합니다. 또한 pandas는 지정된 차원을 따라 자동으로 브로드 캐스팅(역주 : broadcast란 numpy에서 유래한 용어로, n차원이나 스칼라 값으로 연산을 수행할 때 도출되는 결과의 규칙을 설명하는 것을 의미합니다.)됩니다.


```python
s = pd.Series([1,3,5,np.nan,6,8], index=dates).shift(2)
```


```python
s
```


```python
df.sub(s, axis='index')
```

## Apply (적용하기)

데이터에 기능을 적용합니다.


```python
df.apply(np.cumsum)
```


```python
df.apply(lambda x: x.max() - x.min())
```

## Histogramming (히스토그래밍)

더 많은 내용은 [Histogramming and Discretization (히스토그래밍과 이산화)](https://pandas.pydata.org/pandas-docs/stable/basics.html#basics-discretization)항목을 참조하십시오.


```python
s = pd.Series(np.random.randint(0, 7, size=10))
```


```python
s
```


```python
s.value_counts()
```




    8.0    1
    6.0    1
    5.0    1
    3.0    1
    1.0    1
    dtype: int64



## String Mathods (문자열 메서드)

Series 는 아래의 코드 스니펫에서처럼 배열의 각 요소를 쉽게 조작할 수 있도록 하는 문자열 처리 메서드 세트를 갖추고 있습니다. 주로 문자열에서의 패턴 매칭은 자동으로 [regular expressions (정규식)](https://docs.python.org/3/library/re.html)을 사용한다는 것을 유의하십시오. (그리고 가끔 어떤 경우에는 항상 정규식을 사용합니다.) 

더 많은 내용은 [Vectorized String Methods (벡터화된 문자열 메서드)](https://pandas.pydata.org/pandas-docs/stable/text.html#text-string-methods) 항목을 참조하십시오. 


```python
s = pd.Series(['A', 'B', 'C', 'Aaba', 'Baca', np.nan, 'CABA', 'dog', 'cat'])
```


```python
s.str.lower()
```


```python
df = pd.DataFrame(np.random.randn(6,4), index=dates, columns=list('ABCD'))
```


```python
df
```


```python
df['F'] = s1
```

# Merge (병합)

## Concat (연결)

Pandas는 join/merge 와 같은 병합작업의 경우 'concat()' 을 통해<br>
Series, DataFrame, Panel 객체를 index와 관계 대수 기능에 대한 다양한 유형의 논리로<br>
손쉽게 결합할 수 있는 다양한 기능을 제공합니다.

Merging 섹션을 봅시다. [Merging section](https://pandas.pydata.org/pandas-docs/stable/merging.html#merging) 

'concat()'으로 Pandas 객체를 연결(concatenating) 합니다. 


```python
df = pd.DataFrame(np.random.randn(10, 4))
```


```python
df
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
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.129203</td>
      <td>-0.237727</td>
      <td>-0.769031</td>
      <td>-1.964273</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1.040888</td>
      <td>1.448563</td>
      <td>-0.984106</td>
      <td>-0.099231</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-0.722966</td>
      <td>-1.198605</td>
      <td>-0.477420</td>
      <td>-0.265710</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-0.005394</td>
      <td>0.286019</td>
      <td>0.730833</td>
      <td>-0.473830</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1.231130</td>
      <td>-1.574169</td>
      <td>0.781478</td>
      <td>-0.159057</td>
    </tr>
    <tr>
      <th>5</th>
      <td>-1.417875</td>
      <td>-0.247297</td>
      <td>-0.580590</td>
      <td>1.369179</td>
    </tr>
    <tr>
      <th>6</th>
      <td>-0.905663</td>
      <td>0.641291</td>
      <td>0.266012</td>
      <td>-0.474489</td>
    </tr>
    <tr>
      <th>7</th>
      <td>0.196629</td>
      <td>1.592408</td>
      <td>0.017062</td>
      <td>-1.300836</td>
    </tr>
    <tr>
      <th>8</th>
      <td>0.034225</td>
      <td>0.032075</td>
      <td>-1.876997</td>
      <td>-1.712954</td>
    </tr>
    <tr>
      <th>9</th>
      <td>0.399283</td>
      <td>0.087454</td>
      <td>-0.134279</td>
      <td>-1.936356</td>
    </tr>
  </tbody>
</table>
</div>




```python
# break it into pieces
pieces = [df[:3], df[3:7], df[7:]]
pd.concat(pieces)
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
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.129203</td>
      <td>-0.237727</td>
      <td>-0.769031</td>
      <td>-1.964273</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1.040888</td>
      <td>1.448563</td>
      <td>-0.984106</td>
      <td>-0.099231</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-0.722966</td>
      <td>-1.198605</td>
      <td>-0.477420</td>
      <td>-0.265710</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-0.005394</td>
      <td>0.286019</td>
      <td>0.730833</td>
      <td>-0.473830</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1.231130</td>
      <td>-1.574169</td>
      <td>0.781478</td>
      <td>-0.159057</td>
    </tr>
    <tr>
      <th>5</th>
      <td>-1.417875</td>
      <td>-0.247297</td>
      <td>-0.580590</td>
      <td>1.369179</td>
    </tr>
    <tr>
      <th>6</th>
      <td>-0.905663</td>
      <td>0.641291</td>
      <td>0.266012</td>
      <td>-0.474489</td>
    </tr>
    <tr>
      <th>7</th>
      <td>0.196629</td>
      <td>1.592408</td>
      <td>0.017062</td>
      <td>-1.300836</td>
    </tr>
    <tr>
      <th>8</th>
      <td>0.034225</td>
      <td>0.032075</td>
      <td>-1.876997</td>
      <td>-1.712954</td>
    </tr>
    <tr>
      <th>9</th>
      <td>0.399283</td>
      <td>0.087454</td>
      <td>-0.134279</td>
      <td>-1.936356</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.iloc[:,1:3]
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
      <th>B</th>
      <th>C</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>1.324341</td>
      <td>0.153554</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-1.596556</td>
      <td>-0.920610</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>0.204407</td>
      <td>0.256671</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>-0.770913</td>
      <td>-0.330677</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>0.305182</td>
      <td>-1.508353</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>0.705459</td>
      <td>0.369007</td>
    </tr>
  </tbody>
</table>
</div>



## Join
SQL 방식으로 merge합니다. [Database style joining](https://pandas.pydata.org/pandas-docs/stable/merging.html#merging-join) 섹션을 참고하세요.



```python
left = pd.DataFrame({'key': ['foo', 'foo'], 'lval': [1, 2]})
```


```python
right = pd.DataFrame({'key': ['foo', 'foo'], 'rval': [4, 5]})
```


```python
left
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
      <th>key</th>
      <th>lval</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>foo</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>foo</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>




```python
right
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
      <th>key</th>
      <th>rval</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>foo</td>
      <td>4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>foo</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>




```python
pd.merge(left, right, on= 'key')
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
      <th>key</th>
      <th>lval</th>
      <th>rval</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>foo</td>
      <td>1</td>
      <td>4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>foo</td>
      <td>1</td>
      <td>5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>foo</td>
      <td>2</td>
      <td>4</td>
    </tr>
    <tr>
      <th>3</th>
      <td>foo</td>
      <td>2</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>



이와 같은 다른 예시는 :


```python
left = pd.DataFrame({'key' : ['foo', 'bar'], 'lval' : [1, 2]})
```


```python
right = pd.DataFrame({'key': ['foo', 'bar'], 'rval': [4, 5]})
```


```python
left
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
      <th>key</th>
      <th>lval</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>foo</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>bar</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>




```python
right 
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
      <th>key</th>
      <th>rval</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>foo</td>
      <td>4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>bar</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>




```python
pd.merge(left, right, on= 'key')
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
      <th>key</th>
      <th>lval</th>
      <th>rval</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>foo</td>
      <td>1</td>
      <td>4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>bar</td>
      <td>2</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>



## Append (요소 추가)

데이터프레임에 하나, 혹은 여러 개의 행을 추가합니다. [Appending](https://pandas.pydata.org/pandas-docs/stable/merging.html#merging-concatenation) 섹션을 참조하시기 바랍니다.


```python
df = pd.DataFrame(np.random.randn(8, 4), columns=['A', 'B', 'C', 'D'])
```


```python
df
```


```python
s = df.iloc[3]
```


```python
df.append(s, ignore_index=True)
```

# Grouping (그룹화)




**그룹화**는 다음 단계 중 하나 이상을 포함하는 프로세스를 나타냅니다.

- 어떤 기준에 따라 여러 그룹으로 **데이터 분할(Splitting)**
- 각 그룹에 독립적으로 함수(function) **적용(Applying)**
- 결과물들을 하나의 자료구조로  **결합(Combining)**

자세한 내용은 [그룹화 ](https://pandas.pydata.org/pandas-docs/stable/groupby.html#groupby)섹션을 참조하십시오.


```python
df = pd.DataFrame(
    {
        'A' : ['foo', 'bar', 'foo', 'bar', 'foo', 'bar', 'foo', 'foo'],
        'B' : ['one', 'one', 'two', 'three', 'two', 'two', 'one', 'three'],
        'C' : np.random.randn(8),
        'D' : np.random.randn(8)
    })
```


```python
df
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>foo</td>
      <td>one</td>
      <td>0.056468</td>
      <td>-1.700804</td>
    </tr>
    <tr>
      <th>1</th>
      <td>bar</td>
      <td>one</td>
      <td>-0.223937</td>
      <td>-0.448887</td>
    </tr>
    <tr>
      <th>2</th>
      <td>foo</td>
      <td>two</td>
      <td>0.328946</td>
      <td>-0.401242</td>
    </tr>
    <tr>
      <th>3</th>
      <td>bar</td>
      <td>three</td>
      <td>1.023657</td>
      <td>0.246377</td>
    </tr>
    <tr>
      <th>4</th>
      <td>foo</td>
      <td>two</td>
      <td>0.988012</td>
      <td>0.965924</td>
    </tr>
    <tr>
      <th>5</th>
      <td>bar</td>
      <td>two</td>
      <td>-0.170186</td>
      <td>-0.557526</td>
    </tr>
    <tr>
      <th>6</th>
      <td>foo</td>
      <td>one</td>
      <td>-0.808825</td>
      <td>-1.947245</td>
    </tr>
    <tr>
      <th>7</th>
      <td>foo</td>
      <td>three</td>
      <td>0.216881</td>
      <td>1.028468</td>
    </tr>
  </tbody>
</table>
</div>



생성된 데이터프레임을 **그룹화**한 후 각 그룹에 [sum()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.sum.html#pandas.DataFrame.sum) 함수를 **적용**합니다.


```python
df.groupby('A').sum()
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
      <th>C</th>
      <th>D</th>
    </tr>
    <tr>
      <th>A</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>bar</th>
      <td>0.629535</td>
      <td>-0.760035</td>
    </tr>
    <tr>
      <th>foo</th>
      <td>0.781481</td>
      <td>-2.054898</td>
    </tr>
  </tbody>
</table>
</div>



여러 열을 기준으로 **그룹화**하면 계층적 index가 형성됩니다. 여기에도 sum 함수를 **적용** 할 수 있습니다.


```python
df.groupby(['A', 'B']).sum()
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
      <th>C</th>
      <th>D</th>
    </tr>
    <tr>
      <th>A</th>
      <th>B</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="3" valign="top">bar</th>
      <th>one</th>
      <td>-0.223937</td>
      <td>-0.448887</td>
    </tr>
    <tr>
      <th>three</th>
      <td>1.023657</td>
      <td>0.246377</td>
    </tr>
    <tr>
      <th>two</th>
      <td>-0.170186</td>
      <td>-0.557526</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">foo</th>
      <th>one</th>
      <td>-0.752358</td>
      <td>-3.648049</td>
    </tr>
    <tr>
      <th>three</th>
      <td>0.216881</td>
      <td>1.028468</td>
    </tr>
    <tr>
      <th>two</th>
      <td>1.316958</td>
      <td>0.564682</td>
    </tr>
  </tbody>
</table>
</div>



# Reshaping (변형)

[계층적 인덱싱](https://pandas.pydata.org/pandas-docs/stable/advanced.html#advanced-hierarchical) 및 [변형](https://pandas.pydata.org/pandas-docs/stable/reshaping.html#reshaping-stacking)에 대한 섹션을 참조하십시오.






## Stack (스택)


```python
tuples = list(zip(*[['bar', 'bar', 'baz', 'baz',
                     'foo', 'foo', 'qux', 'qux'],
                    ['one', 'two', 'one', 'two',
                     'one', 'two', 'one', 'two']]))
```


```python
index = pd.MultiIndex.from_tuples(tuples, names=['first', 'second'])
```


```python
df = pd.DataFrame(np.random.randn(8, 2), index=index, columns=['A', 'B'])
```


```python
df2  =  df[:4]
```


```python
df2
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
      <th>A</th>
      <th>B</th>
    </tr>
    <tr>
      <th>first</th>
      <th>second</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">bar</th>
      <th>one</th>
      <td>-0.195358</td>
      <td>0.750044</td>
    </tr>
    <tr>
      <th>two</th>
      <td>-0.104833</td>
      <td>-1.433699</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">baz</th>
      <th>one</th>
      <td>-0.113793</td>
      <td>-0.954064</td>
    </tr>
    <tr>
      <th>two</th>
      <td>-2.333533</td>
      <td>0.042629</td>
    </tr>
  </tbody>
</table>
</div>



[stack()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.stack.html#pandas.DataFrame.stack) 메서드는 DataFrame 열들의 레벨을 "압축"합니다.


```python
stacked = df2.stack()
```


```python
stacked
```




    first  second   
    bar    one     A   -0.195358
                   B    0.750044
           two     A   -0.104833
                   B   -1.433699
    baz    one     A   -0.113793
                   B   -0.954064
           two     A   -2.333533
                   B    0.042629
    dtype: float64



"Stacked" DataFrame 또는 Series (MultiIndex를 인덱스로 사용) 인 경우 [stack()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.stack.html#pandas.DataFrame.stack)의 역 연산은 [unstack()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.unstack.html#pandas.DataFrame.unstack)이며, 기본적으로 마지막 레벨을 unstack합니다.


```python
stacked.unstack()
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
      <th>A</th>
      <th>B</th>
    </tr>
    <tr>
      <th>first</th>
      <th>second</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">bar</th>
      <th>one</th>
      <td>-0.195358</td>
      <td>0.750044</td>
    </tr>
    <tr>
      <th>two</th>
      <td>-0.104833</td>
      <td>-1.433699</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">baz</th>
      <th>one</th>
      <td>-0.113793</td>
      <td>-0.954064</td>
    </tr>
    <tr>
      <th>two</th>
      <td>-2.333533</td>
      <td>0.042629</td>
    </tr>
  </tbody>
</table>
</div>




```python
stacked.unstack(1)
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
      <th>second</th>
      <th>one</th>
      <th>two</th>
    </tr>
    <tr>
      <th>first</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">bar</th>
      <th>A</th>
      <td>-0.875011</td>
      <td>-1.556174</td>
    </tr>
    <tr>
      <th>B</th>
      <td>1.395960</td>
      <td>-0.659940</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">baz</th>
      <th>A</th>
      <td>-0.104231</td>
      <td>-0.436920</td>
    </tr>
    <tr>
      <th>B</th>
      <td>2.667967</td>
      <td>-1.299129</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">foo</th>
      <th>A</th>
      <td>1.790953</td>
      <td>0.978248</td>
    </tr>
    <tr>
      <th>B</th>
      <td>-0.232506</td>
      <td>-0.547802</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">qux</th>
      <th>A</th>
      <td>0.980380</td>
      <td>-0.387887</td>
    </tr>
    <tr>
      <th>B</th>
      <td>0.290200</td>
      <td>-0.116857</td>
    </tr>
  </tbody>
</table>
</div>




```python
stacked.unstack(0)
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
      <th>first</th>
      <th>bar</th>
      <th>baz</th>
    </tr>
    <tr>
      <th>second</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">one</th>
      <th>A</th>
      <td>-0.195358</td>
      <td>-0.113793</td>
    </tr>
    <tr>
      <th>B</th>
      <td>0.750044</td>
      <td>-0.954064</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">two</th>
      <th>A</th>
      <td>-0.104833</td>
      <td>-2.333533</td>
    </tr>
    <tr>
      <th>B</th>
      <td>-1.433699</td>
      <td>0.042629</td>
    </tr>
  </tbody>
</table>
</div>



## Pivot Tables (피벗 테이블)

피벗 테이블 섹션을 참조하십시오.


```python
df = pd.DataFrame({'A' : ['one', 'one', 'two', 'three'] * 3,
                   'B' : ['A', 'B', 'C'] * 4,
                   'C' : ['foo', 'foo', 'foo', 'bar', 'bar', 'bar'] * 2,
                   'D' : np.random.randn(12),
                   'E' : np.random.randn(12)})
```


```python
df
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>E</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>one</td>
      <td>A</td>
      <td>foo</td>
      <td>0.988377</td>
      <td>0.841519</td>
    </tr>
    <tr>
      <th>1</th>
      <td>one</td>
      <td>B</td>
      <td>foo</td>
      <td>0.650030</td>
      <td>-1.278552</td>
    </tr>
    <tr>
      <th>2</th>
      <td>two</td>
      <td>C</td>
      <td>foo</td>
      <td>-0.572768</td>
      <td>-0.113546</td>
    </tr>
    <tr>
      <th>3</th>
      <td>three</td>
      <td>A</td>
      <td>bar</td>
      <td>-0.917207</td>
      <td>-0.605644</td>
    </tr>
    <tr>
      <th>4</th>
      <td>one</td>
      <td>B</td>
      <td>bar</td>
      <td>0.041252</td>
      <td>0.490003</td>
    </tr>
    <tr>
      <th>5</th>
      <td>one</td>
      <td>C</td>
      <td>bar</td>
      <td>0.006014</td>
      <td>-1.556474</td>
    </tr>
    <tr>
      <th>6</th>
      <td>two</td>
      <td>A</td>
      <td>foo</td>
      <td>-1.395743</td>
      <td>-0.194504</td>
    </tr>
    <tr>
      <th>7</th>
      <td>three</td>
      <td>B</td>
      <td>foo</td>
      <td>-1.273224</td>
      <td>0.849112</td>
    </tr>
    <tr>
      <th>8</th>
      <td>one</td>
      <td>C</td>
      <td>foo</td>
      <td>0.532535</td>
      <td>-0.997676</td>
    </tr>
    <tr>
      <th>9</th>
      <td>one</td>
      <td>A</td>
      <td>bar</td>
      <td>0.139564</td>
      <td>-2.028593</td>
    </tr>
    <tr>
      <th>10</th>
      <td>two</td>
      <td>B</td>
      <td>bar</td>
      <td>-0.873256</td>
      <td>0.202317</td>
    </tr>
    <tr>
      <th>11</th>
      <td>three</td>
      <td>C</td>
      <td>bar</td>
      <td>-0.821394</td>
      <td>1.874484</td>
    </tr>
  </tbody>
</table>
</div>



이 데이터에서 피벗 테이블을 매우 쉽게 생성 할 수 있습니다.


```python
pd.pivot_table(df, values='D', index=['A', 'B'], columns=['C'])
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
      <th>C</th>
      <th>bar</th>
      <th>foo</th>
    </tr>
    <tr>
      <th>A</th>
      <th>B</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="3" valign="top">one</th>
      <th>A</th>
      <td>0.139564</td>
      <td>0.988377</td>
    </tr>
    <tr>
      <th>B</th>
      <td>0.041252</td>
      <td>0.650030</td>
    </tr>
    <tr>
      <th>C</th>
      <td>0.006014</td>
      <td>0.532535</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">three</th>
      <th>A</th>
      <td>-0.917207</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>B</th>
      <td>NaN</td>
      <td>-1.273224</td>
    </tr>
    <tr>
      <th>C</th>
      <td>-0.821394</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">two</th>
      <th>A</th>
      <td>NaN</td>
      <td>-1.395743</td>
    </tr>
    <tr>
      <th>B</th>
      <td>-0.873256</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>C</th>
      <td>NaN</td>
      <td>-0.572768</td>
    </tr>
  </tbody>
</table>
</div>



# Time Series (시계열)

pandas는 리샘플링 작업을 수행하기 위해 간단하고, 강력하며 효율적인 기능을 제공합니다(예 : 2차 자료를 5-minutely 데이터로 변환). 이는 재무 애플리케이션에서 매우 일반적이지만 이에 국한되지 않습니다. [Time Series(시계열) 섹션](https://pandas.pydata.org/pandas-docs/stable/timeseries.html#timeseries)을 참고하세요.


```python
rng = pd.date_range('1/1/2012', periods=100, freq='S')
```


```python
ts = pd.Series(np.random.randint(0, 500, len(rng)), index=rng)
```


```python
ts.resample('5Min').sum()
```




    2012-01-01    24266
    Freq: 5T, dtype: int64



시간대를 표현합니다 :


```python
rng = pd.date_range('3/6/2012 00:00', periods=5, freq='D')
```


```python
ts = pd.Series(np.random.randn(len(rng)), rng)
```


```python
ts
```




    2012-03-06   -0.823286
    2012-03-07   -0.411211
    2012-03-08   -0.373167
    2012-03-09   -0.296496
    2012-03-10    0.669600
    Freq: D, dtype: float64




```python
ts_utc = ts.tz_localize('UTC')
```


```python
ts_utc
```




    2012-03-06 00:00:00+00:00   -0.823286
    2012-03-07 00:00:00+00:00   -0.411211
    2012-03-08 00:00:00+00:00   -0.373167
    2012-03-09 00:00:00+00:00   -0.296496
    2012-03-10 00:00:00+00:00    0.669600
    Freq: D, dtype: float64



다른 시간대로 변환을 시행합니다 :


```python
ts_utc.tz_convert('US/Eastern')
```




    2012-03-05 19:00:00-05:00   -0.823286
    2012-03-06 19:00:00-05:00   -0.411211
    2012-03-07 19:00:00-05:00   -0.373167
    2012-03-08 19:00:00-05:00   -0.296496
    2012-03-09 19:00:00-05:00    0.669600
    Freq: D, dtype: float64



시간 범위 표현 간에 변환을 시행합니다 :


```python
rng = pd.date_range('1/1/2012', periods=5, freq='M')
```


```python
ts = pd.Series(np.random.randn(len(rng)), index=rng)
```


```python
ts
```




    2012-01-31   -0.421486
    2012-02-29   -0.184594
    2012-03-31   -0.117843
    2012-04-30   -0.126489
    2012-05-31   -0.351443
    Freq: M, dtype: float64




```python
ps = ts.to_period()
```


```python
ps
```




    2012-01   -0.421486
    2012-02   -0.184594
    2012-03   -0.117843
    2012-04   -0.126489
    2012-05   -0.351443
    Freq: M, dtype: float64




```python
ps.to_timestamp()
```




    2012-01-01   -0.421486
    2012-02-01   -0.184594
    2012-03-01   -0.117843
    2012-04-01   -0.126489
    2012-05-01   -0.351443
    Freq: MS, dtype: float64



기간과 타임 스탬프를 변환하면 편리한 산술 기능을 사용할 수 있습니다. 다음 예제에서는 11월에 끝나는 연말 결산의 분기 별 빈도를 다음 달 오전 9시까지 변환합니다 :


```python
prng = pd.period_range('1990Q1', '2000Q4', freq='Q-NOV')
```


```python
ts = pd.Series(np.random.randn(len(prng)), prng)
```


```python
ts.index = (prng.asfreq('M', 'e') + 1).asfreq('H', 's') + 9
```


```python
ts.head()
```




    1990-03-01 09:00    0.427177
    1990-06-01 09:00   -0.042834
    1990-09-01 09:00   -1.484662
    1990-12-01 09:00    0.310516
    1991-03-01 09:00   -0.718662
    Freq: H, dtype: float64



# Categoricals (범주화)

판다스는 데이터프레임 내에 범주형 데이터를 포함할 수 있습니다. 관련 문서는 [범주형 데이터 설명서](https://pandas.pydata.org/pandas-docs/stable/categorical.html#categorical) 와 [API 문서](https://pandas.pydata.org/pandas-docs/stable/api.html#api-categorical)를 참조하세요.


```python
df = pd.DataFrame({"id":[1,2,3,4,5,6], "raw_grade":['a', 'b', 'b', 'a', 'a', 'e']})
```

raw grade를 범주형 데이터 타입으로 바꿔주세요.


```python
df["grade"] = df["raw_grade"].astype("category")
```


```python
df["grade"]
```

범주를 더 의미있는 이름으로 바꿔주세요. (Series.cat을 범주화할 준비가 됐습니다!)


```python
df["grade"].cat.categories = ["very good", "good", "very bad"]
```

범주의 순서를 바꾸고 누락된 범주를 동시에 추가합니다. (Series.cat 메서드는 자동으로 새 Series를 반환합니다.)


```python
df["grade"] = df["grade"].cat.set_categories(["very bad", "bad", "medium", "good", "very good"])
```


```python
df["grade"]
```

정렬(sort)은 어휘 순서(lexical order)가 아닌, 범주(category) 순서로 수행됩니다.


```python
df.sort_values(by="grade")
```

범주의 열을 기준으로 그룹화하면(grouping) 빈 범주도 표시됩니다.


```python
df.groupby("grade").size()
```

# Plotting (플로팅)

[Plotting](https://pandas.pydata.org/pandas-docs/stable/visualization.html#visualization) 문서를 참조하세요.


```python
ts = pd.Series(np.random.randn(1000), index=pd.date_range('1/1/2000', periods=1000))
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-5-1b5db062ba99> in <module>()
    ----> 1 ts = pd.Series(np.random.randn(1000), index=pd.date_range('1/1/2000', periods=1000))
    

    NameError: name 'pd' is not defined



```python
ts = ts.cumsum()
```


```python
ts.plot()
```




    <matplotlib.axes._subplots.AxesSubplot at 0x7fe9146a1668>




![png](output_240_1.png)


DataFrame에서 [plot()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.plot.html#pandas.DataFrame.plot) 메소드는 레이블에 있는 모든 열을 그릴 때 편리합니다




```python
df = pd.DataFrame(np.random.randn(1000, 4), index=ts.index,
                  columns=['A', 'B', 'C', 'D'])  
```


```python
df = df.cumsum()
```


```python
plt.figure(); df.plot(); plt.legend(loc='best')
```




    <matplotlib.legend.Legend at 0x7fe914792cf8>




    <matplotlib.figure.Figure at 0x7fe9145862e8>



![png](output_244_2.png)


#Getting Data In/Out

##CSV

[csv 파일에 씁니다.](https://pandas.pydata.org/pandas-docs/stable/io.html#io-store-in-csv)


```python
df.to_csv('foo.csv')
```

[csv 파일에서 읽습니다.](https://pandas.pydata.org/pandas-docs/stable/io.html#io-read-csv-table)


```python
pd.read_csv('foo.csv')
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
      <th>Unnamed: 0</th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2000-01-01</td>
      <td>-0.026335</td>
      <td>-0.717745</td>
      <td>0.117218</td>
      <td>-0.549751</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2000-01-02</td>
      <td>-1.049763</td>
      <td>-1.785373</td>
      <td>-0.822755</td>
      <td>-0.781237</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2000-01-03</td>
      <td>-1.268265</td>
      <td>-0.791013</td>
      <td>-0.141242</td>
      <td>0.587446</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2000-01-04</td>
      <td>-2.667261</td>
      <td>-1.408698</td>
      <td>0.240404</td>
      <td>-0.705050</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2000-01-05</td>
      <td>-4.471245</td>
      <td>-2.303159</td>
      <td>-0.314543</td>
      <td>-0.252046</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2000-01-06</td>
      <td>-3.832738</td>
      <td>-2.485943</td>
      <td>0.554620</td>
      <td>-1.617591</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2000-01-07</td>
      <td>-3.764604</td>
      <td>-2.644763</td>
      <td>1.224718</td>
      <td>-1.640596</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2000-01-08</td>
      <td>-3.706452</td>
      <td>-3.435865</td>
      <td>-0.816544</td>
      <td>-0.449831</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2000-01-09</td>
      <td>-3.936663</td>
      <td>-3.419143</td>
      <td>-3.106705</td>
      <td>-0.312725</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2000-01-10</td>
      <td>-5.014653</td>
      <td>-3.227070</td>
      <td>-3.314237</td>
      <td>-0.252284</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2000-01-11</td>
      <td>-4.206563</td>
      <td>-3.708036</td>
      <td>-2.286878</td>
      <td>-1.057564</td>
    </tr>
    <tr>
      <th>11</th>
      <td>2000-01-12</td>
      <td>-2.854169</td>
      <td>-2.604047</td>
      <td>-2.011293</td>
      <td>-0.496066</td>
    </tr>
    <tr>
      <th>12</th>
      <td>2000-01-13</td>
      <td>-2.425489</td>
      <td>-1.964353</td>
      <td>-4.310662</td>
      <td>-0.254048</td>
    </tr>
    <tr>
      <th>13</th>
      <td>2000-01-14</td>
      <td>-2.861078</td>
      <td>-2.412133</td>
      <td>-5.397059</td>
      <td>-0.806801</td>
    </tr>
    <tr>
      <th>14</th>
      <td>2000-01-15</td>
      <td>-3.719051</td>
      <td>-2.304485</td>
      <td>-6.486873</td>
      <td>-0.764641</td>
    </tr>
    <tr>
      <th>15</th>
      <td>2000-01-16</td>
      <td>-3.954312</td>
      <td>-2.581573</td>
      <td>-8.355360</td>
      <td>-0.367414</td>
    </tr>
    <tr>
      <th>16</th>
      <td>2000-01-17</td>
      <td>-4.536187</td>
      <td>-1.894429</td>
      <td>-7.774752</td>
      <td>0.640860</td>
    </tr>
    <tr>
      <th>17</th>
      <td>2000-01-18</td>
      <td>-6.213764</td>
      <td>-2.279379</td>
      <td>-7.626798</td>
      <td>1.334903</td>
    </tr>
    <tr>
      <th>18</th>
      <td>2000-01-19</td>
      <td>-5.164765</td>
      <td>-2.382773</td>
      <td>-6.484147</td>
      <td>1.233413</td>
    </tr>
    <tr>
      <th>19</th>
      <td>2000-01-20</td>
      <td>-5.951784</td>
      <td>-3.206533</td>
      <td>-7.456596</td>
      <td>0.322954</td>
    </tr>
    <tr>
      <th>20</th>
      <td>2000-01-21</td>
      <td>-6.094290</td>
      <td>-1.806253</td>
      <td>-9.041151</td>
      <td>0.338585</td>
    </tr>
    <tr>
      <th>21</th>
      <td>2000-01-22</td>
      <td>-4.219268</td>
      <td>-2.402346</td>
      <td>-8.804568</td>
      <td>0.513316</td>
    </tr>
    <tr>
      <th>22</th>
      <td>2000-01-23</td>
      <td>-2.293937</td>
      <td>-0.970808</td>
      <td>-9.969945</td>
      <td>-1.423756</td>
    </tr>
    <tr>
      <th>23</th>
      <td>2000-01-24</td>
      <td>-2.352168</td>
      <td>-1.972728</td>
      <td>-10.398412</td>
      <td>-1.538460</td>
    </tr>
    <tr>
      <th>24</th>
      <td>2000-01-25</td>
      <td>-3.424824</td>
      <td>-3.400619</td>
      <td>-10.598927</td>
      <td>-0.946809</td>
    </tr>
    <tr>
      <th>25</th>
      <td>2000-01-26</td>
      <td>-4.202295</td>
      <td>-3.554636</td>
      <td>-11.156441</td>
      <td>0.381046</td>
    </tr>
    <tr>
      <th>26</th>
      <td>2000-01-27</td>
      <td>-3.952622</td>
      <td>-2.975130</td>
      <td>-11.532670</td>
      <td>-0.797718</td>
    </tr>
    <tr>
      <th>27</th>
      <td>2000-01-28</td>
      <td>-1.792251</td>
      <td>-2.364668</td>
      <td>-12.882036</td>
      <td>-0.858014</td>
    </tr>
    <tr>
      <th>28</th>
      <td>2000-01-29</td>
      <td>-3.438095</td>
      <td>-1.666424</td>
      <td>-12.658937</td>
      <td>-2.489144</td>
    </tr>
    <tr>
      <th>29</th>
      <td>2000-01-30</td>
      <td>-4.057369</td>
      <td>-1.405462</td>
      <td>-12.806334</td>
      <td>-1.991122</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>970</th>
      <td>2002-08-28</td>
      <td>-3.497089</td>
      <td>-21.799331</td>
      <td>-27.512780</td>
      <td>-23.948642</td>
    </tr>
    <tr>
      <th>971</th>
      <td>2002-08-29</td>
      <td>-3.780051</td>
      <td>-23.708894</td>
      <td>-28.615803</td>
      <td>-23.760478</td>
    </tr>
    <tr>
      <th>972</th>
      <td>2002-08-30</td>
      <td>-4.002507</td>
      <td>-21.969386</td>
      <td>-29.438393</td>
      <td>-23.252988</td>
    </tr>
    <tr>
      <th>973</th>
      <td>2002-08-31</td>
      <td>-4.661825</td>
      <td>-22.424417</td>
      <td>-29.850030</td>
      <td>-23.513799</td>
    </tr>
    <tr>
      <th>974</th>
      <td>2002-09-01</td>
      <td>-5.663649</td>
      <td>-22.963628</td>
      <td>-27.758539</td>
      <td>-23.589569</td>
    </tr>
    <tr>
      <th>975</th>
      <td>2002-09-02</td>
      <td>-5.292332</td>
      <td>-23.556915</td>
      <td>-28.301622</td>
      <td>-22.163613</td>
    </tr>
    <tr>
      <th>976</th>
      <td>2002-09-03</td>
      <td>-3.612934</td>
      <td>-22.336902</td>
      <td>-27.114755</td>
      <td>-23.072718</td>
    </tr>
    <tr>
      <th>977</th>
      <td>2002-09-04</td>
      <td>-2.004994</td>
      <td>-21.699757</td>
      <td>-28.022481</td>
      <td>-22.063717</td>
    </tr>
    <tr>
      <th>978</th>
      <td>2002-09-05</td>
      <td>-3.486140</td>
      <td>-20.241942</td>
      <td>-28.106275</td>
      <td>-22.023699</td>
    </tr>
    <tr>
      <th>979</th>
      <td>2002-09-06</td>
      <td>-2.948154</td>
      <td>-20.530027</td>
      <td>-28.772999</td>
      <td>-22.433141</td>
    </tr>
    <tr>
      <th>980</th>
      <td>2002-09-07</td>
      <td>-5.152315</td>
      <td>-21.374976</td>
      <td>-27.403556</td>
      <td>-23.157017</td>
    </tr>
    <tr>
      <th>981</th>
      <td>2002-09-08</td>
      <td>-5.147801</td>
      <td>-20.548175</td>
      <td>-29.534911</td>
      <td>-24.613610</td>
    </tr>
    <tr>
      <th>982</th>
      <td>2002-09-09</td>
      <td>-4.502910</td>
      <td>-20.825335</td>
      <td>-30.456955</td>
      <td>-26.170400</td>
    </tr>
    <tr>
      <th>983</th>
      <td>2002-09-10</td>
      <td>-4.055736</td>
      <td>-20.860546</td>
      <td>-30.771489</td>
      <td>-26.248800</td>
    </tr>
    <tr>
      <th>984</th>
      <td>2002-09-11</td>
      <td>-3.541193</td>
      <td>-20.374508</td>
      <td>-29.947598</td>
      <td>-27.705778</td>
    </tr>
    <tr>
      <th>985</th>
      <td>2002-09-12</td>
      <td>-2.381324</td>
      <td>-20.117239</td>
      <td>-30.709171</td>
      <td>-29.244136</td>
    </tr>
    <tr>
      <th>986</th>
      <td>2002-09-13</td>
      <td>-1.938442</td>
      <td>-20.314696</td>
      <td>-31.080254</td>
      <td>-27.618574</td>
    </tr>
    <tr>
      <th>987</th>
      <td>2002-09-14</td>
      <td>-2.802669</td>
      <td>-20.325638</td>
      <td>-29.945957</td>
      <td>-28.456105</td>
    </tr>
    <tr>
      <th>988</th>
      <td>2002-09-15</td>
      <td>-3.254465</td>
      <td>-20.479762</td>
      <td>-30.494301</td>
      <td>-27.236968</td>
    </tr>
    <tr>
      <th>989</th>
      <td>2002-09-16</td>
      <td>-4.003399</td>
      <td>-20.993692</td>
      <td>-30.913225</td>
      <td>-28.414765</td>
    </tr>
    <tr>
      <th>990</th>
      <td>2002-09-17</td>
      <td>-2.932438</td>
      <td>-21.160098</td>
      <td>-30.772429</td>
      <td>-28.795505</td>
    </tr>
    <tr>
      <th>991</th>
      <td>2002-09-18</td>
      <td>-0.115537</td>
      <td>-20.376504</td>
      <td>-29.998241</td>
      <td>-27.913785</td>
    </tr>
    <tr>
      <th>992</th>
      <td>2002-09-19</td>
      <td>-0.616637</td>
      <td>-21.349927</td>
      <td>-30.673046</td>
      <td>-28.567137</td>
    </tr>
    <tr>
      <th>993</th>
      <td>2002-09-20</td>
      <td>0.162513</td>
      <td>-21.273755</td>
      <td>-29.990274</td>
      <td>-30.597840</td>
    </tr>
    <tr>
      <th>994</th>
      <td>2002-09-21</td>
      <td>0.825661</td>
      <td>-21.142892</td>
      <td>-28.226350</td>
      <td>-32.383629</td>
    </tr>
    <tr>
      <th>995</th>
      <td>2002-09-22</td>
      <td>1.990832</td>
      <td>-21.797458</td>
      <td>-30.384845</td>
      <td>-31.293541</td>
    </tr>
    <tr>
      <th>996</th>
      <td>2002-09-23</td>
      <td>2.935926</td>
      <td>-20.709951</td>
      <td>-29.961604</td>
      <td>-30.726829</td>
    </tr>
    <tr>
      <th>997</th>
      <td>2002-09-24</td>
      <td>3.447949</td>
      <td>-19.751597</td>
      <td>-28.357718</td>
      <td>-31.180625</td>
    </tr>
    <tr>
      <th>998</th>
      <td>2002-09-25</td>
      <td>4.454119</td>
      <td>-20.884311</td>
      <td>-26.421078</td>
      <td>-32.768527</td>
    </tr>
    <tr>
      <th>999</th>
      <td>2002-09-26</td>
      <td>2.200247</td>
      <td>-21.263247</td>
      <td>-25.612438</td>
      <td>-35.104136</td>
    </tr>
  </tbody>
</table>
<p>1000 rows × 5 columns</p>
</div>



##HDF5
[HDFStores](https://pandas.pydata.org/pandas-docs/stable/io.html#io-hdf5)에 읽고 씁니다.

HDF5 Store에 씁니다.



```python
df.to_hdf('foo.h5','df')
```


    ---------------------------------------------------------------------------

    ModuleNotFoundError                       Traceback (most recent call last)

    /usr/local/lib/python3.6/dist-packages/pandas/io/pytables.py in __init__(self, path, mode, complevel, complib, fletcher32, **kwargs)
        444         try:
    --> 445             import tables  # noqa
        446         except ImportError as ex:  # pragma: no cover
    

    ModuleNotFoundError: No module named 'tables'

    
    During handling of the above exception, another exception occurred:
    

    ImportError                               Traceback (most recent call last)

    <ipython-input-26-2030282e689d> in <module>()
    ----> 1 df.to_hdf('foo.h5','df')
    

    /usr/local/lib/python3.6/dist-packages/pandas/core/generic.py in to_hdf(self, path_or_buf, key, **kwargs)
       1469 
       1470         from pandas.io import pytables
    -> 1471         return pytables.to_hdf(path_or_buf, key, self, **kwargs)
       1472 
       1473     def to_msgpack(self, path_or_buf=None, encoding='utf-8', **kwargs):
    

    /usr/local/lib/python3.6/dist-packages/pandas/io/pytables.py in to_hdf(path_or_buf, key, value, mode, complevel, complib, append, **kwargs)
        278     if isinstance(path_or_buf, string_types):
        279         with HDFStore(path_or_buf, mode=mode, complevel=complevel,
    --> 280                       complib=complib) as store:
        281             f(store)
        282     else:
    

    /usr/local/lib/python3.6/dist-packages/pandas/io/pytables.py in __init__(self, path, mode, complevel, complib, fletcher32, **kwargs)
        446         except ImportError as ex:  # pragma: no cover
        447             raise ImportError('HDFStore requires PyTables, "{ex}" problem '
    --> 448                               'importing'.format(ex=str(ex)))
        449 
        450         if complib is not None and complib not in tables.filters.all_complibs:
    

    ImportError: HDFStore requires PyTables, "No module named 'tables'" problem importing

    

    ---------------------------------------------------------------------------
    NOTE: If your import is failing due to a missing package, you can
    manually install dependencies using either !pip or !apt.
    
    To view examples of installing some common dependencies, click the
    "Open Examples" button below.
    ---------------------------------------------------------------------------
    


HDF5 Store에서 읽어옵니다.


```python
pd.read_hdf('foo.h5','df')
```


    ---------------------------------------------------------------------------

    FileNotFoundError                         Traceback (most recent call last)

    <ipython-input-10-4242b2e6e2a5> in <module>()
    ----> 1 pd.read_hdf('foo.h5','df')
    

    /usr/local/lib/python3.6/dist-packages/pandas/io/pytables.py in read_hdf(path_or_buf, key, mode, **kwargs)
        345         if not exists:
        346             raise compat.FileNotFoundError(
    --> 347                 'File %s does not exist' % path_or_buf)
        348 
        349         store = HDFStore(path_or_buf, mode=mode, **kwargs)
    

    FileNotFoundError: File foo.h5 does not exist


## Excel
[MS Excel](https://pandas.pydata.org/pandas-docs/stable/io.html#io-excel)에 읽고 씁니다. 

엑셀 파일에 씁니다. 



```python
df.to_excel('foo.xlsx', sheet_name='Sheet1')
```

엑셀 파일을 읽어옵니다.


```python
pd.read_excel('foo.xlsx', 'Sheet1', index_col=None, na_values=['NA'])
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2000-01-01</th>
      <td>-0.026335</td>
      <td>-0.717745</td>
      <td>0.117218</td>
      <td>-0.549751</td>
    </tr>
    <tr>
      <th>2000-01-02</th>
      <td>-1.049763</td>
      <td>-1.785373</td>
      <td>-0.822755</td>
      <td>-0.781237</td>
    </tr>
    <tr>
      <th>2000-01-03</th>
      <td>-1.268265</td>
      <td>-0.791013</td>
      <td>-0.141242</td>
      <td>0.587446</td>
    </tr>
    <tr>
      <th>2000-01-04</th>
      <td>-2.667261</td>
      <td>-1.408698</td>
      <td>0.240404</td>
      <td>-0.705050</td>
    </tr>
    <tr>
      <th>2000-01-05</th>
      <td>-4.471245</td>
      <td>-2.303159</td>
      <td>-0.314543</td>
      <td>-0.252046</td>
    </tr>
    <tr>
      <th>2000-01-06</th>
      <td>-3.832738</td>
      <td>-2.485943</td>
      <td>0.554620</td>
      <td>-1.617591</td>
    </tr>
    <tr>
      <th>2000-01-07</th>
      <td>-3.764604</td>
      <td>-2.644763</td>
      <td>1.224718</td>
      <td>-1.640596</td>
    </tr>
    <tr>
      <th>2000-01-08</th>
      <td>-3.706452</td>
      <td>-3.435865</td>
      <td>-0.816544</td>
      <td>-0.449831</td>
    </tr>
    <tr>
      <th>2000-01-09</th>
      <td>-3.936663</td>
      <td>-3.419143</td>
      <td>-3.106705</td>
      <td>-0.312725</td>
    </tr>
    <tr>
      <th>2000-01-10</th>
      <td>-5.014653</td>
      <td>-3.227070</td>
      <td>-3.314237</td>
      <td>-0.252284</td>
    </tr>
    <tr>
      <th>2000-01-11</th>
      <td>-4.206563</td>
      <td>-3.708036</td>
      <td>-2.286878</td>
      <td>-1.057564</td>
    </tr>
    <tr>
      <th>2000-01-12</th>
      <td>-2.854169</td>
      <td>-2.604047</td>
      <td>-2.011293</td>
      <td>-0.496066</td>
    </tr>
    <tr>
      <th>2000-01-13</th>
      <td>-2.425489</td>
      <td>-1.964353</td>
      <td>-4.310662</td>
      <td>-0.254048</td>
    </tr>
    <tr>
      <th>2000-01-14</th>
      <td>-2.861078</td>
      <td>-2.412133</td>
      <td>-5.397059</td>
      <td>-0.806801</td>
    </tr>
    <tr>
      <th>2000-01-15</th>
      <td>-3.719051</td>
      <td>-2.304485</td>
      <td>-6.486873</td>
      <td>-0.764641</td>
    </tr>
    <tr>
      <th>2000-01-16</th>
      <td>-3.954312</td>
      <td>-2.581573</td>
      <td>-8.355360</td>
      <td>-0.367414</td>
    </tr>
    <tr>
      <th>2000-01-17</th>
      <td>-4.536187</td>
      <td>-1.894429</td>
      <td>-7.774752</td>
      <td>0.640860</td>
    </tr>
    <tr>
      <th>2000-01-18</th>
      <td>-6.213764</td>
      <td>-2.279379</td>
      <td>-7.626798</td>
      <td>1.334903</td>
    </tr>
    <tr>
      <th>2000-01-19</th>
      <td>-5.164765</td>
      <td>-2.382773</td>
      <td>-6.484147</td>
      <td>1.233413</td>
    </tr>
    <tr>
      <th>2000-01-20</th>
      <td>-5.951784</td>
      <td>-3.206533</td>
      <td>-7.456596</td>
      <td>0.322954</td>
    </tr>
    <tr>
      <th>2000-01-21</th>
      <td>-6.094290</td>
      <td>-1.806253</td>
      <td>-9.041151</td>
      <td>0.338585</td>
    </tr>
    <tr>
      <th>2000-01-22</th>
      <td>-4.219268</td>
      <td>-2.402346</td>
      <td>-8.804568</td>
      <td>0.513316</td>
    </tr>
    <tr>
      <th>2000-01-23</th>
      <td>-2.293937</td>
      <td>-0.970808</td>
      <td>-9.969945</td>
      <td>-1.423756</td>
    </tr>
    <tr>
      <th>2000-01-24</th>
      <td>-2.352168</td>
      <td>-1.972728</td>
      <td>-10.398412</td>
      <td>-1.538460</td>
    </tr>
    <tr>
      <th>2000-01-25</th>
      <td>-3.424824</td>
      <td>-3.400619</td>
      <td>-10.598927</td>
      <td>-0.946809</td>
    </tr>
    <tr>
      <th>2000-01-26</th>
      <td>-4.202295</td>
      <td>-3.554636</td>
      <td>-11.156441</td>
      <td>0.381046</td>
    </tr>
    <tr>
      <th>2000-01-27</th>
      <td>-3.952622</td>
      <td>-2.975130</td>
      <td>-11.532670</td>
      <td>-0.797718</td>
    </tr>
    <tr>
      <th>2000-01-28</th>
      <td>-1.792251</td>
      <td>-2.364668</td>
      <td>-12.882036</td>
      <td>-0.858014</td>
    </tr>
    <tr>
      <th>2000-01-29</th>
      <td>-3.438095</td>
      <td>-1.666424</td>
      <td>-12.658937</td>
      <td>-2.489144</td>
    </tr>
    <tr>
      <th>2000-01-30</th>
      <td>-4.057369</td>
      <td>-1.405462</td>
      <td>-12.806334</td>
      <td>-1.991122</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2002-08-28</th>
      <td>-3.497089</td>
      <td>-21.799331</td>
      <td>-27.512780</td>
      <td>-23.948642</td>
    </tr>
    <tr>
      <th>2002-08-29</th>
      <td>-3.780051</td>
      <td>-23.708894</td>
      <td>-28.615803</td>
      <td>-23.760478</td>
    </tr>
    <tr>
      <th>2002-08-30</th>
      <td>-4.002507</td>
      <td>-21.969386</td>
      <td>-29.438393</td>
      <td>-23.252988</td>
    </tr>
    <tr>
      <th>2002-08-31</th>
      <td>-4.661825</td>
      <td>-22.424417</td>
      <td>-29.850030</td>
      <td>-23.513799</td>
    </tr>
    <tr>
      <th>2002-09-01</th>
      <td>-5.663649</td>
      <td>-22.963628</td>
      <td>-27.758539</td>
      <td>-23.589569</td>
    </tr>
    <tr>
      <th>2002-09-02</th>
      <td>-5.292332</td>
      <td>-23.556915</td>
      <td>-28.301622</td>
      <td>-22.163613</td>
    </tr>
    <tr>
      <th>2002-09-03</th>
      <td>-3.612934</td>
      <td>-22.336902</td>
      <td>-27.114755</td>
      <td>-23.072718</td>
    </tr>
    <tr>
      <th>2002-09-04</th>
      <td>-2.004994</td>
      <td>-21.699757</td>
      <td>-28.022481</td>
      <td>-22.063717</td>
    </tr>
    <tr>
      <th>2002-09-05</th>
      <td>-3.486140</td>
      <td>-20.241942</td>
      <td>-28.106275</td>
      <td>-22.023699</td>
    </tr>
    <tr>
      <th>2002-09-06</th>
      <td>-2.948154</td>
      <td>-20.530027</td>
      <td>-28.772999</td>
      <td>-22.433141</td>
    </tr>
    <tr>
      <th>2002-09-07</th>
      <td>-5.152315</td>
      <td>-21.374976</td>
      <td>-27.403556</td>
      <td>-23.157017</td>
    </tr>
    <tr>
      <th>2002-09-08</th>
      <td>-5.147801</td>
      <td>-20.548175</td>
      <td>-29.534911</td>
      <td>-24.613610</td>
    </tr>
    <tr>
      <th>2002-09-09</th>
      <td>-4.502910</td>
      <td>-20.825335</td>
      <td>-30.456955</td>
      <td>-26.170400</td>
    </tr>
    <tr>
      <th>2002-09-10</th>
      <td>-4.055736</td>
      <td>-20.860546</td>
      <td>-30.771489</td>
      <td>-26.248800</td>
    </tr>
    <tr>
      <th>2002-09-11</th>
      <td>-3.541193</td>
      <td>-20.374508</td>
      <td>-29.947598</td>
      <td>-27.705778</td>
    </tr>
    <tr>
      <th>2002-09-12</th>
      <td>-2.381324</td>
      <td>-20.117239</td>
      <td>-30.709171</td>
      <td>-29.244136</td>
    </tr>
    <tr>
      <th>2002-09-13</th>
      <td>-1.938442</td>
      <td>-20.314696</td>
      <td>-31.080254</td>
      <td>-27.618574</td>
    </tr>
    <tr>
      <th>2002-09-14</th>
      <td>-2.802669</td>
      <td>-20.325638</td>
      <td>-29.945957</td>
      <td>-28.456105</td>
    </tr>
    <tr>
      <th>2002-09-15</th>
      <td>-3.254465</td>
      <td>-20.479762</td>
      <td>-30.494301</td>
      <td>-27.236968</td>
    </tr>
    <tr>
      <th>2002-09-16</th>
      <td>-4.003399</td>
      <td>-20.993692</td>
      <td>-30.913225</td>
      <td>-28.414765</td>
    </tr>
    <tr>
      <th>2002-09-17</th>
      <td>-2.932438</td>
      <td>-21.160098</td>
      <td>-30.772429</td>
      <td>-28.795505</td>
    </tr>
    <tr>
      <th>2002-09-18</th>
      <td>-0.115537</td>
      <td>-20.376504</td>
      <td>-29.998241</td>
      <td>-27.913785</td>
    </tr>
    <tr>
      <th>2002-09-19</th>
      <td>-0.616637</td>
      <td>-21.349927</td>
      <td>-30.673046</td>
      <td>-28.567137</td>
    </tr>
    <tr>
      <th>2002-09-20</th>
      <td>0.162513</td>
      <td>-21.273755</td>
      <td>-29.990274</td>
      <td>-30.597840</td>
    </tr>
    <tr>
      <th>2002-09-21</th>
      <td>0.825661</td>
      <td>-21.142892</td>
      <td>-28.226350</td>
      <td>-32.383629</td>
    </tr>
    <tr>
      <th>2002-09-22</th>
      <td>1.990832</td>
      <td>-21.797458</td>
      <td>-30.384845</td>
      <td>-31.293541</td>
    </tr>
    <tr>
      <th>2002-09-23</th>
      <td>2.935926</td>
      <td>-20.709951</td>
      <td>-29.961604</td>
      <td>-30.726829</td>
    </tr>
    <tr>
      <th>2002-09-24</th>
      <td>3.447949</td>
      <td>-19.751597</td>
      <td>-28.357718</td>
      <td>-31.180625</td>
    </tr>
    <tr>
      <th>2002-09-25</th>
      <td>4.454119</td>
      <td>-20.884311</td>
      <td>-26.421078</td>
      <td>-32.768527</td>
    </tr>
    <tr>
      <th>2002-09-26</th>
      <td>2.200247</td>
      <td>-21.263247</td>
      <td>-25.612438</td>
      <td>-35.104136</td>
    </tr>
  </tbody>
</table>
<p>1000 rows × 4 columns</p>
</div>



#Gotchas

작업을 수행하려고 시도하면 다음과 같은 예외 상황을 볼 수도 있습니다 :


```python
if pd.Series([False, True, False]):
print("I was true")
```


      File "<ipython-input-80-9074a2390e8e>", line 2
        print("I was true")
            ^
    IndentationError: expected an indented block
    


설명 및 수행 할 작업은 [비교](https://pandas.pydata.org/pandas-docs/stable/basics.html#basics-compare)를 참조하십시오.

[Gotchas](https://pandas.pydata.org/pandas-docs/stable/gotchas.html#gotchas)도 참조하십시오.

