# 객체지향 프로그래밍

파이썬은 객체지향 프로그래밍에서의 대표적인 언어 중 하나이다.

절차지향과 객체지향의 차이를 간단히 도식화하면 다음과 같다.

![photo](./python_class_ref.png)

절차지향은 어떠한 행위에 대하여 순차적으로 진행이 된다.

> 1. 고객의 돈, 자판기의 돈 변수를 만들어 자판기에 넣는 행위를 함수로 만든다.
> 2. 준비된 제품 변수를 만들어 돈을 계산하고 잔돈을 주는 함수를 만든다.
> 3. 고객의 제품 변수를 만든다.

객체지향의 경우는 객체를 기반으로 행위가 진행이 된다.

> 1. 자판기와 고객이라는 객체를 만든다.
> 2. 각 객체는 돈과 제품이라는 변수와 행위에 대한 메소드(method)가 정의되어있다.
> 3. 그 객체를 기반으로 행위가 진행된다. (이상의 그림 참고)

**그런데 사실, 객체만으로 어떠한 행위가 진행되는 것은 아니며, 행위가 발생했을 때 그 절차에 따라 진행되는 것은 절차지향과 동일하다.**

```
* 절차지향 프로그래밍은 프로그램의 순서와 흐름을 먼저 세우고 필요한 자료구조와 함수를 설계하는 방식
* 자료구조와 이를 중심으로 한 모듈을 먼저 설계한 후, 실행순서와 흐름을 고려해 설계하는 방식
```

_참고 : [네이버 블로그](https://blog.naver.com/meandyou201/220907281602)


# 클래스(Class)

| 인스턴스의 리터럴 | 클래스       | 메서드                       |
| ----------------- | ------------ | ---------------------------- |
| 1                 | int          | __add__(), __sub__(), ...    |
| 1.5               | float        | __add__(), is_integer(), ... |
| “Hey”             | str          | lower(), strip(), ...        |
| [1, 2]            | list         | append(), sort(), ...        |
| (리터럴 없음)     | pd.DataFrame | head(), melt(), pivot(), ... |



- Object : Class + Instance를 통칭해서 부름

  - Class : Category라고 생각하면 됨. Class 자체에는 실체가 없음 *(Class를 실제로 사용하려면 안의 Instance를 만들어주어야 함, 메세지는 Instance에게 보내게 됨)*
  - Instance : Class의 예시. 실체가 있음
  - Method : Object 내부의 함수. 첫번째 인자로 self를 무조건 받아야 한다.

  

- Class를 쓰는 이유 : 연산을 하기 편함. 있어야 할 것이 없으면 코드가 복잡해짐



- 예시

  - x = 1 : 정수 Class의 Instance인 객체가 생성

  - df = pd.DataFrame(...) : 'pd.DataFrame' Class의 instacne인 object가 생긴 후 df에 담김

  - df = pd.read_csv(...) : read_csv는 pd 모듈에 담긴 함수, 함수 내부에서 pd.DataFrame()을 호출하여 DataFrame class의 instance를 생성

  - df.head() : head는 df의 Method *(위에 pd.read_csv는 pd라는 라이브러리의 모듈을 가져온 것이라 method가 아니라 모듈이지만, df는 객체이기 때문에 method라 부름)*

  - ~~~
    x = 1
    y = x + 2
    z = x.add(2) #사실 이런 함수가 실행되는 것. 정수 객체에는 add라는 method가 담겨있음
    ~~~

  

## Class 정의하기

```
class ClassName:

	def __init__(self, name, age):

		self.name = name

		self.age = age

	def my_method(self, arg):

		pass
```

클래스를 정의하는 코드에서 주의할 점은 크게 3가지 있다.

> 1. 클래스 이름은 Camel 표기법을 따른다. 
>
>    (띄어쓰기 등의 구분을 '_' 대신 대문자로 구분하는 것)
>
> 2. 클래스의 가장 처음은 \_\_init\_\_이라는 것을 사용해 해당 클래스(객체)를 초기화(기본 설정)를 해준다.
>
>    **파이썬에서 언더바( _ ) 두 개로 묶인 이름은 사용하지 않는 것이 좋다.**
>
> 3. def 로 초기화 혹은 함수를 정의할 때, self라는 argument를 주는데, 이는 클래스로 인스턴스를 만들거나 상속할 때, 각각의 인스턴스와 상속받은 아이들이 각자의 존재를 개별로 인정받기 위함이다.



## VendingMachine 실습에 Class 적용하기

~~~python
class VendingMachine:
    def __init__(self):
        self.change = 0
        
# __init__을 해서 처음 생성되면서 self(인스턴스 자기자신)을 위한 change라는 변수를 새로 만들고 0을 대입한다는 의미. 기본설정을 하는 것 혹은 초기화를 하는 것
        
    def run(self):
        pass
~~~
