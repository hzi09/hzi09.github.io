---
title:  "[TIL] 내일배움캠프 90일차_[Chat_pjt] history 트러블 슈팅" 

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
## 문제1 : 채팅 초기화 이슈
- 저장하고 종료를 누르면 위의 코드들이 삭제되어야 하는데, 계속 데이터가 남아있는 현상 발생

    ![Image](https://github.com/user-attachments/assets/1879a623-6521-48ec-b303-c11d0940d496)

- 기존코드
    ```python
        with col2:
            if st.button("종료하고 저장"):
                st.write("면접을 종료합니다.")
                st.session_state.interview_started = False
                st.session_state.show_continue_button = False  # 버튼 숨김
                st.session_state.chat_history = []  # 채팅 기록 초기화
                st.rerun()  # 페이지 새로고침
    ```

- 수정된 코드
    ```python
    with col2:
        if st.button("종료하고 저장"):
            st.write("면접을 종료합니다.")

            # 기존 대화 기록 삭제
            st.session_state.chat_history = []
            st.session_state.messages = []
            st.session_state.first_question_asked = False  # 첫 질문 여부도 리셋
            st.session_state.show_continue_button = False
            st.session_state.interview_started = False

        # 페이지 새로고침하여 완전 리셋
        st.rerun()
    ```
    - 기존코드에서는 `chat_history`만 초기화하였음
    -` chat_history` 외에도 `messages`, `first_question_asked`, `messages`까지 초기화
    - 그 후, `first_question_asked = False`로 변경하여 첫 질문을 다시 받을 수 있도록 리셋
    - 이렇게 하여 면접이 완전히 새로 시작될 수 있도록 수정


## 문제2 : DB 저장
- `챗봇 질문 ➡️ 유저 답변 ➡️ 챗봇 피드백`의 형태로 DB에 저장되어야 하지만, 챗봇의 질문이 저장이 안되는 현상이 발생
- 질문의 함수가 따로 설정되어 있었는데 그 부분을 제대로 인지하지 못해서 문제가 발생했었음
  - 질문을 생성하는 함수인 `generate_question()`에 DB를 저장할 수 있도록 설정

    ```python
    def generate_question():
        ...
        insert_chat_message(session_id, "bot", generated_question)
        st.session_state.messages.append({"role": "bot", "content": generated_question})
        ...
    ```

<br>
<br>

# 💡Today I Thought

## 오늘의 체크리스트
- [x]  알고리즘 코드카타 1문제
- [x]  SQL 코드카타 1문제
- [x]  LLM 복습
- [x]  TIL 작성

## 회고
&nbsp;오늘은 전체 코드를 좀 뜯어보면서 LLM을 복습했다. 아직도 어려운.. 내일도 시간이 있으면 조금 더 공부를 해야할 것 같다🫠 오늘 스탠다드반에서 했던 걸 참고해서 복습해보는게 최종때 도움이 될듯..!