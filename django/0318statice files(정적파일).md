### statice files(정적파일)



- @ :데코레이터 
  - 함수실행전에 실행되는거

```
from django.views.decorators.http import require_http_methods, require_POST

@require_http_methods(['GET', 'POST'])
```



- 정적파일

  - 사용자의 요청에 따라 내용이 바뀐는 것이 아니라 요청한 것을 그대로 응답하면 되는 파일

  - 웹사이트의 구성요소중에서 image,css,js 파일과 같이 해당 내용이 고정되어 응답할때 별도의 처리없이 파일내용을 그대로 보여주면 되는 파일

  - 기본 stactic 경로

    - app_name/static/

    

```
{%load static%} << statice 사용하려면 이친구를 무조건 필요하다
<img scr = "{%static 'articles/sample/png'(경로) %}" alt="sample">
```

- static_url

  - static_root에 있는 정적 파일을 참조할때 사용할 url

  ​	       - 실제 파일이나 디렉토리가 아니며,url로만 존재

  - 비어 있지 않은 값으로 설정한다면 반드시 slash(/)로 끝내야한다

- staticfiles_dirs
  - app내의 static 디렉토리 경로를 사용하는것(기본경로) 외에 추가적인 정적 파일 경로 정의

- STATIC_ROOT

  - Django 프로젝트에서 사용하는 모든 정적파일을 한곳에 모아넣는 경로
  - collectstatic이 배포를 위해 정적 파일을 수집하는 절대 경로
  - collectstatic
    - 프로젝트 배포 시 흩어져 있는 정적 파일들을 모아 특정 디렉토리로 옮기는 작업

  - 개발 단계에서는 STATIC_ROOT 경로를 작성하지 않아도 문제없이 동작
    - 즉, 실제서비스 배포 환경에서 필요한 경로

```
1 base.html 수정
	blcok 설정해줌
2 index.html 수정
	load stactic 해주기
	{% load static %}
	{% block css %}
    <link rel="stylesheet" href=" {% static 'articles/index.css' %} ">
	{% endblock css %}
3 css파일 생성

4 서버 재실행
```

```
FileField, ImageField 사용하기

1.settings.py에 MEDIA_ROOT, MEDIA_URL설정
2.upload_to 속성을 정의하여 업로드 된 파일에 MEDIA_ROOT의 사용할 하위 경로지정

3.업로드 된 파일의 상대 URL경로를 django가 제공하는 url attribute를 통해 사용가능
```

- MEDIA_ROOT

  - 사용자가 업로드 한 파일을 보관할 디렉토리의 절대 경로
  - 실제 해당 파일의 업로드가 끝나면 파일이 저장되는 경로
  - django는 성능을 위해 업로드 파일은 데이터베이스에 저장하지않음
    - 데이터베이스에 저장되는 것을 파일의 경로

  - MEDIA_ROOT와 STATIC_ROOT는 서로 다른 경로를 가져야함

- MEDIA_URL
  - 업로드 된 파일의 주소를 만들어주는 역활
  - MEDIA_ROOT에서 제공되는 미디어 파일을 처리하는 URL
    - 웹서버 사용자가 사용하는 PUBLIC URL



```
enctpye="multipart/form-data" 파일올릴때 필수
<form action="" method="POST" enctpye="multipart/form-data">
```



```
/media/

앞에있는 /는 root 경로 =main root (http://127.0~)
뒤에있는 / 그밑 하위

:
url 태그에서 (app이름:name) 같이 적을때만사용하는것
view 에서 사용 
url 관련된 이동할때

.
oop에서
인스턴스 변수,클래스변수, 

request.POST
인스턴스.변수or메서드(괄호필요) 차이는 괄호의 유뮤

<> 꺽새
pk = int(input())


MEDIA_ROOT = BASE_DIR / 'media'  #파일이 저장되는곳
MEDIA_URL = '/media/' url 주소 만들때 사용 
```

