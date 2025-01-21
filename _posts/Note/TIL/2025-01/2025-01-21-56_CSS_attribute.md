---
title:  "[TIL] 내일배움캠프 56일차_[CSS] CSS 속성정리" 

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
## CSS 속성의 역할과 사용법
- CSS를 작성할 때, 특정 속성들이 어떤 역할을 하고 어떻게 동작하는지 이해하는 것은 매우 중요
  - CSS가 있어야 깔끔하게 작성할 수 있기때문에, 자주 쓰이는 내용만 작성
- [CSS 참고자료](https://developer.mozilla.org/ko/docs/Web/CSS)를 참고하여 작성

### 1. position

```css
position: static;
```

- `position` 속성은 요소의 위치를 설정하는 방법을 정의
  - `static`(기본값): 위치를 따로 지정하지 않고 문서의 흐름에 따라 배치
  - `relative`: 요소를 원래 위치를 기준으로 상대적으로 이동시킬 수 있음
  - `absolute`: 가장 가까운 `position: relative` 또는 `absolute` 부모 요소를 기준으로 위치를 설정
  - `fixed`: 화면(viewport)을 기준으로 위치를 고정하며, 스크롤해도 움직이지 않음
  - `sticky`: 스크롤에 따라 상대적으로 움직이다가 특정 위치에서 고정


### 2. top, left, right, bottom

```css
position: relative;
top: 40px; left: 40px;
```

- 요소의 위치를 상하좌우 기준으로 조정
  - `top: 0`: 요소의 위쪽 경계를 기준으로 위치를 0으로 설정
  - `left: 0`: 요소의 왼쪽 경계를 기준으로 위치를 0으로 설정
- `position` 속성이 `relative`, `absolute`, `fixed`, `sticky`일 때만 효과 있음

### 3. z-index

```css
z-index: 1000;
```

- 요소의 쌓이는 순서를 정의
- 큰 값일수록 요소가 위에 표시
- 음수를 사용할 경우, 요소가 뒤로 배치
- 기본값은 `auto`이며, `position` 속성이 설정된 요소에서만 의미가 있음

### 4. display

```css
display: flex;
display: inline;
```

- 요소의 박스 유형을 정의
  - `block`: 요소가 블록처럼 동작하며, 줄 바꿈이 일어남
  - `inline`: 요소가 인라인으로 동작하며, 콘텐츠 크기만큼만 차지
  - `flex`: 요소를 플렉스 컨테이너로 설정해, 자식 요소를 정렬하고 배치할 수 있음
- 예제
    
    ```css
    display: flex;
    display: inline;
    ```


### 5. flex 관련 속성

```css
flex-direction: column;
justify-content: space-around;
align-items: center;
flex: 1;
```

- 플렉스 컨테이너의 자식 요소 배치를 설정
  - `flex-direction`: 자식 요소의 정렬 방향을 지정
    - `row`: 가로 방향(기본값)
    - `column`: 세로 방향
  - `justify-content`: 자식 요소 간의 수평 공간을 정의
    - `space-around`: 요소 간의 간격이 동일하며, 양 끝에도 여백이 생김
  - `align-items`: 자식 요소의 수직 정렬을 정의
    - `center`: 자식 요소를 수직으로 가운데 정렬
  - `flex`: 플렉스 항목이 부모 요소 내에서 차지할 공간을 설정(1은 남은 공간을 모두 차지함)


### 6. margin과 padding

```css
margin: 0;
padding: 10px 15px;
```

- `margin`: 요소의 외부 여백을 설정(다른 요소와의 거리 조정)
  - 0: 여백 없음.
- `padding`: 요소의 내부 여백을 설정합니다. (내용과 테두리 사이 거리)
  - 10px 15px: 위/아래는 10px, 좌/우는 15px 여백.

### 7. border

```css
border: none;
border-radius: 5px;
```

- 요소의 테두리를 설정
  - `border`: 테두리 스타일과 두께, 색상을 설정
    - `none`: 테두리 없음
  - `border-radius`: 테두리의 모서리를 둥글게 만듦
    - 값이 클수록 모서리가 더 둥글어짐

### 8. transition

```css
transition: background-color 0.3s ease;
```

- 속성의 변화가 즉시 반영되지 않고, 일정 시간 동안 부드럽게 전환됨
  - `background-color`: 배경색 변경에만 적용
  - `0.3s`: 전환 효과의 지속 시간
  - `ease`: 전환 효과의 가속/감속 패턴을 지정



### 9. background-color와 color

```css
background-color: #836489;
color: #ffffff;
```

- `background-color`: 요소의 배경색을 설정
- `color`: 텍스트 색상을 설정
- 색상 값은 `#`으로 시작하는 HEX 코드, `rgb()` 또는 기본 색상 이름으로 지정 가능


### 10. cursor

```css
cursor: pointer;
```

- 사용자가 요소 위에 마우스를 올릴 때 커서 모양을 설정
  - `pointer`: 링크처럼 손가락 모양으로 표시
  - `default`: 기본 커서 모양
  - `text`: 텍스트 편집 커서

### 11. text-align과 text-decoration

```css
text-align: center;
text-decoration: none;
```

- `text-align`: 텍스트를 정렬
  - `center`: 가운데 정렬
  - `left`: 왼쪽 정렬
  - `right`: 오른쪽 정렬
- `text-decoration`: 텍스트에 장식을 추가하거나 제거
  - `none`: 밑줄 등 모든 장식을 제거


### 12.  width와 height

```css
width: 100%;
height: 60px;
```

- 요소의 너비와 높이를 설정
  - 100%: 부모 요소의 전체 너비를 차지
  - 60px: 고정된 높이로 설정

<br>
<br>

# 💡Today I Thought

## 오늘의 체크리스트
- [x]  알고리즘 코드카타 231-240
- [x]  SQL 코드카타 73
- [ ]  백준 코딩테스트 1문제
- [x]  장고 도전과제 : 좋아요 , 댓글 구현
- [x]  TIL 작성

## 회고
&nbsp; CSS는 만지면 만질수록 예뻐지니까 욕심이 생겨버린다.. 분명 footer만 고정하려고 했는데 정신 차려보니 전체적인 틀을 만지고 있는 나를 발견해벌여... 오늘은 오전에 병원을 다녀왔다. 감기라고 하니까 그나마 다행..🤒 독감걸리면 우리 갱얼지들은 오쫀담.. 