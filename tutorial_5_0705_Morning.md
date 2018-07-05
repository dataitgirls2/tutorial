# Today We Learned
## 2018/07/05 thu :cloud:
### python 정리하기


>**수업 목표**
>> 범죄 통계 데이터 분석 과제 점검  
>> 함수와 이름 공간 복습  
>> Lambda 란?  
>과제 실습 1 (딕셔너리 - 평균 구하기)  
>과제 실습 2 (분산, 표준편차 구하기)  

'재귀함수' = 영화 Inception 
- 
- 함수 속 함수 = 꿈 속의 꿈
- def _____ 별 단계 = 꿈
- return result
   - return은 킥 (꿈속에서 벗어나는 계기)
   - result는 토템 (꿈 속에서 갖고 탈출)


# 강력범죄 데이터
```
%matplotlib inline
import pandas as pd
import numpy as np
import math
import matplotlib.pyplot as plt

df = pd.read_csv('https://s3.ap-northeast-2.amazonaws.com/data10902/messy/crime_clean.csv',encoding='utf-8')

data = [d for d in df.get_values().tolist() if not math.isnan(d[-1])]
```
* 데이터를 불러온다.

```
df.groupby(["젠더", "유형"]).agg({"명":"sum"})
```
* 젠더별 유형(가해자,피해자) 명 수의 합을 표로 볼 수 있다.

```
df.groupby(["젠더", "대분류","유형"]).agg({"명":"mean"})
```
* 젠더-대분류-유형을 그룹화하여 명 수의 평균을 볼 수 있다.




```
def get_sum(data):
    result = 0
    for datum in data:
        result = result + datum
    return result

def get_len(data):
    result = 0
    for datum in data:
        result = result + 1
    return result

def get_average(data):
    total = get_sum(data)
    n = get_len(data)
    result = total / n
    return result


score = [50, 60, 70]
average = get_average(score)
print(average)
```


**Lambda**
-
"한 줄 짜리 간단한 함수를 정의하는 간결한 문법"  

lambda 는
- Second-order function(2차 함수)
- 함수 속 함수  


리스트 이름 순으로 정렬하기

    students = [('alan', 50), ('dave', 60), ('brad', 30), ('cate', 40)]
    def by_name(student):
	    return student[0] 
	    #0번째 element 기준으로 정렬하겠다
	    #이름 순으로 정렬됨
	sorted(students, key=by_name)
	>>> [('alan',50),('brad',30),('cate',40),('dave',60)]
	
	#위 함수를 한 줄로 정리하는 방법 (1회용)
	sorted(students, key=lambda     s:s[0])
	#        리스트  함수명따로지정x 변수:표현식 

리스트 나이 순으로 정렬하기

    def by_age(student):
	    return student[1]
	sorted(students, key=by_age)
	#위와 같은 결과 나오는 lambda함수
	sorted(students, key = lambda s:s[1])
	>>> [('brad',30),('cate',40),('alan',50),('dave',60)]

더 쉽게

    def blah (x) :
	    return x+2
	blah = (lambda x : x+2)
	같은 값이 나오는 함수

# 실습 #1 40m

* 당신은 농구팀 코치이며, 네 명의 지원자 중 한 명을 추가로 선발하고자 합니다. 다음은 각 지원자 별 최근 열 번 경기에서의 득점 기록입니다.
```
candidates = {
  'alan': [8, 14, 6, 8, 14, 9, 14, 9, 15, 5],
  'brad': [11, 4, 11, 7, 9, 7, 8, 7, 10, 6],
  'cate': [16, 22, 13, 15, 12, 3, 20, 17, 13, 23],
  'dave': [24, 15, 18, 12, 9, 19, 23, 13, 14, 18],
}
```
* 평균 득점이 가장 높은 선수를 선발하고자 합니다. 어떤 선수를 선발해야 하는지, 그 이유는 무엇인지 설명하는 보고서를 작성하세요.

* 힌트: 자료의 요약 수업 내용을 참고하세요.
```
average = []

for name in candidates.keys():
  total = 0
  n = 0
  for i in candidates[name]:
    total += i
    n += 1
  average.append(total/n)

print(average)

lst = list(zip(candidates.keys(), average))
print(lst)
```
```
sorted_averages = sorted(named_averages, key=lambda s: s[1], reverse=True)
print(sorted_averages)
```
```
[('dave', 16.5), ('cate', 15.4), ('alan', 10.2), ('brad', 8.0)]
```
* 평균이 제일 높은 dave를 택한다.

# 실습 #2 40m

* 당신은 농구팀 코치이며, 네 명의 지원자 중 한 명을 추가로 선발하고자 합니다. 다음은 각 지원자 별 최근 경기에서의 득점 기록 일부를 임의로 추출한 데이터입니다. 선수별로 경기 횟수가 다릅니다.
```
candidates = {
  'alan': [8, 14, 6, 8, 14, 9, 14, 9, 15, 5],
  'brad': [11, 4, 11, 7, 9, 7, 8, 7, 6],
  'cate': [16, 22, 15, 12, 3, 20, 17, 13, 23],
  'dave': [24, 15, 18, 18, 12, 9, 19, 23, 13, 14, 18],
}
```
* 매 경기에서의 기복이 가장 적은 선수를 선발하고자 합니다. 어떤 선수를 선발해야 하는지, 그 이유는 무엇인지 설명하는 보고서를 작성하세요.

* 힌트: 자료의 요약 수업 내용을 참고하세요.

```
import math
candidates = {
  'alan': [8, 14, 6, 8, 14, 9, 14, 9, 15, 5],
  'brad': [11, 4, 11, 7, 9, 7, 8, 7, 6],
  'cate': [16, 22, 15, 12, 3, 20, 17, 13, 23],
  'dave': [24, 15, 18, 18, 12, 9, 19, 23, 13, 14, 18],
}

sd = []

for name, scores in candidates.items():
    # 합계 구하기
    total = sum(scores)
    # value의 전체 개수 구하기
    n = len(scores)
    # 평균구하기
    mean = total / n
    
    # 분산구하기
    vsum = 0
    for x in scores:
      vsum = vsum + (x - mean)**2  # 
    var = vsum / n-1
    
# 표준편차 구하기
    std = math.sqrt(var)
    sd.append(std)
    
    
named_sd = list(zip(candidates.keys(), sd))
    
print(named_sd)
```
```
[('alan', 3.370459909270543), ('brad', 1.9019158631804098), ('cate', 5.647024782032472), ('dave', 4.237768007566061)]
```
* 로 표준편차가 작은 brad를 택해야 한다.
