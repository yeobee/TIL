#### 스택의 특성

- 물건을 쌓아 올리듯 자료를 쌓아올린 형태의 자료구조
- 스택에 저장된 자료는 선형구조
  - 선형구조 : 자료 간의 관계가 1:1관계
  - 비선형 구조: 자료 간의 관계가 1:N의 관계(ex,트리)

- 스택에 자료를 삽입하거나 스택에서 자료를 꺼낼수있다
- 마지막에 삽입한 자료를 가장 먼저 꺼낸다(후입선출)(LIFO)
- 스택의 자료구조 : 자료를 선형으로 저장할 저장소
  - c언어에서는 배열을 사용할수있다. 리스트
  - 저장소 자체를 스택이라 부르기도한다
  - 스택에서 마지막 삽입된 원소의 위치를 top이라 부른다.



- 연산
  - 삽입 : 저장소에 자료를 저장한다 = push
  - 삭제 : 저장소에서 자료를 꺼낸다(역순으로) = pop
  - isEmpty : 스택이 공백인지 아닌지 확인
  - peek : 스택의 top에 있는 item을 반환하는 연산

- 순서 
  - 넣을때 top을 증가하고 자료를 넣고, 자료를 빼고 top을 감소시킨다 

```
def pop():
	if len(s) ==0:  #공백검사
		#underflow
		return
	else:
		return s.pop(-1);
```

#### 피보나치 수열

```
def fibo(n):
    arr[n] +=1
    if n <2:
        return n
    else:
        return fibo(n-1)+fibo(n-2)
arr = [0]*35
print(fibo(20))
print(arr)
```



#### 메모이제이션

- 컴퓨터 프로그램을 실행할때 이전에 계산한 값을 메모리에 저장해서 매번 다시 계산되지 않도록 하여 전체적인 실행속도를 빠르게 하는 기술이다
- 동적계획법(DP)의 핵심이 되는 기술이다

```
def fibo(n):
    global memo
    if n >=2 and len(memo) <=n :
        memo.append(fibo(n-1)+fibo(n-2))
    return memo[n]
    memo = [0,1] 
    print(fibo(20))
```

### DFS 알고리즘

- 1)시작 정점 V를 결정하여 방문한다
- 2)정점 V에 인접한 정점중에서
  - 방문하지 않은 정점 W가 있으면,  정점v를 스택에 push하고 정점 w를 방문한다. 그리고 w를 v로하여 다시 2)를 반복한다
  - 방문하지 않는 정점이 없으면, 탐색의 방향을 바꾸기 위해서 스택을 pop하여 받은 가장 마지막 방문 정점을v로하여 다시 2)를반복한다.

- 3)스택이 공백이 될때까지 2)를 반복한다

```
visited[], stack[] 초기화
DFS(v)
	v 방문;
	visited[v] << true
	do {
		if(v의 인접 정점 중 방문 안한 w 찾기)
			push(v);
		while(w){
			w방문;
			visited[w] <<<< true;
			push(w);
			v << w;
			v의 인접 정점 중 방문 안한 w찾기
		}
		v << pop(stack);
	}while(v)
end DFS()
```



- 정점의 개수 
  - 정점의 번호 

- 간선의 수
  - 간선의 수만큼 연결정보가 들어옴