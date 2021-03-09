## Django



- python 언어 사용



### django-admin startproject 프로젝트이름

### python manage.py runserver

### python manage.py startapp 앱이름

- startapp 하고 난뒤에 settings에 앱이름 추가해줘야한다 istalled_apps에



- `__init__.py` 빈파일, 터치할거 없다
- asgi.py 신생 파일, 잘쓸일없다
- settings.py 많이 사용할것, 모든설정을 포함하는 파일
- urls.py 많이 사용할것, 1차로 요쳥경리 확인하는 곳
- wsgi.py 배포할때 도움줌



1. urls.py 1차로 요쳥경리 확인하는 곳
2. views.py
3. models.py
4. template.py 
5. 1-3-4 순으로 수정을한다

- 장고는 패턴 마지막주소에 /가 무조건 들어가야한다!
- 여러개 추가할때 마지막에 자기가 마지막이여도 ,가 들어가야한다



## 템플릿이 확장하는 방법



1. 확장하는 템플릿이 위치할 폴더를 생성한다(택1)

   1. 설정폴더

   2. 프로젝트 폴더

      - DIRS의 경로를 잘설정 해줘야한다.(위치 찾기)

        1.1 settings.py에 폴더 경로를 설정한다

2. 공통적으로 사용되는 템플릿을 정의한다. (base.html)
   
1. `block` 을 설정해서 상이한 내용이 오는 공간을 확보한다
   
3. 사용한다

   - 템플릿 상단에`{% extends 'base.html'%}`을 추가한다
     - 무조건 최상단에 위치한다

   - `block` 사이에 내용을 집어 넣는다.



## URL 분리

1. 설정 폴더의 `url.py`에서 분리 준비를 한다
   1. 상단 주석을 참고하면 좋다

2. application 폴더에 `urls.py` 파일을 생성
   1. 기본 구조를 잡아줘야함.
   2. path 함수를 사용하기 위한 import
   3. urlpatterns라는 리스트

3. 이제는 application 폴더의 `urls.py` 에 경로를 등록해서 사용



1. 프로젝트 생성하기

   `$django-admin startproject 프로젝트이름`

2. 앱 생성하기

   ```
   #manage.py가 있는 경로확인
   $ python manage.py startapp 앱이릅
   ```

   ```
   프로젝트이름/
   	프로젝트폴더/
   	앱폴더/
   	manage.py
   ```

3. 기본설정(settings.py)

   ```
   언어 설정 ko-kr
   시간 설정 Asia/Seoul
   ```

4. [선택] URL분리

5. ```
   urls.py
   from django.urls import path, include
   path('articles/', include('article.urls'))
   
   articles 만들어서 그안에 urls 만들어서 사용
   ```

6. [선택] 템플릿 상속

   ```
   
   ```

7. urls.py

8. views.py

9. template

```
순서
$django-admin startproject 프로젝트이름   
## 절대경로 상대경로 
. 현재폴더에다가 설치한다
.. 이전폴더

$ python manage.py startapp 앱이릅

Settings.py에서
INSTALLED-APPS에다가
'articles' 추가해주고

언어 설정 ko-kr
시간 설정 Asia/Seoul

DIRS에 경로 설정해주지
'DIRS': [BASE_DIR/ '프로젝트이름'/'templates'],

templates 폴더생성
base.html 만들고
!로 기본만들어주기 
{% block content %}
    {% endblock content %}
    
urls.py 설정
from django.urls import path, include
path('articles/', include('article.urls')),

include('article.urls') 이게 없다
articles폴더 만들어서 그안에 urls새로추가해서 만들어서 사용
from  .  import views
path('index/', views.index),

views.py에 index함수 만들어주기
def index(request):
    return render(request, 'index.html')
#render(request, template_name, context=None)
1 요청정보
2 사용자에게 그려줄 템프릿이름
3.템플릿에 함께 담을 데이터(optional)
 
articles 폴더안에 templates 폴더 생성
그안에 index.html 생성
{% extends 'base.html' %}  #첫줄에 이거 적어줘야한다!

{% block content %}
<h1>인덱스 페이지 입니다.</h1>
{% endblock content %}

<form action = '서버주소'>
	<label for = 'message'>메세지: </label>
	<input type = 'text' id ='message' name='mijeongs'
	<input type = 'submit'>
</form>
python manage.py runserver
```

​	