![](https://images.velog.io/images/wjddk97/post/eafc4f7b-8183-45c5-b494-cce44a4e7d6c/image.png)


  
<br>
  
  

# 1. 동기 (synchronous)
- python은 동기 방식으로 동작하도록 설계된 언어입니다.
- **서버에서 요청할 시 응답을 받아야 다음 동작을 수행할 수 있습니다.**
- 예를들어, a작업이 모두 진행 될때까지 b작업은 대기해야합니다.


<br>

# 2. 비동기 (Asynchronous)
- **요청을 보냈을 때 응답과 상관없이 다음 동작을 수행할 수 있습니다.**
- 예를 들어, a작업을 시작하면 동시에 b작업이 실행되고, a작업은 결과값이 나오는대로 출력됩니다.

<br>
<br>

## 이벤트 루프와 코루틴
`이벤트 루프`
- 이벤트 루프는 작업 루프를 돌면서 하나씩 실행시키는 역할을 합니다.
- 만약 실행중인 작업이 특정 데이터를 요청하고 응답을 기다려야 하는 상황이라면,
- 다음 작업으로 넘어갔다가 응답이 완료되었을 때 다시 돌아가서 마무리하게 됩니다.

<br>

`코루틴` - 비동기 함수
- 응답이 지연되는 부분이 나타나면 다음 작업을 실행하다가
- 멈추었던 부분에서 응답이 완료되었을 때 다시 돌아와서 남은 작업을 완료할 수 있는 함수를 의미합니다.
- 파이썬에서 코루틴이 아닌 일반적인 함수는 `서브루틴(Subroutine)`이라고 합니다.

<br>
<br>

## 파이썬 비동기로 처리하기

- asyncio 모듈 이용
- **함수 앞에 `async`를 붙이면 코루틴**을 만들 수 있습니다.
- 다른 작업으로 통제권을 넘겨줄 필요가 있는 부분에서는 `await`를 써줍니다. 이때, `await`뒤에 오는 함수도 코루틴으로 작성되어 있어야 합니다.

<br>

동기식 프로그래밍

```python
import time

def find_users_sync(n):
    for i in range(1, n + 1):
        print(f'{n}명 중 {i}번 째 사용자 조회 중 ...')
        time.sleep(1)
    print(f'> 총 {n} 명 사용자 동기 조회 완료!')

def process_sync():
    start = time.time()
    find_users_sync(3)
    find_users_sync(2)
    find_users_sync(1)
    end = time.time()
    print(f'>>> 동기 처리 총 소요 시간: {end - start}')

if __name__ == '__main__':
    process_sync()

3명 중 1번 째 사용자 조회 중 ...
3명 중 2번 째 사용자 조회 중 ...
3명 중 3번 째 사용자 조회 중 ...
> 총 3 명 사용자 동기 조회 완료!
2명 중 1번 째 사용자 조회 중 ...
2명 중 2번 째 사용자 조회 중 ...
> 총 2 명 사용자 동기 조회 완료!
1명 중 1번 째 사용자 조회 중 ...
> 총 1 명 사용자 동기 조회 완료!
>>> 동기 처리 총 소요 시간: 6.020448923110962
```

<br>

비동기식 프로그래밍

```python
import time
import asyncio

async def find_users_async(n):
    for i in range(1, n + 1):
        print(f'{n}명 중 {i}번 째 사용자 조회 중 ...')
        await asyncio.sleep(1)
    print(f'> 총 {n} 명 사용자 비동기 조회 완료!')

async def process_async():
    start = time.time()
    await asyncio.wait([
        find_users_async(3),
        find_users_async(2),
        find_users_async(1),
    ])
    end = time.time()
    print(f'>>> 비동기 처리 총 소요 시간: {end - start}')

if __name__ == '__main__':
    asyncio.run(process_async())

1명 중 1번 째 사용자 조회 중 ...
2명 중 1번 째 사용자 조회 중 ...
3명 중 1번 째 사용자 조회 중 ...
> 총 1 명 사용자 비동기 조회 완료!
2명 중 2번 째 사용자 조회 중 ...
3명 중 2번 째 사용자 조회 중 ...
> 총 2 명 사용자 비동기 조회 완료!
3명 중 3번 째 사용자 조회 중 ...
> 총 3 명 사용자 비동기 조회 완료!
>>> 비동기 처리 총 소요 시간: 3.0041661262512207
```