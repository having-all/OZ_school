# HTML Tag 정리

## 1. HTML이란?
**HTML(HyperText Markup Language)**은 웹 페이지의 **구조와 내용**을 만드는 언어다

| 언어 | 역할 | 비유|
|---|---|---|
| **HTML** | 내용과 구조 (제목, 문단, 사진, 표) | 🦴 뼈대 |
| **CSS** | 디자인 (색, 크기, 배치) | 👕 옷  |
| **JavaScript** | 동작 (클릭, 계산, 데이터 처리) | 💪 근육 |

> 💡 VS Code에서 `.html` 파일을 만들고 `!` + Enter를 누르면 기본 뼈대가 자동으로 만들어진다.

---

## 2. Tag의 기본 구조
```html
<태그이름 속성="값">내용</태그이름>
```

```html
<a      href="https://github.com">GitHub</a>
 ↑        ↑                          ↑     ↑ 
여는Tag  속성                        내용    닫는Tag
```

- **여는 Tag** <a>와 **닫는 Tag** </a>가 짝을 이룬다. 닫는 Tag에는 '/'가 붙는다.
- 닫는 Tag가 없는 Tag도 있다 -> **빈 Tag**: <br>, <hr>, <img>, <input>, <meta>
- Tag 안에 Tag를 넣을 수도 있다(**중첩** 가능). 이따 **나중에 연 Tag를 먼저 닫는다.**

```html
<p>이건 <strong>중요한</strong>문장이다.</p>     ✅
<p>이건 <strong>중요한</p>문장이다.</strong>.    ❌  <p><strong></strong></p> 구조가 되어야함
```

---

## 3. 문서 뼈대

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <!-- 화면에 보이는 내용-->
</body>
</html>
```

| Tag | 역할 | 
|---|---|
| <!DOCTYPE html> | "이 문서는 HTML5"라는 선언. 맨 첫 줄 |
| <html lang="en"> | 문서 전체, lang="en" 영어, lang="ko"는 한국어 문서라는 뜻 |
| <head> | 화면에 안 보이는 설정 정보 |
| <meta charset="UTF-8"> | 한글이 깨지지 않게 하는 문자 설정 |
| <meta name="viewport" ....> | 휴대폰에서도 화면 크기에 맞게 보이게 함 |
| <title> | 브라우저 탭에 표시되는 제목 |
| <body> | **화면에 보이는 모든 내용** |
| <!-- text --> | 주석, 화면에 보이지 않는 메모 |

---

## 4. Text Tag

### 제목 <h1></h1>, <h2></h2> ...... <h6></h6>
```html
 <h1>가장 큰 제목</h1>
 <h2>섹션 제목</h2> 
 <h3>소제목</h3> 
 <h4></h4>,,, <h6></h6> 순으로 작아진다
 ```

 > 💡 <h1>은 **페이지에 하나만** 쓰는 것이 원칙. 섹션 제목은 <h2>부터 사용한다.

 ### 문단과 줄바꿈
 | Tag | 설명 |
 |---|---|
 | <p> | 문단 (위아래에 자동 여백) |
 | <br> | 줄바꿈 (빈 Tag) |
 | <hr> | 가로 구분선 (빈 Tag) |

 ### 글자 꾸미기
| Tag | 설명 | 결과 |
|---|---|---|
| <strong> | 중요한 내용 (굵게) | **굵게** |
| <em> | 강조 (기울임) | *기울임* |
| <code> | 코드 글꼴 | print() |
| <span> | 의미 없는 줄 안 묶음 (스타일 적용용) | - |

> 💡 HTML에서는 엔터를 여러 번 쳐도, 공백을 여러 칸 넣어도 **한 칸으로 합쳐진다.** 줄을 바꾸려면 <br>, <p>를 써야 한다.

---

## 5. List Tag

| Tag | 설명 |
|---|----|
| <ul> | 순서 없는 목록 (Unordered List) -> 글머리 기호 • |
| <ol> | 순서 있는 목록 (Ordered List) -> 숫자형태, 알파벳, 로마자 형태로 쓸 수 있음 |
| <li> | 목록의 항목 (List Item) **반드시 <ul> 또는 <ol> 안에** |

```html
<ul style="list-style: square;">
    <li>이름</li>
    <li>주소</li> 
</ul>

<ol>
    <li>Git 설치</li>
    <li>저장소 Clone</li>
