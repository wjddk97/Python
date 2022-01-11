# generator란?

- iterator를 생성해주는 함수이다.

`iterator` : next()메소드를 이용해 데이터에 순차적으로 접근이 가능한 객체

- 제너레이터 객체는 모든 값을 메모리에 올려두고 이용하는 것이 아닌,
- 필요할 때마다 생성해서 반환하는 일을 합니다.
- 이 때문에 메모리를 효율적으로 사용할 수 있다는 장점이 있습니다.

<br>

**yield 구문**

```python
def create_gen():
alist = range(1, 4)
for x in alist:
	yield x

my_generator = create_gen()
print(my_generator)

for n in my_genorator:

#결과
#<generator object create_gen at 0x7fc02986d3c0>
#1
#2
#3
```

- 일반적인 함수의 return문과 유사하며, yield 키워드를 사용하면 제너레이터를 반환합니다.

<br>

```python
# 제너레이터 두번 실행

def create_gen():
    alist = range(1, 4)
    for x in alist:
        yield x

my_generator = create_gen()
print(my_generator)

for n in my_generator:
    print(n)
    
print("-----------------")
    
for n in my_generator:
    print(n)

# 실행 결과
#<generator object create_gen at 0x7f91de9d43c0>
#1
#2
#3
#-----------------
```

- 제너레이터는 한번 실행하면 아무것도 반환하지 않습니다.