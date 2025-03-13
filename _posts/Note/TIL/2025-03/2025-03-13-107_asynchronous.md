---
title:  "[TIL] 내일배움캠프 107일차_[Django] Django와 Python에서의 비동기 처리 " 

categories: 
    - TIL
tags: 
    - TIL
    - 내일배움캠프


toc: True
toc_sticky: True
---

![TIL](/assets/images/TIL2.png){: .align-center style="width:35%;"}

# 👀Today I Learn
- 비동기 처리(asynchronous processing)는 현대 웹 애플리케이션에서 필수적인 개념
- 비동기 처리 덕분에 하나의 작업이 끝날 때까지 기다리지 않고 다른 작업을 수행할 수 있음

## 동기(Synchronous)와 비동기(Asynchronous)
### 1. 동기 처리
- 동기 처리란 하나의 작업이 끝나야만 다음 작업이 실행되는 방식
- 즉, 코드가 순차적으로 실행되며, 하나의 작업이 완료될 때까지 다른 작업은 대기해야 함

```python
import time

def sync_function():
    print("작업 시작")
    time.sleep(3)  # 3초 동안 대기
    print("작업 완료")

sync_function()
```

- 위 코드에서는 time.sleep(3)이 실행되는 동안 다른 작업이 블로킹(blocking)됨

### 2. 비동기 처리
- 비동기 처리란 하나의 작업이 끝날 때까지 기다리지 않고 다음 작업을 수행하는 방식
- Python에서는 async와 await 키워드를 활용하여 비동기 처리를 구현할 수 있음

```python
import asyncio

async def async_function():
    print("작업 시작")
    await asyncio.sleep(3)  # 3초 대기, 다른 작업 가능
    print("작업 완료")

asyncio.run(async_function())
```

- 이 방식에서는 await을 통해 대기하는 동안 다른 작업을 수행할 수 있어 보다 효율적인 처리가 가능

<br>

## Python에서의 비동기 처리
### 멀티스레딩
- 멀티스레딩(Multi-threading)은 여러 개의 스레드를 생성하여 동시에 실행하는 방식
- 주로 I/O 작업(파일 읽기/쓰기, 네트워크 요청 등)에 사용됨

```python
import threading
import time

def task():
    print("작업 시작")
    time.sleep(3)
    print("작업 완료")

thread = threading.Thread(target=task)
thread.start()
```

### 멀티프로세싱 
- 멀티프로세싱(Multi-processing)은 여러 개의 프로세스를 실행하여 CPU 작업을 병렬로 수행하는 방식
- CPU 연산이 많은 작업에 적합

```python
import multiprocessing
import time

def task():
    print("작업 시작")
    time.sleep(3)
    print("작업 완료")

process = multiprocessing.Process(target=task)
process.start()
```

<br>

## Django에서의 비동기 처리
### Celery + Redis
- Django에서는 Celery를 활용하여 비동기 처리를 수행할 수 있음
- Celery는 분산 태스크 큐 시스템으로, 비동기적으로 백그라운드 작업을 실행할 때 사용됨
- Celery의 메시지 브로커로는 Redis를 주로 사용
- 사용법
  - 설치

    ```bash
    pip install celery redis
    ```
  - 설정(Django 프로젝트 `settings.py`)

    ```python
    CELERY_BROKER_URL = 'redis://localhost:6379/0'
    ```

  - 작업 정의(`tasks.py`)

    ```python
    from celery import shared_task
    import time

    @shared_task
    def async_task():
        time.sleep(3)
        return "작업 완료"
    ```

  - Celery 실행:

    ```bash
    celery -A 프로젝트명 worker --loglevel=info
    ```


### async/await
- Django 3.1 이상에서는 비동기 뷰를 지원하여 async와 await을 사용할 수 있음

```python
from django.http import JsonResponse
import asyncio

async def async_view(request):
    await asyncio.sleep(3)  # 비동기 처리
    return JsonResponse({"message": "비동기 작업 완료"})
```