</ol>
```

### 글머리 기호 바꾸기 (list-style)
| 값 | 모양|
|---|---|
| disc | ● (기본값) |
| circle |  ○ |
| `square` | ■ |
| `none` | 기호 없음 |

---

## 6. 링크와 이미지

### 링크 <a>
```html
<a href="https://github.com/having-all/OZ_school">Respository 바로가기</a>
<a href="mailto:email@example.com">메일 보내기</a>
```

| 속성 | 설명 |
|---|---|
| href | 이동할 주소 |
| mailto | 누르면 메일 앱이 열림 |
| target="blank" | 새 탭에서 열기 |
| #아이디 | 같은 페이지 안에서 id가 붙은 위치로 이동 |

### 이미지 <img> (빈 Tag)
```html
<img src="./sunset.jpeg" alt="Profile Picture" style="width: 200px; height: 200px;">
```

| 속성 | 설명 |
|---|---|
| src | 이미지 파일 경로 (./는 "지금 HTML 파일과 같은 폴더") |
| alt | 이미지가 안보일 때 대신 나오는 text 설명 (시각장애인용 화면 낭독기도 읽어 줌) |
| width, height | 이미지 크기 |

---

## 7. 표 (Table)

```html
<table border="1">
    <thead>
        <tr>
            <th>Project</th>
            <th>내용</th>
            <th>역할</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <th>온새로미</th>
            <td>난임환자 대상 임신 성공여부 예측 AI 모델 개발</td>
            <td>PPT 작성, 발표</td>
        </tr>
    </tbody>
</table>
```

| Tag | 설명 |
|---|---|
| <table> | 표 전체 |
| <thead> | 표의 머리 (제목 줄) |
| <tbody> | 표의 몸통 (내용 줄) |
| <tr> | 한 줄 (Table Row) |
| <th> | **제목 칸** (Table Header) -> 굵게, 가운데 정렬 |
| <td> | **내용 칸** (Table Data) |

> 💡 <th>는 제목 칸에만 쓴다. 내용 칸까지 <th>로 쓰면 모든 글자가 굵게 가운데 정렬된다.

### 칸 합치기
| 속성 | 설명 | 예시 |
|---|---|---|
| colspan | 가로로 칸 합치기 | <td colspan="2"> |
| rowspan | 세로로 칸 합치기 | <td rowspan="3"> |

---

## 8. Form

사용자에게 입력을 받는 영역

```html
<form action="" style="display: flex; gap: 10px;">
    <label for="emailInput>담당자 이메일:</label>
    <input id="emailInput" type="email" placeholder="email@example.com">

    <label for="companyInput">회사명:</label>
    <input id="companyInput" type="text" placeholder="(주)Paper Company">

    <button type="submit">이력서 전송하기</button>
</form>
```

| Tag | 설명 |
|---|---|
| <form> | 입력 양식 전체, 'action'에 데이터를 보낼 주소 |
| <label> | 입력칸의 이름표, 'for'가 'input'의 'id'와 **같아야** 연결됨 |
| <input> | 입력값 (빈 태그) |
| <button> | 버튼 |
| <textarea> | 여러 줄 입력칸 |
| <select> + <option> | 드롭다운 선택 |

### <input>의 type
| type | 모양 |
|---|---|
| text | 일반 글자 |
| email | 이메일 (형식 자동 검사) |
| password | 비밀번호 (●●●로 가려짐) |
| number | 숫자 |
| data | 날짜 선택 |
| checkbox | 체크박스 (여러 개 선택) |
| radio | 라디오 버튼 (하나만 선택) |
| file | 파일 첨부 |

> ⚠️ HTML 만으로는 데이터를 실제로 **전송, 저장할 수 없다.** 받아서 처리할 서버(예: FastAPI)가 필요하다.

---

## 9. Semantic Tag
<div> 대신 **의미가 있는 이름**의 tag로 영역을 나무면, 코드를 읽기 쉽고 검색엔진과 화면 낭독기도 구조를 이해한다.

```html
<body>
    <nav>상단 메뉴</nav>
    <main>
        <header>프로필</header>
        <section>About Me</section>
        <section>
            <article>프로젝트 1</article>
            <article>프로젝트 2</article>
        </section>
    </main>
    <footer>© 2026 홍길동</footer>
