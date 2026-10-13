# CSS

## 1. CSS란

**CSS (Cascading Style Sheets)**는 HTML로 만든 내용에 **디자인 (색, 크기, 간격, 배치)**을 입히는 언어

| CSS로 하는 일 | 예시 |
|---|---|
| 글자 꾸미기 | 글자 색, 크기, 폰트 |
| 여백과 위치 | 여백, 정렬, 위치 |
| 레이아웃 | Flex, Grid -> 화면에 요소를 어떻게 배치할지 |
| 반응형 디자인 | 화면 크기에 따라 레이아웃이 자동으로 바뀜 |

> 💡 **HTML = 구조(뼈대)**, **CSS = 모양과 배치(옷)**
> 태그 자체에 의미를 담는 **Semantic HTML** (header, main, footer)로 구조를 잡고, 디자인은 CSS로 입힌다.

---

## 2. CSS 적용 방식

### 1) Inline Style
태그에 style 속성으로 직접 작성한다.

**기본 HTML**
```html
<body>
    <p>홍길동</p>
    <p>백엔드 개발자</p>
    <p>Copyright &#169 홍길동</p>
</body>
```

**font-size & font-weight 추가**
```html
<p style="font-size: x-large; font-weight: bold;">홍길동</P>
<p style="font-size: medium;">백엔드 개발자</p>
<p style="font-size: xx-small;">Copyright &#169 홍길동</p>
```

**text-align 추가** -> 태그마다 반복해야 해서 번거로움
```html
<p style="font-size: x-large; font-weight: bold; text-align: center;">홍길동</P>
<p style="font-size: medium; text-align: center">백엔드 개발자</p>
<p style="font-size: xx-small; text-align: center">Copyright &#169 홍길동</p>
```

**공통 스타일은 부모에게** -> text-align은 묶음으로 처리한다
```html
<div style="text-align: center;">
    <p style="font-size: x-large; font-weight: bold;">홍길동</P>
    <p style="font-size: medium;">백엔드 개발자</p>
    <p style="font-size: xx-small;">Copyright &#169 홍길동</p>
</div>
```

**Semantic HTML로 바꾸기**
```html
<header style="font-size: x-large; font-weight: bold; text-align: center;">홍길동</header>
<main style="font-size: medium; text-align: center">백엔드 개발자</main>
<footer style="font-size: xx-small; text-align: center">Copyright &#169 홍길동</footer>
```

> ⚠️ 여는 태그와 닫는 태그가 같아야 한다. <header>...</p>처럼 짝이 틀리면 브라우저가 빈 <p>를 만들어 **의도하지 않은 간격**이 생기고, header가 닫히지 않아 아래 요소까지 header 스타일을 물려 받는다.

### 2) Internal CSS 
<head> 안의 <style> 태그에 작성한다.

**기본 구조** : selector {property: value;}
```html
<head>
    <style>
        p { color: red;}
    </style>
</head>
```

인라인 스타일을 Internal CSS로 옮기면 HTML이 깔끔해진다
```html
<style>
    div {text-align: center;}
    header {font-size: x-large; font-weight: bold;}
    main {font-size: medium;}
    footer {font-size: xx-small;}
</style>
```

### 3) External CSS 
별도의 CSS 파일을 분리해서 관리하는 방법. <head>에서 <link>로 연결한다.
```html
<head>
    <link rel="stylesheet" href="./style(파일이름).css">
</head>
```

### 4) 3가지 방식 비교

| Inline | Internal | EXternal |
|---|---|---|
| 작성 위치 | 태그 안에 style=" " | <head>의 <style> | 별도 .css 파일 |
| 적용 범위 | 사용된 태그 하나 | HTML 파일 | 연결한 모든 HTML 파일 |
| 재사용| ❌ | △ | ✅ |
| 장점 | 바로 확인 가능 | HTML 본문이 깔끔 | 여러 페이지가 같은 디자인 공유 |
| 단점 | 반복, 수정 어려움 | 다른 파일에서 재사용 불가 | 경로가 틀리면 적용 안됨 |

---

## 3. Selectors (선택자)

**어떤 HTML 요소에 스타일을 적용할지 지정하는 규칙**

### 1) 기본 Selector
| Selector | 문법 | 의미 |
|---|---|---|
| 전체 selector | * | 해당 태그 전부 |
| 태그 selector | div | 해당 태그 전부 (묶음) |
| 클래스 selector | .class | class="해당class"인 요소 전부 |
| ID selector | #id | id="해당id"인 요소 **하나** |

### 2) 결합자(관계) Selector
| Selector | 문법 | 의미 |
|---|---|---|
| 자손 선택자 | div p | div 안에 있는 **모든** p (깊이 상관없음) | 
| 자식 선택자 | div > p | div의 ** 바로 아래 자식** p만 |  
| 인접 형제 | div + p | div **바로 다음**에 오는 p **하나** |   
| 일반 형제 | div ~ p | div **뒤에 오는 모든** 형제 p |      

```html
<div>
    <p>A</p>                    <!-- div p ✅  div > p ✅ -->
    <section><p>B</p></section> <!-- div p ✅  div > p ❌ -->
</div>
<p>C</p>                        <!-- div + p ✅  div ~ p ✅ -->
<p>D</p>                        <!-- div + p ❌  div ~ p ✅ -->
```

### 3) 속성 Selector
| Selector | 의미 |
|---|---|
| a[href] | href 속성을 **가진** a 태그 |  
| input[type="text"] | type 속성이 **text인** input 태그 |    


