# CSS
**CASCADING** STYLE SHEET의 앞글자를 따서 CSS라고 한다. 잠깐, Cascading?  
![cascading](../statics/classdata/css/cascading.png)  
폭포처럼 속성이 위에서 아래로 떨어지는데(상속).. 이렇게 들어서는 전혀 알 수가 없다! 그러면 이번에도 다시한번 무작정 따라해보자!

##### 따라하기 전에
한때 HTML에는 대단히 많은 태그들이 있었다. `<bgcolor>` 태그라던가, `<marquee>` 태그라던가, 표를 나타내기 위한 `<table>` 태그가 레이아웃을 위해 사용된다던가.. 결국 HTML 문서 안에 뼈대와 꾸밈이 모두 들어가 있던 것이었다.
이 구조를 HTMl과 CSS로 분리하여 직관적으로 웹 디자인과 웹 프로그래밍을 나누기 위해 CSS가 도입되었다고 생각하면 된다. 

### 무작정 따라해보기
```
a{
    color : black;            # 선택자: 무엇에 효과를 줄 것인가?
    text-decoration :none;    # 선언: 어떤 효과를 줄 것인가?(속성: 값)의 형태를 띄고 있다.
}
```
위의 예시처럼 선택자를 통해 *무엇에* 효과를 줄 것인지 정한 후에  
선언부에서 속성의 값을 지정해 *어떤* 효과를 줄 것인지 설정한다.  
여러가지 속성이 많이 있으니 전부 외우진 않더라도(사실 거의 불가능하기도 하고) 어떤 종류가 있는 것인지 한 번 알아보도록 하자.

#### 선택자
위의 예시에서 CSS의 선택자 부분에 태그가 올 수 있다는 걸 알게 되었을 것이다. 하지만 `<div>` 태그 같은 경우 정말 많이 쓰이게 되는데, 이 때 각각 다른 효과를 주고 싶을 때라거나,
같은 태그들을 그룹으로 나누어 효과를 주고 싶을 때 사용하는 것이 `선택자`이다.

선택자에는 `class`와 `id`가 있는데, 일단 예시로 확인해보자.

```
<div class="black" id="alpha">div박스 1</div>
<div class="red" id="omega">div박스 2</div>
```
위와 같이 태그별로 class와 id를 설정할 수 있다. class의 경우에는 한 문서에 여러 번 등장할 수 있지만, id는 하나의 고유한 이름을 한 문서에 오직 한 번만 사용할 수 있다.  
class와 id의 이름은 자유롭게 지을 수 있지만, 숫자로 시작하면 안 된다.

### 어떻게 사용하나요?
class는 `.(class명)`, id는 `#(id명)` 으로 지정할 수 있다. 위 코드블럭의 경우 css파일을 뜯어보면 다음처럼 되어 있을 것이다.
```
.black{
    color: black;
}

.red{
    color: red;
}

#alpha{
    font-size: 35px;
}

#omega{
    font-size: 20px;
}
```

### 그럼 어떻게 적용하나요?
HTML문서에 CSS를 적용하는 방법에는 크게 3가지의 방법이 있는데, 
1. Inline Style Sheet(태그 내부에 삽입)
```
<div style="color: blue">깔깔쓰</div>
```
2. Internal Style Sheet(html 문서 `<head>`내부에 `<style>`태그를 삽입)
```
...
<head>
...
<style>
    div{
        color: blue;
    }
</style>
...
```
3. External Style Sheet / Linking Style Sheet(외부의 CSS파일을 별도로 만들어 관리)
```
index.html
...
<head>
...
<link rel=:"stylesheet" href="style.css">
...


style.css
div{
    color: blue;
}
```

본인이 생각하기에 적당한 방법을 사용하면 되지만.. 보통은 3번이 재사용이 가능하고 유지보수가 용이한 연유로 많이 사용된다.

#### 실습과제
[자기소개카드 만들기](https://github.com/haedal-with-knu/instuctorTraining/blob/master/challenge/A.HTML_CSS_mycard.md)