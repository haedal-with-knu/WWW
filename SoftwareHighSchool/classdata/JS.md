# JavaScript 기초

### 시작하기 전에.. 다시한번 무작정 따라하기
html문서의 body 부분을 다음과 같이 작성해 보자.
```
<body>
    <script>
        var age=prompt("당신의 나이는?", "0");
        if(age>=20){
            document.write("성인");
        }
        else{
            document.write("미성년자");
        }
    </script>
</body>
```
## 언어를 배울 때 꼭 짚고 지나가는 것들
마치 관혼상제처럼.. C든 JAVA든 파이썬이든 처음에 이것들은 배운다!
+ 주석 `//, /* */`
+ 변수 `var s`
    - 문자(string)
    - 숫자(number)
    - 논리(boolean) / 예제
    - 빈데이터(undefined) / null과 undefined
+ 연산자
    - 산술 연산자 `+, -, *, /, %`
    - 문자 결합 연산자 `+`
    - 대입 연산자 `=, +=, *=, /=, %=`
    - 증감 연산자 `++, --`
    - 비교 연산자 `>, <, >=, <=, ==, !=, ===, !==`
    - 논리 연산자 `||or, &&and, !not`
    - 삼항 연산자 `a?b:c`
    - 연산자 우선 순위 `괄호-단항연산자-산술연산자-비교연산자-논리연산자-대입연산자`
+ 제어문
+ 반복문
+ 함수
+ 객체의 개념

간단하게 쭉 훑고 넘어갈 수 있도록 하자.

##### example - 논리형 연산자
```
<script>
    var a = true;
    var b = false;
    var c = 5 > 2;
    var d = Boolean(undefined);

    document.write(a, "<br>");
    document.write(b, "<br>");
    document.write(c, "<br>");
    document.write(d, "<br>");
```
##### example - 문자 결합 연산자
```
<script>
    a = "100"+200
    document.write(a)
```

##### example - script + html
```
<script>
    var result = "<table border='0.5'>";
    result += "<tr>";
    result += "<td>1</td><td>2</td><td>3</td></tr>";
    result += </table>;
    document.write(result);
```
##### example - 변수 입력받기
```
prompt("당신의 나이는?", "10");
```

##### PRACTICE - 키와 몸무게 입력받아 정상체중인지 아닌지 판별하기
`prompt`를 이용하여 키, 몸무게를 입력받아 정상체중인지 아닌지 판별해 보자. 단, `평균체중=(현재체중-100)*0.9`이고, `0.95*평균체중<=정상체중<=1.05*평균체중` 이라고 하자.

##### example - 제어문
```
    var num = 100;
    if(num>100){
    document.write("num은 100보다 큽니다."}
```

###### 여기서 잠깐! 다음 식은 False로 반환된다
`0, null, "", undefined"`

##### example - switch문
```
var a=1;
var b;
switch(a){
    case 1: b=1;
    break;
    case 2: b=2;
    break;
    default: b=5;
}
```

##### example - for문
```
for(var i=0; i<10; i++){
    document.write(i+"br");
```

##### PRACTICE - 반복문
4행 4열 표를 만들고, 숫자가 각각 1부터 16까지 출력되도록 script를 작성하시오.

Hint: for문 2개와 Number()함수