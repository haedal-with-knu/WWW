## Github Pages

python의 django와, Flask 라이브러리를 사용해서 서버를 켜보았다.  
그런데, 우리가 작은 프로젝트를 하는데 컴퓨터 한대를 계속 켜놓거나, 돈을 내고 웹 서버를 빌릴 수는 없다.(ㅠㅠ)  
그런 우리를 위해서 github에서 서버를 무료로 빌려준다!  
물론 공짜로 빌려주는 것이라 데이터를 저장한다거나 할 수는 없지만 연습용이나 간단한 포트폴리오를 만들어서 저장할 수 있다.  
지금부터 한번 서버를 공개해보자! ~~이번에는 쉬울 것이다..~~  

먼저 `github`에 접속해서 새 레포지토리를 만든다.  
여기서 주의할 점은 레포지토리의 이름을 `username.github.io`의 형태로 만들어야 한다.  

![page_repo](./statics/page_repo.PNG)  

레포지토리를 만들었다면 이제 이전시간에 만든 `HTML`파일과 `CSS`파일을 넣어보자!  
여기서 주의할 점은 `HTML`파일의 이름은 `index.html`로 통일해주어야 `github`에서 인식해서 `html`을 적용해준다.  
파일을 넣었다면 이제 완성입니다! 주소창에 `username.github.io`를 타이핑해주면  
우리가 만든 페이지가 나타나는걸 확인할 수 있다.  

![github_pages1](./statics/github_pages1.PNG)
## Bootstrap

이전시간까지 우리가 직접 웹페이지를 만들어서 github pages를 이용해 웹상에서 호스팅 해봤다.  
하지만 솔직히 말해서! 우리가 만든 웹페이지들은 전문가들이 만든 페이지들에 비해서 부족할 수 밖에 없다.  
이번시간에는 `Bootstrap`을 통해 전문가들이 만들어놓은 페이지 템플릿을 사용해서 더 완성도 있는 페이지를 만들어 보도록 하자.  

### Bootstrap?
그럼 과연 부트스트랩은 뭘까?  
부트스트랩은 웹사이트를 쉽게 만들 수 있게 돕는 프론트엔드 프레임워크들 중 하나이다.  
하나의 CSS로 휴대폰, 태블릿, 데스크탑까지 다양한 기기에서 작동하며  
다양한 기능을 제공하여 우리가 쉽게 웹사이트를 제작, 유지, 보수할 수 있도록 도와준다.  

부트스트랩이 뭔지 대충 알았으니 실제로 적용해보면서 배워보자!  
부트스트랩을 사용하는 다양한 방법이 있지만 우리는 CDN을 통해서 부트스트랩을 사용할 것이다.  
CDN은 멀리 있는 사용자에게 컨텐츠를 더 빠르게 제공할 수 있는 기술인데, 사용자가 Origin Server로부터  
Content를 다운받는 대신, 사용자와 가까운 곳에 있는 Cache Server로부터 Content를 가져오는 방법이다.
아래의 코드를 `html`파일의 `<head>`태그 안에 추가하면 부트스트랩이 제공하는 CSS를 사용할 준비가 되었다.  
```html
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.2/css/bootstrap.min.css">
```  

  
### Navbar 만들기
먼저 navbar부터 만들어 보자.
`div`의 `class`를 `navbar navbar-default`, `navbar navbar-inverse`등으로 설정하여 navbar의  
형태를 잡을 수 있다. 그리고 내부에 `container`를 만들어 그 안에 우리가 넣고싶은 것들을 넣을 수 있다.  
`container`는 부트스트랩에서 사이트 콘텐츠를 감싸고 반응형 레이아웃을 만들기 위한 요소이므로 지정해주는게 좋다.  
```html
<body>
    <div class="navbar navbar-inverse">
        <div class="container">
        
        </div>
    </div>
</body>
```  
  
