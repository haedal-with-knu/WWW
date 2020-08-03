# 6일차

## JavaScript를 해보자!
JS 예시 코드도 마찬가지로 `pycharm`을 이용하여 코드를 무작정 따라해보도록 하자.

### 무작정 따라하기
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>JS EXAMPLE</title>
</head>
<body>
    <script>
        var age=prompt("당신의 나이는?","0");
        if(age>=20){
            document.write("성인입니다.");
        }
        else{
            document.write("미성년자입니다.");
        }

    </script>
</body>
</html>
```
CSS를 분리해서 `style.css` 파일로 저장하여 html에 연결해서 사용했던 것 처럼, `javascript`구문도 따로 분리할 수 있다.
새로운 `javascript` 구문을 작성 후 그 부분만 따로 적어보자.
```
document.write("환영합니다.")

js/example.js
``` 
```
<!doctype html>
<html lang="ko">
<head>
    <meta charset='utf-8'>
    <title>자바스크립트 외부파일 연동</title>
    <script src="js/example.js"></script>
</head>
<body>
</body>
</html>
```