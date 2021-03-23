![image](S:\ssafy_ed\D02\image.png)

* 장고 프로젝트 생성

  * django-admin startproject 프로젝트명
  * cd 로 프로젝트 폴더 내로 이동. (bash 사용시 경로 체크! manage.py가 있어야함.)

* 장고 앱 생성

  * python manage.py startapp 어플리캐션이름s (이름은 복수형)

  * 바로 settings.py 에 INSTALLED_APPS 에 등록!!! 
  * language code, time zone 수정.

* MTV 장고 패턴을 가지고 있음.

* 수정 파일 3대장 

  * urls.py
  * views.py
  * template 파일.



* 템플릿에서 변수 사용하기.
  * render()  세번째 인자로 변수 값을 넘길 수 있음. (dictionary type으로 넘긴다.)
    * context 라는 변수에 dictionary 를 만들어서 넘기는것이 일반적.
  * template 에서 변수를 사용할 때 `{{ 변수명(딕셔너리의 키) }}`



* Variable Routing

  * 주소의 일부를 변수에 담아서 사용하는 방법
  * `hello/ed` , `hello/우영` ... 

  * urls.py 에서 `path('hello/<str:name>/', views.hello)`
  * views.py 에서 변수를 매개변수로 만들어서 받아줘야 한다.
    * `def hello(request, name):`
    * 매개변수의 이름은 urls 에서 정의한 변수명과 같아야 한다.

  * str 은 기본값이므로 생략 `<name>`
  * 숫자는 int 로 표현 `<int:age>`



* Html Form tag
  * 사용자로 부터 입력받은 데이터를 전송하기 위한 태그
  * 설정해야할 속성은 2가지
    * action : 입력 데이터가 전송되는(도착하는, 전달되는) 경로
    * method : http method 를 입력. (GET, POST), 기본값은 (GET)
      * GET : 정보를 조회할 때, 읽어 올 때 
      * POST: 정보의 데이터가 변경점이 있을때. (수정, 삭제, 생성)
  * 전달을 할 때는 반드시 `submit` 동작이 필요.
    * `<input type=submit>`
    * `<button>`



* DTL

  * 장고 템플릿에서 사용하는 내장 시스템 언어.
  * 태그와 필터로 구성.
  * `{% 태그 %}`  / `{% value|필터 %}`

  * 값을 표현 할 때 `{{ value }}`

  * 주석 : 한줄`{# #}`, 여러줄 `{% comment %} 사이에 모든 것을 주석 처리 {% endcomment %}`

  * Tags

    * `if / elif / else`
      * in, not, is 사용 가능
    * `for / for empty`
      * forloop : counter, counter0, first, last
    * `lorem [갯수] [단위(w, p, b)] [random]`

    * `now "시간 포멧 형식"`
      * `now "시간포맷형식" as 별명`  를 사용해서 별명을 붙일 수 있다.

  * Filters - `:` 콜론뒤에 공백 없이 적어야 함.

    * `add:숫자`
    * `date:"시간 포멧 형식"`
    * 문자 관련
      * `capfirst` / `lower` / `title` / `upper`
      * `truncatewords:갯수`
      * `truncatechars:갯수` : `...` 도 갯수로 포함된다.
    * `length` 
    * `random`

 

----

### 템플릿 확장(상속)

1. templates 폴더를 생성
   * 설정폴더 밑에 생성을 하거나
   * 프로젝트 폴더 밑에 생성을 하거나

2. base.html 작성
   * `{% block 블럭명 %} {% endblock %}` 꼭 추가해준다.
3. `settings.py` 에 등록
   * TEMPLATES 에서 DIRS 에 `base.html` 의 경로를 등록해준다.

4. `{% extends 'base.html' %}` 을 각 템플릿 상단에 적어서 사용해 준다.
   * 템플릿 내용은 `{% block 블럭명 %} {% endblock %}` 사이에 위치해 있어야 한다.



-----

## URL 분리

1. 설정 폴더 `urls.py` 에서 분리를 시작한다.
   * hint : 상단 주석에 방법이 친절히 적혀져 있다!!!
   * url 분리는 application 단위로 분리해주면 됨.
2. include 안에 설정된 위치에 `urls.py` 파일이 없어서 생성을 해주면 됨.
3. `urls.py` 에 내용을 채워 넣는다.
   * 필요한 함수는 `path`
   * 필요한 리스트는 `urlpatterns`

4. 사용을 하면 된다. 
   * path(경로, views.함수명)



----



## URL namespace

1. `path` 함수 세번째 위치에 `name='별명'` 추가한다.

2. 경로가 필요한 부분 (링크, form action 부분) 에 `url` 템플릿 태그를 이용해서 사용하면 끝

   * `{% url '별명' %}`

   * 단점 : 어플리케이션이 많아지는 경우 동일한 별명이 있을 수 있다.
     * 이러한 경우 어떤 url 인지 구분이 명확하지 않게 됨.
   * 해결 방법 : `app_name` 지정.

3. `app_name` 지정

   * `app_name = 어플리케이션 이름` 
     * app_name 을 설정한 순간 부터는 `{% url '별명' %}` 형식은 사용 불가능.
   * 사용 방법
     * `{% url '설정한app_name:별명'%}` 사용해서 구분을 해준다.



## Template namespace



1. 문제의 원인
   * 장고는 INSTALLED_APPS 에 등록된 순서대로 template 파일 목록을 찾기 때문에 어떤 어플리케이션의 template 파일인지 구분을 할 수 가 없게 된다.
   * 다른 경로로 요청을 했지만 같은 이름의 템플릿 파일의 소속 어플리케이션을 구분할 수 없기 때문에 같은 화면이 보여지는 문제점이 발생한다.
2. 해결 방법
   * `templates` 폴더 내부에 어플리케이션 이름으로 폴더를 하나 더 작성 한다!





-----

### 연습 첫 번째

* Fake Google
  * 요청 경로 : `/pages/fake-google/` 
  * 보여지는 페이지 : 검색어를 입력할 수 있는 페이지가 응답으로 보여진다.
  * 동작
    * 검색어를 입력하고 버튼을 누르면 google 결과가 페이지에 보여지게 하자.
    * `https://www.google.com/search?q=ssafy` 주소로 요청
    * form action : 데이터를 전달 받는 곳  : https://www.google.com/search
    * form method : 데이터를 보내는 방식 : GET  => 쿼리 스트링 형식으로 데이터가 날아간다.
      * url`?키=벨류&키=벨류`

