### 4) 가상 클래스 Selector
**요소의 상태**를 기준으로 선택한다.

| Selector | 의미 |
|---|---|
| :hover | 마우스를 요소 위에 올렸을 때 |   
| :focus | 요소가 focus를 가졌을 때 (입력칸 클릭 등) |     
| :active | 요소를 클릭하고 있는 순간 |
| :nth-child() | 부모 기준으로 n번째 자식 요소 | 
| :not() | 괄호 안 조건이 **아닌** 요소 |  

```css
.github-link:hover {
    text-decoration: underline;     /*마우스 올리면 밑줄 */
}
```

### 5) Selector 우선 순위
같은 요소에 여러 규칙이 겹치면 위에 있을수록 우선한다.

| 순위 | 종류 | 예시 |
|---|---|---|
| 1 | !important | color: red !important; |   
| 2 | inline style | style= "" |      
| 3 | id 선택자 | #id |   
| 4 | class/속성/pseudo-class | .class, [type], :hover |  
| 5 | 태그 선택자 | div, p |   
| 6 | 전체 선택자 | * |  

✅ **id > class > tag**, 같으면 **나중 코드 우선**

> 💡 **상속 주의** : color, font-size, text-align 같은 글자 속성은 부모 -> 자식으로 상속되지만, **자식에게 직접 지정된 값이 상속값보다 항상 우선순위이다.**
> * {color: black;}을 쓰면 모든 자식에게 검은색이 직접 지정되어, 부모에 준 색을 물려 받지 못한다. -> 기본 글자색은 body에 적용한다.

---

## 4. 텍스트, 배경 스타일 

### 1) 속성
| 속성 | 설명 | 예시 |
|---|---|---|
| font-size | 글자 크기 | x-large, medium, xx-small, 2.4rem |   
| font-weight | 글자 굵기 | bold, normal |      
| text-align | 가로 정렬 | center, left, right |   
| color | 글자 색 | gray, darkcyan, inherit(부모 색 그대로) |  
| background-color | 배경 색 | red, skyblue,,, |   
| text-decoration | 밑줄 | none(밑줄 제거), underline |  
| font-family | 글꼴 | Times New Raman 등|   
| font | 글꼴 관련 속성 한 번에 | bold x-large 'Times New Roman' |  

### 2) background-color
```css
header {
    font-size: x-large;
    font-weight: bold;
    background-color: red;
}

main {
    font-size: medium;
    background-color: green;
}

footer {
    font-size: xx-small;
    background-color: yellow;
}
```

### 3) font-family
```css
header {
    font-family: 'Times New Roman', Times, serif;
}
```
- 앞에서부터 차례로 시도하고, 없으면 다음 글꼴로 사용
- 마지막에는 'serif'(명조 계열), 'sans-serif(고딕계열)' 같은 기본 계열을 둔다

**구글 폰트 적용** (https://fonts.google.com/): <link>로 폰트를 불러온 뒤 'font-family'에 이름을 적는다.
```css
body {
    margin: 0;
    font-family: "BBH Bogle", sans-serief;
}
```

### 4) font (단축 속성)
- 순서: **font-weight -> font-size -> font-family**
- font-size와 font-family는 **반드시 포함**
```css
header {
    font: bold x-large 'Times New Roman', Times, serif;
}
```

### 5) 링크 꾸미기
```html
<a class="github-link" href="https://github.com/OZ_school">My GitHub</a>
```
```css
.github-link {
    font-size: small;
    color: gray;
    text-decoration: none;      /* 기본 밑줄 제거 */
}

.github-link:hover {
    text-decoration: underline;  /* 마우스 올리면 밑줄 */
}
```

### 6) 아이콘 추가 (fontawesome 이용)
웹에서 쓰는 아이콘을 **글꼴처럼** 제공하는 라이브러리 (https://fontawesome.com/)
```html
<link
    rel="stylesheet"
    href=""https://cdnjs.cloudflare.com/ajax/libs/font-awesome/7.0.1/css/all.min.css"
/>

<a class="github-link" href="https://github.com/OZ_school">
    <i class="fa-brands fa-github"></i>GitHub
</a>
```
> 💡 아이콘이 글자처럼 취급되므로 color, font-size로 색과 크기를 바꿀 수 있다.

---

## 5. CSS 박스 모델

**모든 HTML 요소를 '사각형 박스'로 보고 크기와 여백을 계산하는 규칙**
```
┌─────────────────────────────────┐
│            margin               │  바깥 여백 (투명)
│   ┌─────────────────────────┐   │
│   │         border          │   │  테두리
│   │   ┌─────────────────┐   │   │
│   │   │     padding     │   │   │  안쪽 여백 (배경색 적용됨)
│   │   │   ┌─────────┐   │   │   │
│   │   │   │ content │   │   │   │  실제 내용 (width × height)
│   │   │   └─────────┘   │   │   │
│   │   └─────────────────┘   │   │
│   └─────────────────────────┘   │
└─────────────────────────────────┘
```

| 요소 | 설명 |
|---|---|
| **마진 (margin)** | 테두리 바깥, 다른 요소와 간격 |   
| **테두리 (border)** | 박스의 테두리 |     
| **패딩 (padding)** | 콘텐츠와 테두리 사이의 안쪽 여백 |   
| **콘텐츠 (content)** | 글자, 이미지 등 실제 내용 |  

