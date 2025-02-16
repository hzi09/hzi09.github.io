---
title:  "[TIL] 내일배움캠프 82일차_[Streamlit] Streamlit과 MySQL 연동하기" 

categories: 
    - TIL
tags: 
    - TIL
    - 내일배움캠프
    - Streamlit
    - MySQL


toc: True
toc_sticky: True
---

![TIL](/assets/images/TIL2.png){: .align-center style="width:35%;"}

# 👀Today I Learn
## Streamlit과 MySQL 연동
- 데이터를 실시간으로 시각화하고 관리하려면 데이터베이스와의 연동이 필요
- Streamlit의 Docs의 [Connect Streamlit to MySQL](https://docs.streamlit.io/develop/tutorials/databases/mysql)를 참조하여 진행

## MySQL DB 설정
### MySQL DB 및 테이블 생성
- MySQL에 접속하여 사용할 데이터베이스와 테이블을 생성

    ```sql
    CREATE DATABASE streamlit_db;
    USE streamlit_db;

    CREATE TABLE users (
        id INT AUTO_INCREMENT PRIMARY KEY,
        name VARCHAR(100),
        email VARCHAR(100)
    );
    ```

<br>

## Streamlit에서 MySQL 연결하기
- Streamlit 앱에서 MySQL과 연결하려면 mysql-connector-python 패키지를 설치

    ```bash
    pip install mysql-connector-python
    ```

### MySQL 접속 정보 설정
- Streamlit에서 보안적으로 MySQL 접속 정보를 관리하기 위해 `.streamlit/secrets.toml` 파일을 생성

    ```toml
    [connections.mysql]
    host = "localhost"
    port = 3306
    database = "streamlit_db"
    user = "root"
    password = "your_password"
    ```


### Streamlit 앱에서 MySQL 연결
- Streamlit 앱에서 MySQL 데이터베이스를 연결하고 데이터를 조회하는 코드

    ```sql
    import streamlit as st
    import mysql.connector

    # MySQL 연결
    conn = mysql.connector.connect(
        host=st.secrets["connections"]["mysql"]["host"],
        user=st.secrets["connections"]["mysql"]["user"],
        password=st.secrets["connections"]["mysql"]["password"],
        database=st.secrets["connections"]["mysql"]["database"]
    )
    cursor = conn.cursor()

    # 데이터 조회
    def get_users():
        cursor.execute("SELECT * FROM users")
        return cursor.fetchall()

    st.title("Streamlit과 MySQL 연동")

    if st.button("데이터 불러오기"):
        users = get_users()
        for user in users:
            st.write(user)
    ```

<br>

## Streamlit 클라우드에서 MySQL 사용하기

- Streamlit Cloud에서 MySQL을 사용하려면 `.streamlit/secrets.toml` 파일을 클라우드 환경에서 설정해야 함
    1. Streamlit Cloud의 Secrets 설정 페이지에서 접속 정보 추가
    2. MySQL 호스팅 서비스를 사용하여 원격 접속 가능하도록 설정
- 이렇게 하면 Streamlit 앱을 배포한 후에도 MySQL 데이터베이스에 안전하게 연결할 수 있음

<br>
<br>

# 💡Today I Thought

## 오늘의 체크리스트
- [x] 알고리즘 코드카타 325
- [x] SQL 코드카타 116
- [x] Streamlit 구현
- [x] TIL 작성

## 회고
&nbsp;오늘은 이것저것 하다보니까 공부를 너무 늦게 시작해버렸다😢 해야할 게 많았는데, 진짜 쥐꼬리만큼만 공부를 해버린.. 내일은 다시 월요일이니까 다시 더 열심히 해야지!🫠