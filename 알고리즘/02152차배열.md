## 2차원 배열의 접근

### 행 우선 순회

```python
for i in range(len(Array)):
	for j in range(len(Array[i])):
		Array[i][j] # 필요한 연산 수행
```



### 열 우선 순회

```python
for j in range(len(Array[0])):
	for i in range(len(Array)):
		Array[i][j] # 필요한 연산 수행
```



### 지그재그 순회

```python
for i in range(len(Array)):
	for j in range(len(Array[0])):
		Array[i][j + (m(열의 길이) - 1 - 2 * j) * (i % 2)]
```



## 델타를 이용한 2차 배열 탐색

- 2차 배열의 한 좌표에서 4방향의 인접 배열 요소를 탐색하는 방법

```python
ary[0...n-1][0...n-1]
dr = [-1, 1, 0, 0]
dc = [0, 0, -1, 1]
# drc = [[-1, 0], [1, 0], [0, -1], [0, 1]]

r = 0
c = 1
N = 3

for i in range(4):
    nr = r + dr[i]
    nc = c + dc[i]

    # if nr < 0 or nr >= N or nc < 0 or nc >= N: continue
    if 0 <= nr < N and 0 <= nc < N:
        print(arr[nr][nc])
```



### 전치행렬

```python
for i in range(3):
    for j in range(3):
        if i < j:
            arr[i][j], arr[j][i] = arr[j][i], arr[i][j]
```



### 비트연산자

`&` : 비트 단위로 AND 연산을 한다.

`|` : 비트 단위로 OR 연산을 한다.

`<<` : 피연산자의 비트 열을 왼쪽으로 이동시킨다.

`>>` : 피연산자의 비트 열을 오른쪽으로 이동시킨다.

#### `<<` 연산자

- 1 << n = 2^n 즉, 원소가 n 개일 경우의 모든 부분집합의 수를 의미한다.

#### `&` 연산자

- i & (1<<j) : i의 j번째 비트가 1인지 아닌지를 리턴한다.



## 보다 간결하게 부분집합을 생성하는 방법

```python
arr = [3, 6, 7, 1, 5, 4]
n = len(arr) # 원소의 개수
for i in range(1<<n): # 1<<n : 부분 집합의 개수
    for j in range(n): # 원소의 수만큼 비트를 비교함
        if i & (1<<j): # i의 j번째 비트가 1이면 j번째 원소 출력
            print(arr[j], end=", ")
        print()
    print()
    
ex)
재료 = ["계란", "치즈", "떡"]
N = 3
for i in range(1<<N):
    for j in range(N):
        if i & (1<<j):
            ans += 재료[j] + " "
    print(ans, "라면입니다.")
```



## 순차 검색

```python
arr = [4, 9, 11, 23, 19, 7]

key = 2

for i in range(len(arr)):
    if key == arr[i]:
        print(1, '에 위치하고 있음')
        break
else:
    print('못찾음')

    
arr = [4, 7, 9, 11, 19, 23]
for i in range(len(arr)):
    if key == arr[i]:
        print(i, '에 위치하고 있음')
        break
    elif key < arr[i]:
        pirnt(i, '번째까지만 탐색해봄')
        break
else:
    print('못찾음')
```



## 이진 검색(Binary Search)

- 반드시 정렬이 되어있어야 사용할 수 있다.

```python
def bianrySearch(a, key):
    start <- 0 end <- length(a)-1
    while start <= end:
        middle = (start + end) // 2
        if a[middle] == key # 검색 성공
        	return true
        elif a[middle] > key:
            end = middle - 1
        else: start = middle + 1
            return false # 검색 실패
```



- 재귀함수 이용

```python
def binarySearch2(a, low, high, key):
    if low > high : # 검색 실패
        return False
   else:
    middle = (low + high) // 2
    if key == a[middle] : # 검색 성공
        return True
    elif key < a[middle]:
        return binarySearch2(a, low, middle-1, key)
    elif a[middle] < key:
        return binarySearch2(a, middle+1, high, key)
```



## 셀렉션 알고리즘

```python
def select(list, k):
	for i in range(0, k):
        minIndex = i
        for j in range(i + 1, len(list)):
            if list[minIndex] > list[j]:
                minIndex = j
        list[i], list[minIndex] = list[minIndex], list[i]
    return list[k - 1]
```



## 선택 정렬

- 주어진 리스트 중에서 최소값을 찾는다.
- 그 값을 리스트의 맨 앞에 위치한 값과 교환한다.
- 맨 처음 위치를 제외한 나머지를 반복한다.

```python
def selectionSort(a):
    for i in range(0, len(a) - 1):
        min_idx = i
        for j in range(i+1, len(a)):
            if a[min_idx] > a[j]:
                min_idx = j
        a[i], a[min] = a[min], a[i]
```



```python
arr = [10, 15, 2, 19, 6, 14]

for i in range(len(arr) - 1):
    min_idx = i
    for j in range(i+1, len(arr)):
        if arr[j] < arr[min_idx]:
            min_idx = j
    arr[i], arr[min_idx] = arr[min_idx], arr[i]
```