`container` 안에 로고를 넣을 `navbar-header`를 `div` 태그로, 메뉴를 나타낼 부분을 `ul` 태그로 지정한다.      
```html
<body>
    <div class="navbar navbar-inverse">
        <div class="container">
            <div class="navbar-header"></div>
            <ul class="nav navbar-nav"></ul>
        </div>
    </div>
</body>
```  
  
`<a>`태그를 이용해서 로고를 누르면 다른 홈페이지로 이동하게 만들어보자.  
로고는 부트스트랩에서 제공하는 아이콘을 사용할 것이다.  
더 다양한 아이콘을 [여기](http://bootstrapk.com/components/#glyphicons)를 참고해서 사용하자  
메뉴는 `<ul>` 태그 안에 `<li>`와 `<a>`를 조합해서 만들어 준다.  
하나의 `<li>`에는 `active`를 클래스로 주어 현재 해당 메뉴에 들어와 있는 것처럼 보이게 해주자.
```html
<body>
    <div class="navbar navbar-inverse">
        <div class="container">
            <div class="navbar-header">
                <a href="http://haedal.io/" class="navbar-brand">
                    Haedal Programming
                    <i class="glyphicon glyphicon-cloud"></i>
                </a>
            </div>
            <ul class="nav navbar-nav">
                <li class="active"><a href="#">메뉴1</a></li>
                <li><a href="#">메뉴2</a></li>
                <li><a href="#">메뉴3</a></li>
                <li><a href="#">메뉴4</a></li>
            </ul>
        </div>
    </div>
</body>
```  

### 메뉴 만들기
페이지의 윗 부분에 `Navigationbar`가 있다면, 페이지의 옆부분에는 메뉴바가 있어야 한다.  
메뉴바를 만들어보자. 먼저 메뉴바를 감싸는 `menu-wrapper`를 하나 만들어주자.  
```html
    <div class="menu-wrapper" style="float:left; width: 15%; text-align:center">
    </div>
```  
그 다음 메뉴의 내용을 채워보자  
```html
    <div class="menu-wrapper" style="float:left; width: 15%; text-align:center">
        <ul class="list-group">
            <li class="list-group-item"><a href="#">상의</a></li>
            <li class="list-group-item"><a href="#">하의</a></li>
            <li class="list-group-item"><a href="#">신발</a></li>
            <li class="list-group-item"><a href="#">모자</a></li>
            <li class="list-group-item"><a href="#">양말</a></li>
        </ul>
    </div>
```  
이렇게 코드를 작성하고 확인해보자.  

이제 다음으로 본문이 들어갈 공간을 만들어보자.  
본문은 `contents`로 감싸서 구성해보자.  
```html
    <div class="contents" style="font-size:5em;">
        <div class="container" style="padding-left:1em;">
            <p>여기는 메인페이지 입니다. </p>
            <button class="btn btn-primary">버튼1</button>
            <button class="btn btn-secondary">버튼2</button>
            <button class="btn btn-danger">버튼3</button>
            <button class="btn btn-success">버튼4</button>
        </div>
    </div>
```  
다양한 버튼들을 통해 부트스트랩에서 제공하는 색들을 확인할 수 있다.  
`primary`는 파랑, `danger`는 빨강 등과 같이 여러가지 색을 이름을 통해 사용할 수 있다.  
지금까지 부트스트랩에서 제공하는 외부 CSS를 통해 웹페이지를 꾸며보는 방법을 배웠다.  
이 강의에서 나오는 것 말고도 훨씬 많은 기능들이 있으니 [여기](http://bootstrapk.com/)에서 찾아보길 바란다.  

이렇게 부트스트랩을 사용해서 조금 더 깔끔한 페이지를 만들 수 있게 되었으나,  
아직 전문적인 홈페이지들과는 거리가 멀다.  
이번에는 많은 사람들이 만들어놓은 템플릿을 이용해보자.  
[템플릿 이용하기](./classdata/Bootstrap.md)  
