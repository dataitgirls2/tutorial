# 180816 오후수업

## Kaggle Titanic

### Kaggle titanic 데이터로 시각화하기

`conda install -c conda-forge missingno`

```python
import missingno as msno
msno.matrix(train)
```

#### 1. pivot_table과 groupby 활용해 보기

- [pandas.DataFrame.groupby — pandas 0.23.4 documentation] (https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.groupby.html)

```python
data.groupby(['col1', 'col2']).mean()
data.groupby('col1')[['col2']].mean()

data.pivot_table(index=['col1'], values=['col2'], aggfunc=np.mean)
```

- [pandas.pivot_table — pandas 0.23.4 documentation] (https://pandas.pydata.org/pandas-docs/stable/generated/pandas.pivot_table.html)

#### 2. 타이타닉 데이터 시각화

https://www.rstudio.com/wp-content/uploads/2015/03/ggplot2-cheatsheet.pdf

```python
train['Survived'] = train['Survived'].astype('category')

(ggplot(train)
 + aes(x='Sex', y='Survived')
 + geom_col() + ggtitle('성별 생존률')
 + theme(text=element_text(family='NanumBarunGothic'))
)

(ggplot(train)
 + aes(x='Age', y='Fare', fill='Pclass')
 + geom_point() + ggtitle('생존 여부별 성별 요금 등급 분포')
 + facet_wrap('~Survived')
 + theme(text=element_text(family='NanumBarunGothic'))
)

(ggplot(train)
 + aes(x='Age')
 + geom_histogram(binwidth=10)
 + ggtitle('연령대 분포')
 + theme(text=element_text(family='NanumBarunGothic'))
)
```

#### 3. 결측치 처리

결측치 처리 후 시각화 해보기

`train['Age'] = train['Age'].dropna()` 

#### 4. 캐글 스코어 올리기 - 실습

EDA를 바탕으로 생존자 예측하고 점수 올려보기
