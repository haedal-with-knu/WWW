# 장고랑 친해지자
> 장고는 파이썬을 기반으로 한 웹 프레임워크이다.  

## 개발 환경 설정  
개발 과정에서 여러 라이브러리들이 충돌할 수 있기 때문에 우리는 가상환경에 라이브러리들을 설치하도록 하겠다.  

```shell script
$ source venv/scripts/activate
```  

가상환경을 열었으면, 우리가 배울 `django` 라이브러리를 다운 받자.  

```shell script
$ pip install django
``` 

조금만 기다리면 `3.0.8`버젼의 `django`가 다운로드 될 것이다.  
그러면 준비는 모두 끝났지만 장고를 사용하기 위해서는 프로젝트를 시작해야 한다.  

### 장고 프로젝트 시작하기  
`web_study`라는 프로젝트를 하나 만들어 보자.    
```shell script
$ django-admin startproject web_study
```
장고(`django`)가 사용할 데이터베이스(`DB`)를 생성한다.(`migrate`)  
데이터 베이스를 생성하기 위해서는 방금 만든 장고 프로젝트 폴더로 들어가야한다.  
```console
$ cd web_study
$ python manage.py migrate
```  

### 장고 프로젝트 실행하기
이제 데이터 베이스도 만들었으니 프로젝트를 실행해서 서버를 한번 켜보자.  
```console
$ python manage.py runserver 
```  
로켓이 보인다면 서버가 켜진 것이다!  
아직 아무것도 없으니까 너무 좋아하지는 말자. 갈 길이 멀다.  

### 첫 페이지 만들기
프로젝트를 만들었지만 우리가 페이지를 추가하려면 앱(`App`)이라는 것을 만들어야 한다.  
장고의 모든 프로젝트는 여러개의 `HTML`과 `.py`파일로 이루어진 앱들이 여러개 모여서 만들어진다.  
`main`이라는 이름의 첫 번째 앱을 만들어보자.  
```shell script
$ python manage.py startapp main
```  
앱을 만들었으면 프로젝트에서 사용할 수 있도록 등록을 해야한다.  
`web_study/settings.py`의 약 40번째 줄인 `INSTALLED_APPS`에 아래와 같이 추가해준다.  
```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'main',
]
```  
여기까지 했다면 기초공사가 완료된 것이다!  
이제 `web_study/main/templates/main`폴더를 하나 만들어,  
그 안에 `index.html`파일을 만들어주자.  

이제 우리가 만들 `html`파일을 인코딩해서 웹에 띄우는 작업을 해야한다.  
`main/views.py`파일을 열어 다음 코드를 추가해준다.  

```python
from django.shortcuts import render

# Create your views here.
def index(request):
    return render(request,'main/index.html')
```  
이제 마지막으로 우리의 `view`와 `url`을 연결만 해주면 된다.  
`main/urls.py`파일을 하나 새로 만들어 아래의 코드를 추가해준다.  
```python
from django.urls import path

from . import views


urlpatterns = [
    path('', views.index, name='index'),
]
```  
이 앱의 `url`과 프로젝트의 `url`을 연결해주자
`main/urls.py`에 들어가서 아래와 같이 바꿔준다.  

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('main.urls')),
]
```  
그러면 끝이 났다. 터미널에 아까전에 서버를 호스팅하는데 사용했던  
명령어를 입력해 우리가 만든 페이지를 호스팅해보자.  

```shell script
$ python manage.py runserver
```

![shell](./statics/classdata/boot/shell.PNG)  
위에 적힌 주소를 클릭하면 우리가 만든 페이지가 나타날 것이다!  

## 다음 강의는
### [게시판 만들기](./classdata/Django2.md)