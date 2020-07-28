```
from flask import Flask, render_template
# app이란 이름으로 flask 프로젝트 초기화
app = Flask(__name__)



@app.route('/')
def index():
    return ('메인 페이지입니다. 주소창 뒤에 숫자를 입력하세요')

@app.route('/<int:num>')

def gugudan(num, output=''):
    for i in range(1,10):
        temp = str(num) + ' * ' + str(i) + ' = ' + str(i*num)
        output = output + temp + ' '
    return(output)


if __name__=='__main__':
    app.run(debug=1)
```
```
body {
background-image: url('https://media.discordapp.net/attachments/682866632237907983/686866185840754689/1.png'),url('https://cdn.discordapp.com/attachments/682866632237907983/686865228134088746/2.png');
-webkit-animation: snow 10s linear infinite;
-moz-animation: snow 10s linear infinite;
-ms-animation: snow 10s linear infinite;
animation: snow 10s linear infinite;
}
```