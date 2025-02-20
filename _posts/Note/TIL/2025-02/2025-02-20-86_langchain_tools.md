---
title:  "[TIL] 내일배움캠프 86일차_[LLM] LangChain의 유용한 기능들을 활용해보기" 

categories: 
    - TIL
tags: 
    - TIL
    - 내일배움캠프
    - LLM
    - LanChain
    - Streaming
    - Caching
    - multi-turn
    - agent


toc: True
toc_sticky: True
---

![TIL](/assets/images/TIL2.png){: .align-center style="width:35%;"}

# 👀Today I Learn

[LangChain 공식문서](https://www.google.com/url?q=https%3A%2F%2Fpython.langchain.com%2Fdocs%2Fintegrations%2Ftools%2F)에서 Tool을 확인할 수 있음!

## 1. Streaming
- ChatGPT는 사용자 질문에 대해 사람이 실시간으로 타이핑하는 것처럼 답변을 제공함
- 이는 LLM이 한 단어씩 답변을 생성하기 때문에 가능하며, 이를 활용하면 사용자 경험을 더욱 향상시킬 수 있음

### LangChain에서 Streaming 구현

```python
from langchain_openai import ChatOpenAI

chat = ChatOpenAI(model_name="gpt-4o-mini")

#chat.invoke("고양이에 대한 시를 써줘.") # 평소에 완성된 대답을 받던 함수 (invoke)

for chunk in chat.stream("고양이에 대한 시를 써줘.") :
  print(chunk.content, end="", flush=True)
```

- `stream()` 함수를 활용하여 모델의 답변을 연속적으로 받아옴
- for문을 사용하여 각 청크를 출력하여 실시간 응답을 제공할 수 있음
- 이를 활용하면 더욱 자연스럽고 효과적인 챗봇을 구축할 수 있음

<br>

## 2. Caching
- 실제 LLM 챗봇을 운영할 때 가장 중요한 요소 중 하나는 답변 속도
- 모델의 크기나 하드웨어 성능에 따라 속도가 제한되지만, 응답을 캐싱하면 속도를 크게 개선할 수 있음

![Image](https://github.com/user-attachments/assets/13ad44ad-4835-4aa7-b348-f7094ca5d1f1){: .align-center style="width:75%;"}

### LangChain에서 Caching 적용
```python
%%time
from langchain.globals import set_llm_cache
from langchain.cache import InMemoryCache

chat = ChatOpenAI(model_name="gpt-4o-mini")
set_llm_cache(InMemoryCache()) # 캐시 메모리 설정
chat.invoke("일반 상대성 이론을 한마디로 설명해줘.") #첫번째로 물어봄 -> 응답시간이 길게 걸림
```

```
CPU times: user 1.13 s, sys: 49.2 ms, total: 1.18 s
Wall time: 2.38 s
```

```python
%%time
chat.invoke("일반 상대성 이론을 한마디로 설명해줘.") #동일한 질문을 두번째로 물어봄 -> 응답시간이 훨씬 짧아짐
```

```
CPU times: user 2.16 ms, sys: 0 ns, total: 2.16 ms
Wall time: 2.05 ms
```

- 동일한 질문에 대한 응답을 저장하여 반복 요청 시 캐싱된 결과를 반환
- API 비용 절감 및 응답 속도 개선 가능
- 간단한 캐싱 기능을 추가하는 것만으로도 챗봇의 성능을 크게 향상시킬 수 있음

<br>

## 3. message_type
1. SystemMessage : LLM에 역할을 부여하는 메세지 ex) 너는 코딩 전문가야.
2. HumanMessage : LLM에 전달하는 사용자의 메세지 ex) A 함수 작성해줘.
3. AIMessage : LLM이 출력한 메세지 ex) def A(x): ...

### ChatPromptTemplate 모듈 사용해보기
```python
from langchain_core.prompts import ChatPromptTemplate

chat_template = ChatPromptTemplate.from_messages([
    ("system", "너의 이름은 {name}이고, 아주 귀여운 햄스터야. 모든 말을 햄으로 끝내."), # system message : 챗봇의 역할과 이름을 부여
    ("human", "{name}아 잘 지냈어?"),
    ("ai","잘 지냈햄. 너도 잘 지냈햄?"), # human message와 ai message로 지난 대화 히스토리 주입
    ("human", "{user_input}"),
    ]
)

messages = chat_template.format_messages(name="햄식이", user_input="잘 지냈지.. 너 줄라고 해바라기씨 사왔어.")
print(messages)
```

