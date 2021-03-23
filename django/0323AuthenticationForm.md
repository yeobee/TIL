# AuthenticationForm



1. POST동작할때는 request 필수
2. get_user()로 user 정보 획득



### session 생성

- login(request, 유저정보)



### 로그인 되었는지 확인

- user 인스턴스
- is_authenticated 
  - 로그인 했다면 True
  - 로그인 안했다면 False

- request.user
  - 로그인했다면 user 인스턴스
  - 로그인 안했다면 AnonymousUser 인스턴스



### 회원가입 modelForm

- UserCreationForm



### 회원수정 modelForm

- UserChangeForm
- xx 
- CustomUserChangeForm
  - model = get.user.model()

### 회원탈퇴

- request.user.delete()

### login

- AuthenticationForm(request, request.POST)
- auth_login(request, 유저정보)

### logout

- auth_logout(request)



### 비번변경

- PasswordChangeForm(유저정보)
- update_session_auth_hash(request,유저정보)
  - 이거안해주면 풀리기때문에 이거 쳐줘야 안풀리고 사용가능하다

