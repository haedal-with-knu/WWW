## CSS_2. 실습하기
![html구조](../statics/classdata/html/html_structure.png)  
우리는 앞에서 위와같은 코드를 한번 따라해봤다.
지금부터 실습을 통해서 이 코드가 어떻게 구성되어있는지 알아보자!

### HTML
먼저 HTML파일을 하나 만들어서 살펴보자.  
```
<!DOCTYPE html>
<html lang="ko">
<head>
    <title>haedal</title>
</head>
<body>
    <header>header</header>
    <nav>nav</nav>
    <section>
    section
        <article id="article">article1</article>
        <article class="article">article2</article>
    </section>
<aside>aside</aside>
<footer>footer</footer>
</body>
</html>
```  

HTML부분만 보기 위해서 `<head>`안의 `<style>` 부분은 삭제했다.  
위 코드를 실행 시키면 아래와 같이 단지 글만 나오게 된다.  
![sementic_html](../statics/classdata/css/sementic_html.PNG)   

이제 이것을 `CSS`를 통해서 맨 위 그림처럼 꾸며보자  
이전의 `HTML`시간에서는 `<head>`태그안에 `<style>`을 넣는 방법을 통해 `CSS`를 적용했었는데,  
이번에는 `style.css`파일을 만들고 `html`문서에서 불러오는 방법으로 해볼 것이다.  
먼저 `style.css`파일을 HTML파일과 같은 디렉토리에 만들어 아래의 내용을 넣는다.  
```
body{
width:440px;
}
header, nav, section, article, aside, footer{
display:block; 
width:400px; 
margin:4px; 
padding:4px; 
background-color:#dbdbdb; 
text-align:center; 
border-radius: 5px;
}
section{
float:left; 
width:280px; 
height:200px;
}
article{
width:264px; 
height:77px; 
line-height: 77px; 
border-radius: 5px;
}
.article{
    background-color:skyblue;
}
#article{
    background-color:hotpink;
}
aside{
float:left; 
width:104px; 
height:200px; 
line-height: 200px;
}
footer{
overflow:hidden;
}
```  

우리는 아까 선택자와 속성 선언에 대해서 배웠다. 위에서부터 차근차근 읽어보자.  
먼저 선택자 `body`가 나온다. `html`내부의 `<body>`태그를 수정함을 알 수 있다.  
`body`안의 내용에는 `width:440px;`이 있다. `<body>`태그가 차지하는 공간의 너비를 `440px`로 지정하라는 뜻이다.  
이번엔 그 아래를 살펴보자 선택자가 `(,)`로 구분되어 여러개를 가리키고 있는것이 보이는데,  
여러개의 태그에 같은 속성을 지정하고 싶을때 사용 할 수 있다.  
여기에 사용된 속성들은 너무 많아서 모두 설명할 수는 없고 [여기](http://web.simmons.edu/~grabiner/comm244/weekthree/css-basic-properties.html)에서 기본 속성들을 확인하거나 추가적으로 검색해서 알아보자.  
마지막으로 살펴볼 것은 `article`부분이다. 위 코드에서 `article`, `.article`, `#article`이 있다.  
이전 시간에 배웠던 것처럼 선택자에는 `class`와 `id`를 사용해 세부 스타일을 지정할 수 있다.  
위 코드에서는 모두 `article`처럼 보이지만 `id=article`인 부분은 `hotpink`색으로 지정되고,  
`class=article`인 부분은 `skyblue`색으로 지정된다.  
위 코드를 모두 따라했다면 최종적으로는 아래와 같이 나타남을 확인할 수 있다!  
![sementic](../statics/classdata/css/sementic2.PNG)  


#### 지금까지 따라해본 내용을 바탕으로 아래 실습 과제를 해보자!
[자기소개카드 만들기](https://github.com/haedal-with-knu/instuctorTraining/blob/master/challenge/A.HTML_CSS_mycard.md)