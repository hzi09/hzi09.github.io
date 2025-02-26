---
title:  "[TIL] 내일배움캠프 92일차_[python] requirements.txt를 삭제하기" 

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
- 작업을 하다가보면 requirements.txt를 글로벌에 install 하는 문제가 자주 발생(주의하자🤯)
- 내용 정리해두고 또 실수하면 참고할 수 있도록 기록해두기

## 설치된 패키지 목록 확인
- 먼저, requirements.txt에 있는 패키지가 현재 설치된 패키지와 동일한지 확인

    ```bash
    pip list
    ```

## 삭제하기
- 다음 명령어를 실행하면, requirements.txt에 나열된 모든 패키지를 한 번에 삭제
- -y 옵션을 사용하면 삭제 여부를 묻지 않고 자동으로 제거됨

    ```bash
    pip uninstall -r requirements.txt -y
    ```

## 삭제 확인
- 아래의 명령어를 사용하여 제대로 되었는지 삭제

    ```bash
    pip freeze
    ```

<br>
<br>

# 💡Today I Thought

## 오늘의 체크리스트
- [x] 알고리즘 코드카타 1문제
- [x] SQL 코드카타 6문제
- [x] 팀프로젝트 발표
- [x] 최종 팀 회의
- [x] TIL 작성

## 회고
&nbsp;내일부터는 최종 팀프로젝트.. 잘 할 수 있겠지..? 팀원에게 민폐가 되지 않도록 열심히 해야겠다.