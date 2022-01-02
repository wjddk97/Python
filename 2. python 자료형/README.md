# 1. Data Types

- int(정수), float(실수), complex(복소수) 
- bool(불) 
- str(문자열) 
- list(리스트)
- tuple(튜플)
- set(집합, 셋)
- dictionary(딕셔너리)

<br>

**크게 수치 자료형, 불 자료형, 군집 자료형으로 구분할 수 있습니다.**

- 수치 자료형 : 숫자 저장
  - int, float, complex
  <br>
- 불 자료형 :True, False 저장
  - bool
  <br>
- 군집 자료형 : 여러 데이터 저장
  - str, list, tuple, set, dict
  <br>
  
## Sequence Type
- 시퀀스 자료형이란 값이 연속적으로 이어진 자료형으로 list, tuple, str이 있다.
- 즉, 데이터에 순서(번호)를 붙여 나열한 것이다.
<br>

## iterable과 iterator
### iterable
 - 요소를 하나씩 차례로 반환 가능한 object를 말한다. 
 - 예로는 sequence type인 list, str, tuple 이 대표적이다.
 - non-sequence type 인 dict도 있다.
 
 ```python
a = [1, 2, 3, 4, 5]

for el in a:
    print(el)

# 1
# 2
# 3
# 4
# 5

-----------------------------------
    
a = {"key1":1, "key2":1, "key3":1}

for el in a:
    print(el)
    
# key1
# key2
# key3
```
<br>

### iterator
- next() 메소드로 데이터를 순차적으로 호출 가능한 object 이다.
- iterable 이라고 해서 반드시 iterator 라는 것은 아니다. 
```python
a = [1, 2, 3, 4, 5]
next(a)

# Traceback (most recent call last):
# File "/solution.py", line 4, in <module>
# print(next(a))
# TypeError: 'list' object is not an iterator
```
<br>

- iter()를 사용하여 iterator객체로 변환할 수 있다.
```python
a    = [1, 2, 3]
iter = iter(a)
next(iter)
next(iter)
next(iter)

# 1
# 2
# 3
# 마지막 요소 이후에 next() 를 호출하면 StopIteration 이라는 exception 이 발생
```
-  하지만, 우리가 list 나 tuple 같은 iterable 한 object 를 사용할 때 
-  굳이 iter() 함수를 사용하지 않아도 for 문을 사용하여 순차적으로 접근이 가능하였다. 
-  for 문으로 looping 하는 동안, python 내부에서 임시로 list를 iterator로 자동 변환해주었기 때문이다.
<br>

# 2. 가변객체와 불변객체
- 가변객체 : 객체의 상태를 **바꿀 수 있다.**
- 불변객체 : 객체의 상태를 **바꿀 수 없다.**
<br>

|                | data type                       |
|----------------|---------------------------------|
|가변 (mutable)   | list, set, dict                 |
|불변 (immutable) | int, float, bool, tuple, string |


<br>

# 3. 정적언어와 동적언어
정적타입 언어는 변수를 선언할 때 자료형을 함께 명시해야한다.

컴파일 시에 잘못된 자료형으로의 대입이나 연산 등의 오류를 미리 체크한다.

```cpp
//C++
int num1 = 3;
float num2 = 4.6f;
double num3 = 3.23d;
char ch = 's';
string str = "abc";
//컴파일 시 자료형 결정
```

<br>

그에 반해 동적타입 언어인 파이썬에서는

자료형 없이 변수에 값을 대입하면, 알아서 자료형을 지정.

따라서 컴파일시가 아니라 런타임시에 변수의 자료형이 결정된다.

> **런타임** : 프로그램이 실행되고 있는 동안의 동작



```python
#Python
num1 = 12
num2 = 1.2
str = "Hello world!"
#자료형을 작성하지 않는다.
```

<br>

동적타입 언어는 실행시켜보기 전에는 자료형에서 비롯되는 오류를 검출하기 어렵다는 단점이 있지만,

코드 구현시 자료형을 일일이 지정할 필요가 없어서 **유연하고 매우 빠르게 코딩이 가능하다.**
