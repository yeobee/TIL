## A many to one relationship

### Foreign Key (외래키)

- RDBMS에서 한 테이블의 필드 중 다른 테이블의 행을 식별할수 있는 키
- 참조하는 테이블에서 1개의 키에 해당하고 이는 참조되는 측의 테이블의 기본키를 가르킴
- 하나의 테이블이 여러개의 외래키를 포함할 수 있음
  - 그리고 이러한 외래키들은 각각 서로 다른 테이블을 참조할수있음
- 참조하는 테이블의 행 여러개가 참조되는 테이블의 동일한 행을 참조할수 있음
- 참조하는 테이블과 참조되는 테이블이 동일할 수도 있음(재귀적 외래키)



#### 특징

- 키를 사용하여 부모 테이블의 유일한 값을 참조
- 외래키의 값이 반드시 부모 테이블의 기본키 일 필요는 없지만 유일해야함
- 데이터 무결성
  - 컴퓨팅 분양에서 완전한 수명 주기를 거치며 **데이터의 정확성과 일관성**을 유지하고 보증하는 것
  - 데이터베이스나 RDBMS시스템의 중요한 기능이다



### A many to one relationship fields in django

#### ForeignKey()

- django에서 A many to one relationship(1:N )을 표현하기 위한 model field
- 2개의 필수 위치 인자가 필요
  1. 참조하는 모델 클래스
  2. on_delete 옵션

```
class Comment(models.Model):
	article = modles.ForeignKey(Article, one_delete=models.CASCADE)
```

#### on_delete

- ForeignKey가 참조하는 객체가 사라졌을때 foreignKey를 가진 객체를 어떻게 처리할지 정의
- 데이터 무결성을 위해서 매우 중요한 설정

-  **CASCADE: 부모 객체(참조 된 객체)가 삭제 됐을때 이를 참조하는 객체도 삭제**
- PROTECT : 참조가 되어있는경우 오류발생
- SET_NELL: 부모 객체 삭제 > 모든값 NULL로 치환
- SET_DEFAULT: 모든값이 DEFAULT값으로 치환
- SET(): 특정함수 호출
- DO_NOTHING: 아무것도 하지않음
  - 다만, 데이터 베이스 필드에 대한 SQL ON DELETE 제한 조건 설정해야함
- RESTRICT







- articles 게시글,댓글
- accounts 인증 ,유저



### 1:N model manager

- Comment(N)가 Article(1)을참조
  - comment.article

- Article(1)이 Comment(N)을 참조(역참조)
  - article.comment_set.all()
  - comment_set
  - django에서는 역참조시 모델이름_set 형식의 manager를 생성_



###  related_name

- django가 기본적으로 만들어주는 _set manager(역참조 manager)를 변경할 이름 설정_
- 1:N 관계에서는 거의 사용 하지않지만 M:N관계에서 반드시사용

```
class Comment(models.Model):
    article = models.ForeignKey(
    		Article, 
    		on_delete=models.CASCADE,
    		related_name='comments'
    		)
```

```
댓글작성
python manage.py shell_plus
comment= comment()
comment.content = '댓글1'
article =Article.objects.get(pk=1)
exit
```

### Relationship fields

- 모델 간 관계를 나타내는 필드
- Many to one(1:N)
  - ForeignKey()

- Many to Many(M:N)
  - ManyToManyField()
- one to one(1:1)
  - OneToOneField()



### THE save() method

- save(commit=False)
  - create, but don't save the new instance
  - 아직 데이터베이스에 저장되지않은 인스턴스를 반환
  - 저장하기 전에 객체에 대한 사용자 지정 처리를 수행할때 유용하게 사용



## AUTH_USER_MODEL

- User를 나타내는데 사용하는 모델
- 기본값은 auth.User
- 주의사항
  - 프로젝트가 진행되는 동안 변경할수없음(변경하기위해 많은 노력이필요)
  - 프로젝트 시작시 설정하기 위한 것이며, 참조하는 모델은 첫번째 마이그레이션에서 사용할수있어야함



### AbstractBaseUser

- 기보적으로 password와 last_login 만 제공
- 자유도가 높지만 필요한 다른 필드는 모두 직접 작성해야함

### AbstractUser

- 관리자 권한과 함께 완전한 기능을 갖춘 사용자 모델을 구현하는 기본클래스



```
models.Modles
>
class AbstractBaseUser
>
class AbstractUser
>
class User
```

```
User Custimise

models.py
유저모델 정의
from django.contrib.auth.models import AbstractUser
class User(AbstractUser):
    pass
   
seetings.py등록
AUTH_USER_MODEL = 'accounts.User'

makemigrations
migrate

User 커스텀한다
관련된 ModelForm의 model을 수정


수정할때
models.py 에선
setting AUTH_USER_MODEL

그외에선
get_user_model()
```

