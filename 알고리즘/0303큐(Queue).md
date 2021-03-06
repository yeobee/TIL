### 큐(Queue)

- 스택과 마찬가지로 삽입과 삭제의 위치가 제한적인 자료구조
- 큐의 뒤에서는 삽입만 하고 큐의 앞에서는 삭제만 이루어지는 구조
- 선입선출구조 (First In First Out)
  - 큐에 삽입한 순서대로 원소가 저장되어, 가장 먼저 삽입된 원소는 가장 먼저 삭제된다

- 머리(Front) :저장된 원소중 첫번째 원소
- 꼬리(Rear) : 저장된 원소중 마자막 원소
- 삽입: enQueue(item): 큐의 뒤쪽에 원소 삽입
- 삭제: deQueue(): 큐의 앞쪽에 원소를 삭제하고 반환하는 연산
- createQueue(): 공백 상태의 큐를 생성하는 연산
- isEmpty(): 큐가 공백상태인지 확인하는 연산
- isFull():큐가 포화상태인지를 확인하는 연산
- Qpeek(): 큐의 앞쪽에서 원소를 삭제없이 반환하는 연산



### 선형큐

- 1차원 배열을 이용한 규
  - 큐의크기 = 배열의 크기
  - front: 저장된 첫번째 원소의 인덱스
  - rear: 저장된 마지막 원소의 인덱스
  - 초기상태: front = rear = -1
  - 공백상태: front = rear 
  - 포화상태: rear = n-1 (n: 배열의크기, n-1:배열의 마지막 인덱스)



### 원형큐

- 초기 공백상태
  - front = rear = 0 으로 초기화

- index의 순환
  - front와 rear의 위치가 배열의 마지막 인덱스인 n-1을 가르킨 후, 그 다음에는 논리적 순환을 이루어 배열의 처음 인덱스인 0으로 이동해야함
  - 이들 위해 나머지 연산자 mod(%)를 이용함 





- 삽입 위치 및 삭제 위치 
- 선형큐 : rear = rear +1                         front = front+1
- 원형큐 : rear = (rear+1) mod(%)  n     front = (front+1) mod(%) n
- front 변수
  - 공백 상태와 포화 상태를 구분을 쉽게 하기 위해 front가 있는 자리는 사용하지 않고 형상 빈자리로 둠



### 연결큐

#### 단순 연결 리스트(linked list)를 이용한 큐

- 큐의 원소: 단순 연결 리스트의 노드
- 큐의 원소 순서: 노드의 연결 순서, 링크로 연결되어 있음
- front: 첫번째 노드를 가르키는 링크
- rear: 마지막 노드를 가르키는 링크
- 초기상태 :  front = rear = None
- 공백상태 : front = rear = None





### 버퍼

- 데이터를 한곳에서 다른 한 곳으로 전송하는 동안 일시적으로 그데이터를 보관하는 메모리의 영역