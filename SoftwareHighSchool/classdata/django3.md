# 게시글 업그레이드 하기
이전 시간까지 우리는 장고의 `model`을 사용해서 제목과 내용이 있는  
기본 게시판과 게시글을 만들었다.  

하지만 실제 게시판들에서는 게시글과 함께 이미지가 올라간다.  
이를 구현해보자.  

## 이미지 업로드
우리가 만들었던 `Post`모델에 사진이 들어갈 부분을 추가하자  

`mainphoto = models.ImageField(blank=True, null=True)`  
위 코드에서 `null=True`는 데이터베이스 상에서 `null`값을 허용한다는 뜻이고,  
`blank=True`는 입력을 받을 때에 입력이 없어도 된다는 뜻이다.  
둘다 똑같이 들리겠지만 코드가 작동하는 위치가 다르기 때문에 엄연히 다른 코드이다.  

##### `mysite/main/models.py`
```python
from django.db import models

class Post(models.Model):
    postname = models.CharField(max_length=50)
    # 게시글 Post에 이미지 추가
    mainphoto = models.ImageField(blank=True, null=True)
    contents = models.TextField()
    
    # postname이 Post object 대신 나오기
    def __str__(self):
        return self.postname
```

장고는 많은걸 할 수 있지만 모든것을 할 수 있지는 않다.  
모델을 수정한 후 사진을 처리할 수 있는 라이브러리를 설치해야 한다.  
`Pillow`를 사용하며 아래와 같이 설치할 수 있다.  

```console
$ pip install pillow==2.9.0

$ python3 manage.py makemigrations

$ python3 manage.py migrate

$ python manage.py runserver
```

#### 사진이 저장될 공간 설정
글에 사진이 들어갈 자리는 만들었는데, 아직 할게 더 남았다!  
글에 들어간 사진이 데이터베이스에 저장되어야 하는데 이 공간을 설정해주자.  
##### `web_study/settings.py`
`setting.py`파일 제일 아래에 다음과 같이 추가한다.
```python
MEDIA_ROOT = os.path.join(BASE_DIR, 'media')
MEDIA_URL = '/media/'
```

파일이 저장되는 공간을 추가했지만 아직 `django`가 파일 경로를 찾지 못한다.  
이미지의 경로를 설정해서 가져오자.  

##### `web_study/main/urls.py`

```python
from django.contrib import admin
from django.urls import path
# index는 대문, blog는 게시판
from main.views import index, blog, posting

# 이미지를 업로드하자
from django.conf.urls.static import static
from django.conf import settings

urlpatterns = [
    path('admin/', admin.site.urls),
    # 웹사이트의 첫화면은 index 페이지이다 + URL이름은 index이다
    path('', index, name='index'),
    # URL:80/blog에 접속하면 blog 페이지 + URL이름은 blog이다
    path('blog/', blog, name='blog'),
    # URL:80/blog/숫자로 접속하면 게시글-세부페이지(posting)
    path('blog/<int:pk>/', posting, name='posting'),
]

# 이미지 URL 설정
urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```

이제 업로드한 사진이 뜬다.  
  
##### `web_study/main/templates/main/posting.html`
이미지는 저장됐지만, 아직 html파일에 추가하지 않았으므로 나타나지 않는다.  
게시글마다 이미지를 나타내 보자.  
```html
<html>
    <head>
        <title>Posting!</title>
    </head>
    <body>
        <h1>게시글 개별 페이지입니다</h1>
        <p>{{post.postname}}</p>
        <p>{{post.contents}}</p>
        <!-- 이미지 보여주기 -->
        {% if post.mainphoto %}
            <img src = "{{ post.mainphoto.url }}" alt="" height="600">
            <br>
        {% endif %}
        <a href="/blog/">목록</a>
    </body>
</html>
```
이미지가 뜬 걸 확인할 수 있다!  

#####다음시간에는
[로그인 기능](django4.md)