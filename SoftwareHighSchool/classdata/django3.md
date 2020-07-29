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
$ pip install pillow

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

## 글쓰기페이지
이제 게시판을 완성했지만 중요한 기능이 남아있다.  
글쓰기 페이지를 만들어 관리자페이지에 들어가지 않고도 글을 써보자.  

글쓰기 페이지를 위한 새로운 파일 `new_post.html`을 만들어보자.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>글쓰기 페이지</title>
</head>
<body>
    <h1>글쓰기 페이지</h1>
    <form method="POST">
        {% csrf_token %}
        제목<br>
        <input type="text" name="postname"><br>
        내용<br>
        <textarea rows="10" cols="50" name="contents"></textarea><br>
        <input type="file" name="mainphoto"><br>
        <input type="submit" value="글쓰기">
    </form>
</body>
</html>
```  
갑자기 모르는게 많아졌을 것이다. form? POST? csrf?  

#### <form>
form부터 알아보자.  
`html`에서 `<form>`태그는 내부의 정보를 한번에 서버로 전송하는 역할을 한다.  
위 코드에서 보면 `<form>`태그 안에 3개의 `<input>`태그와 하나의 `<textarea>`태그가 있다.  
여기에 작성된 정보를 `type="submit"`버튼이 클릭되면 서버로 전송한다.  

이제 `<form>`태그의 속성 `method="POST"`에 대해서 알아보자.  
웹에서 정보를 서버에 전송할 때, 크게 두가지의 방식으로 통신한다.  
바로 `GET`방식과 `POST`방식이다.  
`GET`방식은 정보를 가져오는 방식이다. 즉, 원하는 데이터를 서버에 요청해서 받아온다고 생각하면 편하다.  
이 방식은 주소창에 가져올 정보가 모두 표시되기 때문에 중요한 정보는 `GET`방식을 사용하면 안된다.   
`POST`방식은 정보를 서버에 전송하여 서버 데이터베이스에 우리가 보낸 정보를 저장하는 방식이다.  
이 방법은 우리가 보낸 정보가 숨겨져 있다.  

#### csrf?
csrf란 사이트간 요청 위조 라는 뜻인데, 이름만 봐서는 잘 모르겠다!  
무엇인지 살펴보면 가해자와 피해자가있다고 하자.  
*가해자는 피해자가 자주 사용하는 사이트와 유사한 페이지를 만들고,  
피해자가 그에 속아 가해자가 만든 페이지에 접속하면 그 계정정보를 이용해  
가해자는 피해자의 권한을 얻어 사이트를 공격하는 방식이다.*  

너무 어렵다면 `django`에서는 이러한 공격에 대한 취약성을 보완하는 기능이 탑재되어있다고 생각하자...  

### 다시 django  
이제 글쓰기 페이지를 만들었으니 view를 연결해주자. 
`main/views.py`

```python
def new_post(request):
    if request.method == 'POST':
        if request.POST['mainphoto']:
            new_article=Post.objects.create(
                postname=request.POST['postname'],
                contents=request.POST['contents'],
                mainphoto=request.POST['mainphoto'],
            )
        else:
            new_article=Post.objects.create(
                postname=request.POST['postname'],
                contents=request.POST['contents'],
                mainphoto=request.POST['mainphoto'],
            )
        return redirect('/blog/')
    return render(request, 'main/new_post.html')
```  
`new_post`라는 view를 만들어 템플릿과 연결해주었다.  
`Post.objects.create`함수를 사용해서 새로운 `Post`모델을 하나 만들었다.  
이 함수는 사용자가 `POST`~~(둘다 post네;;)~~방식으로 전송한 정보(postname, contents, mainphoto)를  
바탕으로 새로운 글(post)모델을 만드는 함수이다.  
글이 생성되면 `redirect`함수를 사용해 게시판페이지로 돌아가고, 생성되지 않으면 글쓰기 페이지로 돌아간다.  

마지막으로 url을 연결하자.
`main/urls.py`
```python
    path('blog/new_post/', new_post),
```
위 경로로 추가해주면 된다!  

마지막으로 게시판 페이지에 글쓰기버튼만 추가해주자.  
`main/blog.html`
```html
<button><a href="new_post/">글쓰기</a></button>
```

## 글 삭제
마지막으로 글 삭제 기능만 구현하고 마치도록 하자!  
늘 하던대로 글 삭제 페이지부터 작성해보자.  
`templates/main/remove_post.html`
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>글 삭제</title>
</head>
<body>
    <form method="POST">
        {% csrf_token %}
        <h3>{{ Post.postname }} - 삭제하기</h3>
        <button>삭제</button>
    </form>
</body>
</html>
```  
삭제버튼을 누르면 글이 삭제되도록 views를 구현해보자.  
`main/views.py`
```python
def remove_post(request, pk):
    post = Post.objects.get(pk=pk)
    if request.method == 'POST':
        post.delete()
        return redirect('/blog/')
    return render(request, 'main/remove_post.html', {'Post': post})
```
마찬가지로 `POST`방식으로 요청이 들어왔다면 글을 삭제하고 목록으로 돌아가도록 구현했다.  

이제 `urls`를 연결해보자.  
`main/urls.py`
```python
    path('blog/<int:pk>/remove/', remove_post),
```  
글마다 가지고 있는 primary key를 주소로 받아 `remove_post`뷰를 연결했다.  

이제 글 상세페이지 `posting.html`에 삭제버튼을 만들어보자.  
```html
<a href="/blog/{{post.pk}}/remove">삭제</a>
```  
`<a>`태그를 이용해 삭제 버튼을 클릭하면 해당 글의 pk를 주소로 받는 삭제페이지로 연결된다.  

## 마무리
이번 시간에는 제목과 내용, 이미지를 갖는 게시글을 모델을 만들어보았고,  
이 모델들을 표시하는 게시판페이지와 게시글 상세페이지를 구현해보았다.  
또 이 글을 쓸 수 있는 글쓰기페이지를 구현했고, 삭제기능까지 추가했다.  
물론 django가 다양한 기능을 편리하게 사용할 수 있는 만큼  
많은 기능을 사용하려면 처음에 적응을 하는데 어려움이 따른다.  
하지만 게시판을 한번 만들어본 경험, django를 사용해본 경험이 쌓이면 분명이 훌륭한 웹 서비스를 만들 수 있을것이다.
이상으로 django 게시판 만들기 수업을 마치도록하겠다.

