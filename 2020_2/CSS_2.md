# CSS 2

## 3. 그리드
### 3-1. 그리드 레이아웃이란?
1. 화면을 바둑판 형식으로 나누고 그에따라 배치를 하는 것입니다.
2. 장점:편리하고 손쉽게 다양한 레이아웃 표현할 수 있습니다.
3. 단점:브라우저 호환성을 고려 해야합니다.   

### 3-2. 요소를 나란히 배치하기 
`코드설명`
1. 부모 박스가 그리드 박스의 역할을 담당하므로 자식 요소를 감싸는 부모 박스를 만들어줘야 합니다. 부모와 자식의 구분을 위해 부모 박스에 grid라는 id값을 주었습니다.
2. 부모 박스를 자식 박스와 구별하기 위해 서로 다른 색상의 테두리를 그렸줬습니다. (부모는 분홍색 자식은 회색)
3. 본격적으로 그리드 레이아웃을 위해 display를 grid로 설정합니다. (여기까지만 해서는 아무 변화가 없다)
4. 자식 박스를 나란히 배치하기 위해 grid-template-columns 값을 설정해줍니다. 아래 예제에서는 왼쪽 영역은 150px로 고정하고 오른쪽 영역은 1fr로 설정했습니다. (fr은 그리드 컨테이너의 비율입니다. 창 크기에 따라 가변적으로 변합니다.)

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title></title>
    <style>
      #grid{
        border:5px solid pink;
        display:grid;
        grid-template-columns: 150px 1fr;
      }
      div{
        border:5px solid gray;
      }
    </style>
  </head>
  <body>
    <div id="grid">
      <div>NAVIGATION</div>
      <div>Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.</div>
    </div>
  </body>
</html>
```
<img src="./img/그리드1.PNG">

### 3-3. 본격적으로 그리드 사용해보기
-> ol태그와 h2,p태그를 나란히 배치해 보자
`코드설명`
1. h2태그와 p태그를 div태그를 사용하여 묶어줍니다. (CSS부분)
2. ol태그와 h2 & p태그를 나란히 배치하기 위해 그리드 레이아웃을 사용합니다. div태그로 묶어 부모 박스를 만들어줍시다.
3. display를 grid로 설정하고 grid-template-columns 값을 설정해줍니다.
```html
<!doctype html>
<html>
<head>
  <title>WEB - CSS</title>
  <meta charset="utf-8">
  <style>
    body{
      margin:0;
    }
    a {
      color:black;
      text-decoration: none;
    }
    h1 {
      font-size:45px;
      text-align: center;
      border-bottom:1px solid gray;
      margin:0;
      padding:20px;
    }
    ol{
      border-right:1px solid gray;
      width:100px;
      margin:0;
      padding:20px;
    }
    #grid{
      display: grid;
      grid-template-columns: 150px 1fr;
    }
    #grid ol{
      padding-left:33px;
    }
    #grid #article{
      padding-left:25px;
    }
  </style>
</head>
<body>
  <h1><a href="index.html">WEB</a></h1>
  <div id="grid">
    <ol>
      <li><a href="1.html">HTML</a></li>
      <li><a href="2.html">CSS</a></li>
      <li><a href="3.html">JavaScript</a></li>
    </ol>
    <div id="article">
        <h2>CSS</h2>
        <p>
          Cascading Style Sheets (CSS) is a style sheet language used for describing the presentation of a document written in a markup language.[1] Although most often used to set the visual style of web pages and user interfaces written in HTML and XHTML, the language can be applied to any XML document, including plain XML, SVG and XUL, and is applicable to rendering in speech, or on other media. Along with HTML and JavaScript, CSS is a cornerstone technology used by most websites to create visually engaging webpages, user interfaces for web applications, and user interfaces for many mobile applications.
        </p>
      </div>
  </div>
  </body>
  </html>
```
<img src="./img/그리드2.PNG">

## 4. 반응형 디자인
### 4-1. 반응형 디자인이란? 
1. 화면의 크기에따라 웹페이지의 요소들이 바뀌는 것입니다.   
2. 핸드폰,태블릿,데스크탑등 화면의 크기에 따라 웹페이지의 배치가 달라집니다.

### 4-2. 미디어쿼리 
1. 특정 조건을 만족할때만 css를 적용하는 문법입니다.
2. @media(조건)형식으로 사용하고 조건에는 주로 화면 크기와 관련된 내용이 들어갑니다.
3. 예를들어 max-width:800px -> 화면 크기가 800px이하일때 적용할 css코드를 작성하기
4. 아래 예제를 시행하면 화면 크기가 800px 이하일때는 화면에 아무것도 보이지 않습니다.
5. 화면 크기는 개발자모드에서 알 수 있습니다.
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title></title>
    <style>
      div{
        border:10px solid green;
        font-size:60px;
      }
      @media(max-width:800px) {
        div{
          display:none;
        }
      }
    </style>
  </head>
  <body>
    <div>
      Responsive
    </div>
  </body>
</html>
```
### 4-3. 미디어 쿼리를 이용하여 반응형 웹 만들기
```그리드 2번째 예제를 바꿔봅시다```
`코드설명`
1. 화면 크기가 800px보다 작아지면 화면이 바뀌게 해봅시다.   
->@media(max-width:800px)
2. 그리드 예제에서 그리드 레이아웃을 해제하고 display를 block레벨로 바꿔줍니다. (블록레벨!)
3. 선이 보기 싫으니 없애줍니다.   
-> ol과 h1태그의 border 값에 none 설정하기
```html
<!doctype html>
<html>
<head>
  <title>WEB - CSS</title>
  <meta charset="utf-8">
  <style>
    body{
      margin:0;
    }
    a {
      color:black;
      text-decoration: none;
    }
    h1 {
      font-size:45px;
      text-align: center;
      border-bottom:1px solid gray;
      margin:0;
      padding:20px;
    }
    ol{
      border-right:1px solid gray;
      width:100px;
      margin:0;
      padding:20px;
    }
    #grid{
      display: grid;
      grid-template-columns: 150px 1fr;
    }
    #grid ol{
      padding-left:33px;
    }
    #grid #article{
      padding-left:25px;
    }
    @media(max-width:800px){
      #grid{
        display: block;
      }
      ol{
        border-right:none;
      }
      h1 {
        border-bottom:none;
      }
    }
  </style>
</head>
<body>
  <h1><a href="index.html">WEB</a></h1>
  <div id="grid">
    <ol>
      <li><a href="1.html">HTML</a></li>
      <li><a href="2.html">CSS</a></li>
      <li><a href="3.html">JavaScript</a></li>
    </ol>
    <div id="article">
        <h2>CSS</h2>
        <p>
          Cascading Style Sheets (CSS) is a style sheet language used for describing the presentation of a document written in a markup language.[1] Although most often used to set the visual style of web pages and user interfaces written in HTML and XHTML, the language can be applied to any XML document, including plain XML, SVG and XUL, and is applicable to rendering in speech, or on other media. Along with HTML and JavaScript, CSS is a cornerstone technology used by most websites to create visually engaging webpages, user interfaces for web applications, and user interfaces for many mobile applications.
        </p>
      </div>
  </div>
  </body>
  </html>
```
<img src="./img/미디어쿼리.PNG">
화면의 크기가 달라지면 그리드 2번 예제와 다른 배치의 화면이 나옵니다!
 