</body>
```

| Tag | 의미 |
|---|---|
| <header> | 머리 부분 (로고, 제목, 소개) |
| <nav> | 메뉴 |
| <main> | 핵심 본문 (페이지에 하나) |
| <section> | 주제별 구역 |
| <article> | 독립된 내용 하나 (글, 카드) |
| <aside> | 옆 부가 정보 (사이드바) |
| <footer> | 꼬리 부분 (저작권, 연락처) |
| <div> | 의미 없는 묶음 상자 (배치용) |

### <div> VS <span>
| | <div> | <span> |
|---|---|---|
| 종류 | **블록** 요소 | **인라인** 요소 |
| 차지하는 공간 | 한 줄 전체 | 내용만큼만 |
| 다음 요소 | 아래 줄로 내려감 | 옆에 이어서 붙음 |
| 용도 | 큰 영역 묶기 | 문장 속 일부 꾸미기 |

---

## 10. 자주 쓰는 속성

모든 Tag에 쓸 수 있는 공통 속성

| 속성 | 설명 |
|---|---|---|
| id | 고유 이름 (페이지에 하나뿐) |
| class | 디자인을 묶어 적용할 이름 (하나의 클래스 안에서 사용 가능) |
| style | 그 자리에서 바로 CSS 적용 |
| title | 마우스를 올리면 나오는 설명 |

### style 쓰는 법
```html
<태크 style="속성: 값; 속성:값;">
```
- 속성과 값 사이는 **콜론 ':'**
- 각 설정의 끝은 **세미콜론 ';'**

| 자주 쓰는 CSS | 설명 | 예시 |
|---|---|---|
| color | 글자 색 | color: #333; |
| background-color | 배경 색 | background-color: #f5f5f5; |
| font-size | 글자 크기 | font-size: 18px; |
| width / height | 너비 / 넓이 | width: 200px; height: 300px; |
| margin | **바깥** 여백 | margin-bottom: 40px; |
| padding | **안쪽** 여백 | padding: 10px; |
| border | 테두리 | border: 1px solid #ccc; |
| text-align | 글자 정렬 | text-align: center; |

---

## 11. style로 배치하기 (float, flex)

### float: 사진 옆으로 글 흐르게 하기
```html
<img src="./sunset.jpeg" style="width: 200px; float: left; margin-right: 20px; margin-bottom: 40px;">
<p>사진 오른쪽으로 흐르는 글</p>

<div style="clear: both;"></div> <!-- float 해제. 다음 내용은 사진 아래부터 -->
```
| 속성 | 설명 |
|---|---|
| float: left | 왼쪽에 띄우고 글이 오른쪽으로 흐름 |
| clear: both | float 효과 끝내기 (안하면 아래 내용까지 옆으로 딸려 올라감) |

### flex: 나란히 배치하기 
```html
<div style="display: flex; gap: 20px;">
    <img src="./sunset.jpeg" style="width: 200px; height: 200px;">
    <ul style="height:200px; margin: 0; display: flex; flex-direction: colum; justify-content: space-between;">
        <li>이름: 김태숙</li>
        <li>거주지: 대한민국, 세종특별자치시</li>
    </ul>
</div>
```
| 속성 | 설명 |
|---|---|
| display: flex | 안의 요소들을 가로로 나란히 |
| gap | 요소 사이 간격 |
| flex-direction: column | 세로로 쌓기 |
| align-items: center | 세로 방향(교차축) 가운데 정렬 |
| justify-content: space-between | 첫, 끝 요소를 양 끝에 두고 나머지를 고르게 배치 |

---

## 12. 자주 하는 실수

| ❌ 잘못된 코드 | ✅ 올바른 코드 | 이유 |
|---|---|---|
| `style="list-style; square"` | `style="list-style: square;"` | 속성과 값 사이는 콜론 `:` |
| `<ul><li>A</li><br><li>B</li></ul>` | `<ul><li>A</li><li>B</li></ul>` | `<ul>` 안에는 `<li>`만 |
| `<li>` 만 단독으로 사용 | `<ul>` 또는 `<ol>`로 감싸기 | `<li>`는 목록 안에서만 |
| 내용 칸을 `<th>`로 작성 | 내용 칸은 `<td>` | `<th>`는 제목 칸 |
| `<label for="companuInput">` + `<input id="companyInput">` | `for`와 `id` 철자 일치 | 철자가 다르면 연결 안 됨 |
| 짝 없는 `</h1>` | 지우기 | 여는 태그 없는 닫는 태그 |
| `<form>`만 열고 안 닫음 | `</form>` 추가 | 열었으면 닫기 |
| float 후 `clear` 없음 | `<div style="clear: both;"></div>` | 아래 내용이 옆으로 딸려 올라감 |
| `<html lang="en">` (한국어 페이지) | `<html lang="ko">` | 문서 언어 정확히 표시 |

---

## 13. Tag 요약표

| 분류 | Tag | 한 줄 설명 |
|---|---|---|
| 뼈대 | <html> <head> <body> | 문서 / 설정 / 보이는 내용 |
| 설정 | <meta> <title> | 문자,화면 설정 / 탭 제목 |
| 제목 | <h1> ~ <h6> | 큰 제목 ~ 작은 제목 |
| 텍스트 | <p> <br> <hr> | 문단/ 줄바꿈 / 구분선 |
| 강조 | <strong> <em> <code> | 굵게 / 기울임 /코드 |
| 목록 | <ul> <ol> <li> | 순서 없는 / 순서 있는 / 항목 |
| 링크 | <a href=" "> | 다른 페이지로 이동 |
| 이미지 | <img src=" " alt=" "> | 이미지 넣기 |
| 표 | <table> <tr> <th> <td> | 표 / 줄 / 제목 칸 / 내용 칸 |
| 폼 | <form> <label> <input> <button> | 양식 / 이름표 / 입력칸 / 버튼 |
| 구조 | <header> <nav> < main> <section> < article> <footer> | 의미 있는 영역 나누기 |
| 묶음 | <div> <span> | 블록 묶음 / 줄 안 묶음|