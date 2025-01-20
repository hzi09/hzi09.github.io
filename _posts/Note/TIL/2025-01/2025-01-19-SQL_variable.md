---
title:  "[TIL] 내일배움캠프 54일차_[MySQL] SET, PREPARE, EXECUTE" 

categories: 
    - TIL
tags: 
    - TIL
    - 내일배움캠프
    - MySQL


toc: True
toc_sticky: True
---

![TIL](/assets/images/TIL2.png){: .align-center style="width:35%;"}

# 👀Today I Learn
## MySQL에서 변수 사용하기
- MySQL에서는 프로시저, 쿼리의 동적 생성 및 실행 시 유용하게 사용할 수 있는 다양한 변수를 제공
- MySQL 변수의 사용법과 함께 SET, PREPARE, EXECUTE 명령어에 대해 정리

### 1. MySQL 변수의 종류
- MySQL에서 변수는 크게 세 가지로 나뉨
  - 사용자 변수
    - @로 시작하며, 세션 스코프에 한정됩니다.
    - 예: `SET @var_name = 'Hello';`
  - 로컬 변수
    - 저장 프로시저나 함수 내부에서 선언하여 사용
    - 예: `DECLARE var_name VARCHAR(50);`
  - 시스템 변수
    - 서버의 설정과 관련된 변수
    - 예: `SET GLOBAL max_connections = 1000;`


### 2. 사용자 변수 사용하기

- 사용자 변수는 세션 내에서 사용 가능하며, 특정 값을 저장하고 쿼리에서 재사용할 수 있음
- 예제
    ```sql
    -- 사용자 변수 설정
    SET @name = 'Alice';

    -- 사용자 변수 사용
    SELECT @name;  -- 결과: Alice

    -- 사용자 변수를 활용한 동적 쿼리
    SET @table_name = 'users';
    SET @sql = CONCAT('SELECT * FROM ', @table_name);
    PREPARE stmt FROM @sql;
    EXECUTE stmt;
    DEALLOCATE PREPARE stmt;
    ```

- 주의
  - 사용자 변수는 명시적으로 데이터 타입을 선언하지 않으며, 처음 할당된 값에 따라 데이터 타입이 결정

### 3. 동적 SQL과 PREPARE/EXECUTE

- MySQL에서 동적 SQL은 쿼리를 실행 시점에 동적으로 생성하여 실행할 수 있게 함
- 이를 위해 `PREPARE`, `EXECUTE`, `DEALLOCATE PREPARE`를 사용합니다.

<h4>PREPARE와 EXECUTE 사용법</h4>

- `PREPARE`: 동적 SQL 문장을 준비
- `EXECUTE`: 준비된 SQL 문장을 실행
- `DEALLOCATE PREPARE`: 준비된 문장을 삭제하여 리소스를 해제
- 예제: 동적 SQL 실행
    ```sql
    -- 테이블 이름과 조건을 변수로 설정
    SET @table_name = 'orders';
    SET @condition = 'status = \"shipped\"';

    -- 동적 SQL 문 생성
    SET @sql = CONCAT('SELECT * FROM ', @table_name, ' WHERE ', @condition);

    -- PREPARE, EXECUTE, DEALLOCATE 사용
    PREPARE stmt FROM @sql;
    EXECUTE stmt;
    DEALLOCATE PREPARE stmt;
    ```

### 4. 동적 SQL에서 바인딩 변수 사용하기

- 바인딩 변수를 사용하면 동적 SQL에서 더 안전하고 효율적으로 데이터를 처리할 수 있음
- `?`를 사용한 바인딩 변수는 동적 SQL을 더 안전하게 만듦
- 예제: 바인딩 변수 사용
    ```sql
    -- 변수 설정
    SET @status = 'pending';
    SET @sql = 'SELECT * FROM orders WHERE status = ?';

    -- PREPARE와 EXECUTE 사용
    PREPARE stmt FROM @sql;
    EXECUTE stmt USING @status;
    DEALLOCATE PREPARE stmt;
    ```

<br>
<br>

# 💡Today I Thought

## 오늘의 체크리스트
- [x] 알고리즘 코드카타 211-220
- [x] SQL 코드카타 72
- [x] 백준 코딩테스트 1문제
- [x] TIL 작성

## 회고
&nbsp; SQL문제가 어려워지면서 모르는 것들이 나오기 시작했다.. 그래서 SQL에 대한 공부도 조금 필요하지 않을까 싶다. 뭐.. 나중에 자격증 따려면 하긴 해야니까.. 오늘도 알차게 마무리!