**1. instance <br>
2. static <br>
3. class**

위 3가지 method의 차이점

<br>

# 1. instance method
- 흔히 class 안에서 만들어준 함수를 의미한다.
- 인스턴스 변수에 엑세스할 수 있도록 첫 번째 인자에 
항상 객체 자신을 의미하는 **self** 파라미터를 갖는다.


<br>

- 아래 코드에선 **print_info(), test_func()** 가 인스턴스 메서드에 해당한다.

<br>

[ 호출 방법 ] <br>


**#1** - 메서드 내에서 호출할 시 **self.메서드()** <br>
**#2, #3** - 클래스 밖에서는 **객체.메서드()**

```py
class Test:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def print_info(self):
        print(self.name, ',', self.age) #1

    def test_func(self):
        self.print_info() 

test1 = Test('hong', 22)
test1.print_info() #2 hong , 22 
test1.test_func()  #3 hong , 22
```

<br>

# 2. static method (정적 메서드) 

- self를 받지 않아 인스턴스 속성, 인스턴스 메서드가 필요 없을 때 사용
- 인스턴스 변수에 액세스가 불가능, **인스턴스 상태를 변화시키지 않는다.**
- 클래스 변수(속성) 에는 **클래스명.클래스속성명**으로 엑세스 가능
- **@staticmethod** 데코레이터 사용

<br>

[ 호출 방법 ] <br>

**#1, #2** 클래스.메서드()

```py
class Calc:
    count = 10  #클래스 변수
    
    @staticmethod
    def add(a):
        print(a + Calc.count)	#클래스 속성(Calc.count)에는 접근 가능
 
    @staticmethod
    def mul(a):
        print(a * Calc.count)
 
Calc.add(10)  #1
>>>20

Calc.mul(10)  #2 
>>>100
```

<br>

# 3. class method
- self 파라미터 대신 **cls라는 클래스를 의미하는 파라미터 가진다.**
- cls로 **클래스 속성에 접근**할 수 있다.
- cls를 사용하면 클레스 메서드 내부에서 현재 클래스의 인스턴스를 만들 수도 있다. ( **cls() = 현재클래스명()** )
- **@classmethod** 데코레이터 사용

<br>

[ 호출 방법 ]

 <br>

**#** 클래스.메서드()

```py
class Person:
    count = 0    # 클래스 속성
 
    def __init__(self):
        Person.count += 1    # 인스턴스가 만들어질 때
                             # 클래스 속성 count에 1을 더함
 
    @classmethod
    def print_count(cls):
        print('{0}명 생성되었습니다.'.format(cls.count))    # cls로 클래스 속성에 접근
     
     
    @classmethod
    def create(cls):
        p = cls()    # cls()로 인스턴스 생성
        return p
        
 
james = Person()
maria = Person()
Person.print_count()    # 2명 생성되었습니다.

Person.create()  # cls()로 인스턴스 생성
Person.print_count()    # 3명 생성되었습니다.
```

<br>

# 4. Static   vs   Class

## 공통점
- 별도의 인스턴스 생성 없이 클래스명 뒤에 `.` 오퍼레이터를 붙여서 호출 가능

<br>

## 차이점
- 상속 관계에서 클래스 메소드의 경우 cls인자를 활용하여 현재클래스 속성을 가져온다.

- 스테틱 메소드의 경우 부모 클래스의 속성을 가져온다.

```py
class Test:
    default = "parent"

    def __init__(self):
        self.data = self.default
    
    @classmethod
    def class_test(cls):
        return cls()
    
    @staticmethod
    def static_test():
        return Test()
    
class ChildTest(Test):
    default = "child"

test1 = ChildTest.class_test()
test2 = ChildTest.static_test()

print(test1.default)
print(test2.default)

#출력 결과
#child
#parent
```