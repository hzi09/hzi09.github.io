---
title:  "[TIL] 내일배움캠프 89일차_[GitHub] GitHub를 활용한 협업 가이드" 

categories: 
    - TIL
tags: 
    - TIL
    - 내일배움캠프
    - GitHub
    - 협업


toc: True
toc_sticky: True
---

![TIL](/assets/images/TIL2.png){: .align-center style="width:35%;"}

# 👀Today I Learn
## 협업의 기본 흐름
1. Repository 생성 및 클론
- 팀장이 GitHub에서 저장소를 생성하고 팀원들에게 초대 링크를 공유
- 팀원들은 `git clone` 명령어로 로컬에 프로젝트를 복제
    ```bash
    git clone https://github.com/팀이름/프로젝트명.git
    ```

2. Branch 전략 설정
- `main` 또는 `develop` 브랜치는 항상 안정적인 상태를 유지해야 함
- 각 개발자는 기능 단위로 새로운 브랜치를 생성하여 작업
    ```bash
    git checkout -b feature/new-feature
    ```

3. 코드 작업 및 커밋
- 작업한 파일을 스테이징 후 커밋
    ```bash
    git add .
    git commit -m "feat: 새로운 기능 추가"
    ```

4. 원격 저장소에 푸시
- 자신의 브랜치를 GitHub에 푸시
    ```bash
    git push origin feature/new-feature
    ```

5. Pull Request(PR) 생성
- GitHub에서 `feature/new-feature` 브랜치를 `main` 또는 `develop` 브랜치로 병합하는 Pull Request(PR) 를 생성
- PR 작성 시 코드 리뷰를 위해 팀원들을 리뷰어로 지정합

6. 코드 리뷰 및 머지(Merge)
- 리뷰어가 피드백을 제공하면, 필요한 경우 수정 후 다시 푸시
- 모든 리뷰어가 승인하면 `main` 또는 `develop` 브랜치에 병합(Merge)
- 병합 후에는 `feature/new-feature` 브랜치를 삭제
    ```bash
    git branch -d feature/new-feature
    ```

7. 최신 코드 업데이트(Pull)
- 모든 팀원은 최신 코드를 반영하기 위해 `git pull` 을 수행
    ```bash
    git checkout main
    git pull origin main
    ```

<br>

## 협업 시 주의사항
1. main/develop 브랜치에서 직접 작업하지 않기
- 항상 새로운 브랜치를 생성하여 작업 후 PR을 통해 병합해야 함

2. Commit 메시지 컨벤션 통일
- 팀원 간의 코드 가독성을 위해 일관된 커밋 메시지를 사용
- 예시
    ```
    feat: 로그인 기능 추가
    fix: 로그인 버그 수정
    refactor: 데이터베이스 쿼리 최적화
    ```

3. 코드 리뷰를 적극 활용하기
- 모든 PR은 최소 한 명 이상의 팀원이 리뷰한 후 병합하는 것이 좋음
- 리뷰어는 코드 스타일, 기능 구현, 버그 가능성을 중점적으로 확인해야 함

4. 코드 충돌(Conflict) 해결하기
- 같은 파일을 여러 명이 수정하면 충돌이 발생할 수 있음
- `git pull`을 활용하여 최신 코드를 반영한 후 충돌을 직접 해결
    ```bash
    git pull origin main
    ```
- 충돌이 발생한 경우, 수동으로 수정 후 다시 커밋 & 푸시

5. PR 머지 후 로컬 브랜치 정리하기
- 사용이 끝난 브랜치는 삭제하여 깔끔한 저장소 상태를 유지
    
    ```bash
    git branch -d feature/new-feature
    ```

6. `git rebase`는 신중하게 사용하기
- `git rebase` 는 커밋 히스토리를 깔끔하게 정리하는 데 유용하지만, 협업 시 주의해야 함
- 강제 푸시(`git push --force`)는 팀원들의 작업을 덮어쓸 위험이 있으므로 사용하지 않는 것이 좋음


<br>

## GitHub Issues와 Projects
### Issues
- 작업할 기능, 버그 수정 등을 기록하고 담당자를 지정하여 협업을 효율화할 수 있음
- #이슈번호 를 커밋 메시지에 포함하면 자동으로 연동됨

    ```bash
    git commit -m "fix: 로그인 오류 해결 #12"
    ```

### Projects
- 칸반보드 형식으로 작업 진행 상황을 한눈에 파악할 수 있음
- To Do → In Progress → Done 형태로 관리하면 체계적인 작업이 가능

<br>

# 💡Today I Thought

## 오늘의 체크리스트
- [x] 알고리즘 코드카타 1문제
- [x] SQL 코드카타 1문제
- [x] History 구현
- [x] 19시 팀회의
- [x] TIL 작성

## 회고
&nbsp;오늘 History를 구현하면서 꽤나 애를 먹었는데, 진짜 예상치도 못한 실수를 했다. Langchain 코드가 아니고 기본 코드로 열심히 돌리고 있었던것.. 그러니까 안되지.. DB 컬럼명도 잘못보고 코드 짜서 처음부터 다시 짰다. 다음부터는 세세하게 확인하고 해야지🫠