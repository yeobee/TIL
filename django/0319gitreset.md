## 에러발생

4xx. 사용자 잘못

5xx. 개발자 잘못



# GIT

```
commit 메세지 수정

git commit --amend
ese 
누르면 취소
i
눌러서 끼워넣기상태할수있다
:wq 
현재상태에서 저장하고 commit 끝시킴

git log 
```

```
파일을 빠트렷을때
git add c.txt
git status
git commit=m 'c,d'
c만 추가되어있고 d는 안되어있다
이때 c와d 둘다 되어있어야하는데 c만 했다
다시친뒤
git add d.txt
git status
git commit --amend

git log -oneline
```

```
git log -oneline
working direcroty             staging area          repository
1. hard 완전히 그때로 되돌아간다. 완전히 다 지워버린다
하드는 add 했던 것 까지 없어지고
git reset --hard 내가가고싶은부분의 코드 치기(3)
git log -oneline
그러면 여기까지 내가 3번으로 온 부분까지만 나온다
그뒤에 그럼내가 뒤에 수정할수있다

2. soft 과거로 돌아가지만 기억을 지우지않고 남겨둔다(히스토리가 남아있다)
soft는 add까지는 남아있다
git reset --soft 내가가고싶은부분의 코드치기(3)
git log -oneline
commit의 시점은 돌아감 현재시점에서 add까진 되어있다

3 mixed 
git reset --mixed 내가가고싶은부분의 코드치기(3)
git log -oneline
git status하면 add까지 남아있는게아니라 add전까지 남아있어서 다시 add 해줘야한다

```

```
프로젝트생성
앱생성> 앱등록
urls.py 생성
models.py
forms.py > 모델등록,fields등록
views.py 생성 내가원하는함수 만들어줌 CRUD
-templates 랜더링
settings.py 
	-base_dir
	-templates
	-static
단단한 페이지만들기 - require_POST,get_object_or_404

```