- 이러한 프롬프트 템플릿 작성법은 여러가지가 존재하며, 아래 방식으로도 작성 가능

    ```python
    from langchain_core.prompts import ChatPromptTemplate
    from langchain_core.messages import SystemMessage
    from langchain.prompts import HumanMessagePromptTemplate

    chat_template = ChatPromptTemplate.from_messages([
        SystemMessage(content=("너의 이름은 {name}이고, 아주 귀여운 햄스터야. 모든 말을 햄으로 끝내.")),
        HumanMessagePromptTemplate.from_template("{user_input}"),
    ]
    )
    messages = chat_template.format_messages(name="햄식이", user_input="잘 지냈지.. 너 줄라고 해바라기씨 사왔어.")
    print(messages)
    ```

<br>

## 4. multi-turn 대화
- ChatGPT를 사용하면 이전 대화를 계속 기억해 나가면서 대화를 이어나감
- 이렇게 전체 대화의 맥락을 읽고 대화를 주고 받는 것을 멀티 턴(Multi-turn)이라고 함
- 이와 다르게 바로 직전의 질문에만 답하는 것은 싱글 턴(Single-turn)이라고 함

### multi-turn 대화 사용해보기
```python
from langchain_core.prompts import ChatPromptTemplate

chat_template = ChatPromptTemplate.from_messages([
    ("system", "너의 이름은 햄식이이고, 아주 귀여운 햄스터야. 모든 말을 햄으로 끝내."),
    ("human", "햄식아 나 어제 수능쳤어 대박이지"), # 사람의 질문 (history)
    ("ai","진짜햄? 고생 많았햄!! "), # ai의 대답 (history)
    ("human", "{user_input}"), # 사람의 질문 (history)
    ]
)
# 이 messages에는 multi-turn 대화 기록(history)이 저장되어있다.
messages = chat_template.format_messages(user_input="햄식아 내가 어제 뭐했게!")


model = ChatOpenAI(model_name="gpt-4o-mini")
model.invoke(messages)
```

- ChatMessageHistory() 클래스를 활용하여 대화 내용을 저장할 수도 있음
  - 첫번째 방법은 대화 기록을 직접 튜플과 리스트로 작성하여 넘겨주었지만 이번에는 조금 더 효율적으로 메모리를 저장할 수 있도록 히스토리를 저장하고 로드하는 클래스의 도움을 받음

    ```python
    from langchain.schema import SystemMessage
    from langchain_community.chat_message_histories import ChatMessageHistory

    model = ChatOpenAI(model_name="gpt-4o-mini")

    # ChatMessageHistory 객체 생성
    chat_history = ChatMessageHistory()

    # System 메시지 추가 (history에 system 메세지 쌓기)
    chat_history.messages.append(SystemMessage(content="너의 이름은 햄식이이고, 아주 귀여운 햄스터야. 모든 말을 햄으로 끝내."))

    # 사용자 메시지 추가 (history에 user message 쌓기)
    chat_history.add_user_message("햄식아 나 어제 수능쳤어 대박이지")

    # AI 메시지 추가 (history에 ai message 쌓기)
    chat_history.add_ai_message("진짜햄? 고생 많았햄!!")

    ### 최종적으로 chat history 객체에는 메세지들이 쌓여있다.

    # 저장된 대화 히스토리 확인
    for msg in chat_history.messages:
        print(f"{msg.type}: {msg.content}")

    ## 히스토리를 넣어주고, 대화하기
    messages = chat_history.messages
    print(model(messages))
    ```


<br>

## 5. agent
- AI 에이전트란 주어진 명령에 대해 직접 액션 플랜을 세우고, 이를 차례대로 실행하여 완성도 높은 작업 수행이 가능한 AI 프레임워크를 뜻함

- agent 과정

    ![Image](https://github.com/user-attachments/assets/3d6dee5e-39b2-4d1c-8404-34c766af4de2){: .align-center style="width:75%;"}

    - 주어진 문제를 해결하기 위한 action이 무엇인지 생각해보고
    - 이를 해결하기 위한 도구가 무엇인지 추론하고
    - 이를 실행하여 정답을 추론

<br>
<br>

# 💡Today I Thought

## 오늘의 체크리스트
- [x] 알고리즘 코드카타 318
- [x] SQL 코드카타 120
- [x] history UI 및 데이터 연결(DB)
- [x] TIL 제출

## 회고
&nbsp;오늘은 유독 컨디션이 안좋아서 하루종일 집중을 잘 못한 것 같다. 최종 전에 컨디션 관리 잘 해야겠다..🫠