<br>


## Django와 Channels
### 웹소켓(WebSocket)
- 웹소켓은 양방향 실시간 통신을 가능하게 하는 프로토콜
- 기존 HTTP 요청/응답 방식과 달리, 지속적인 연결을 유지하며 데이터를 주고받을 수 있음

- HTTP vs WebSocket

| 비교 항목 |  HTTP | WebSocket |
| --------- | --------- | --------- |
| 연결 방식 | 요청-응답 | 지속적인 연결 유지 |
| 데이터 교환 | 단방향 (클라이언트 요청 → 서버 응답) | 양방향 (서버와 클라이언트 간 실시간 데이터 송수신)|
| 주요 용도 | 일반적인 웹 요청 | 실시간 채팅, 주식 데이터 전송 등 |

### Django Channels로 웹소켓 구현
- Django는 기본적으로 웹소켓을 지원하지 않지만, Django Channels를 사용하면 웹소켓을 쉽게 구현할 수 있음
- 사용법
  - 설치

    ```bash
    pip install channels
    ```

  - `settings.py` 설정

    ```python
    INSTALLED_APPS = [
        'channels',
        'myapp',
    ]
    ASGI_APPLICATION = 'myproject.asgi.application'
    ```

  - ASGI 설정(`asgi.py`)

    ```python
    import os
    from django.core.asgi import get_asgi_application
    from channels.routing import ProtocolTypeRouter, URLRouter
    import myapp.routing

    os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'myproject.settings')

    application = ProtocolTypeRouter({
        "http": get_asgi_application(),
        "websocket": URLRouter(myapp.routing.websocket_urlpatterns),
    })
    ```

    - 웹소켓 소비자(`consumers.py`):

    ```python
    from channels.generic.websocket import AsyncWebsocketConsumer
    import json

    class ChatConsumer(AsyncWebsocketConsumer):
        async def connect(self):
            await self.accept()

        async def receive(self, text_data):
            await self.send(text_data=json.dumps({"message": "메시지 수신됨"}))
    ```

  - 라우팅 설정(`routing.py`):

    ```python
    from django.urls import re_path
    from .consumers import ChatConsumer

    websocket_urlpatterns = [
        re_path(r'ws/chat/$', ChatConsumer.as_asgi()),
    ]
    ```

### Redis와 함께 사용하여 다중 서버 운영
- Channels는 기본적으로 Django의 메모리 내에서만 실행됨
- 하지만 여러 서버에서 웹소켓을 운영하려면 Redis를 사용하여 메시지를 공유해야 함
- 설정(`settings.py`):

    ```python
    CHANNEL_LAYERS = {
        "default": {
            "BACKEND": "channels_redis.core.RedisChannelLayer",
            "CONFIG": {
                "hosts": ["redis://localhost:6379"],
            },
        },
    }
    ```


<br>

## 비동기 처리의 한계와 주의할 점
- CPU 바운드 작업에서는 비동기 처리보다는 멀티프로세싱이 더 적합
- Django ORM은 기본적으로 비동기 처리를 지원하지 않음 (따라서 `sync_to_async` 변환 필요)
- Redis 브로커 관리 주의 (메모리 초과 가능)

<br>
<br>

# 💡Today I Thought

## 오늘의 체크리스트
- [x]  알고리즘 코드카타 1문제
- [x]  SQL 코드카타 2문제
- [x]  프론트엔드
    - [x]  Chatbot API 연결
- [x]  중간 발표회 발표자료 제작
- [x]  TIL 작성

## 회고
&nbsp;아.. 내일 벌써 중간 발표.. 한 게 한개도 없는 거 같은데.. 이상하다. 시간이 너무 빨리 흘러가는 거 같다. 이제 중간 발표 끝내면 주말동안 ML 기능 구현하고, 다음주부터는 다시 또 프론트 달려야할듯.. 이상하네.. 프론트 왜.. 다 하고 있지..😶‍🌫️