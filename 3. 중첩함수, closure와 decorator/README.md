# 1. 중첩함수란?
- 함수 내부에 정의된 또 다른 함수를 말합니다.
- 중첨함수는 상위 부모함수 안에서만 호출 가능합니다.

```python
def parent_function():
    def child_function():
        print("this is a child function")

    child_function()

#부모함수 호출 결과
parent_function()
> "this is a child function"
```

<br>
<br>

# 2. 클로져 (closure)
- 부모 함수의 변수나 정보를 가두어 사용합니다.

`클로져 조건`

- 중첩함수는 부모함수의 변수나 정보를 사용해야 합니다.
- 부모함수는 중첩함수를 return 합니다.

```python
def generate_power(base_number):   
    def nth_power(power):          
        return base_number ** power
    return nth_power                
    

# closure 생성 및 출력

power_of_two = generate_power(2)
# 부모함수의 변수인 base_number가 중첩함수에 격리되어 사용됨 => closure

power_of_two(7) 
# base_number가 2로 이미 셋팅 되어 있는 함수 

>>> 128
# 2^7 = 128
```

<br>
<br>


# 3. 데코레이터 (decorator)
- 함수를 인자로 받아 새로운 함수를 만들어 반환하는 함수
- 특정 함수의 전/후에 원하는 기능을 추가할 수 있다.

```python
import time

# 함수의 수행시간을 출력해주는 데코레이터
def elapsed(func): # 함수를 인수로 받는다.
    def wrapper():
        start = time.time()
        func()     # 함수를 수행한다.
        end = time.time()
        print("함수 수행시간: %f 초" % (end - start))  # 함수의 수행시간을 출력한다.
        
    return wrapper

@elapsed    # @decorator함수이름
def myfunc():
    print("함수가 실행됩니다.")

myfunc()
>>> 함수가 실행됩니다.
>>> 수행시간: 0.000005 초

# 동작원리
# decorated_myfunc = elapsed(myfunc)
# decorated_myfunc()
```

### 클로져와의 차이
- 데코레이터는 함수를 인자로 받는다는 차이가 있습니다.