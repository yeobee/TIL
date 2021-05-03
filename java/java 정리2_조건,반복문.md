# java 정리2-조건,반복문

## 조건문과 반복문



### 조건문 if statement

- if, else if ,else
  - 조건은 소괄호(condition) 안에 작성
  - 실행할코드는 중괄호{} 안에 작성
  - 블록 스코프 생성

```
if (condition) {
	do 
}else if (condition) {
	do
}else {
	do
}
```

### 조건문 switch statement

- switch
  - 표현식(expression)의 결과값을 이용한 조건문
  - 표현식의 결과값과 case문의 오른쪽 값을 비교
  - break 및 default문은 선택적으로 사용가능
  - break 문이 없는 경우 break 문을 만나거나 default문을 실행할때 까지 담음 조건문 실행
  - 블록 스코프 실행
  - default 는 else의 느낌과 똑같다

```
switch(expression) {
	case ' first value' :{
		do
		[break]
	}
	case ' second value' :{
		do
		[break]
	}
	[defualt:{
		do
	}]
}
```



## 반복문

### 반복문의 종류와 특징

- while
- for
- for... in
  - 주로 객체(object)의 속성들을 순회할때 사용
  - 배열도 순회 가능하지만 인덱스 순으로 순회한다는 보장이 없으므로 권장x
- for.. of
  - 반복 가능한(iterable) 객체를 순회하며 값을 꺼낼 때 사용
  - 반복 가능한 객체의 종류 
    - Array,Map,Set,String



### while

-  조건문이 참인 동안 반복시행
- 조건은 소괄호() 안에 작성
- 실행할 코드는 중괄호{} 안에 작성

```
while (conditon) {
	do
}
```



### for

- 세미콜론; 으로 구분되는 세부분으로 구성
- initialization
  - 최초 반복문 진입시 1회만 실행되는 부분
- condition
  - 매 반복 시행 전 평가되는 부분
- expression
  - 매 반복 시행 이후 평가되는 부분

```
for(초기값;조건;값의 증감){
	do
}
for(initialization; condition; expression){
	do something
}
```

### for..in

- 주로 객체(object)의 속성들을 순회할때 사용
- 배열도 순회 가능하지만 인덱스 순으로 순회한다는 보장이 없으므로 권장x
- 블록 스코프 생성

```
for (variable in object) {
	do
}
```

### for.. of

- 반복 가능한(iterable) 객체를 순회하며 값을 꺼낼 때 사용
- 반복 가능한 객체의 종류 
  - Array,Map,Set,String

```
for (variable of iterables) {
	do
}
```

```
const fruits = ['딸기','바나나','메론']
for (let fruit of fruits) {
	console.log(fruit)  // 딸기, 바나나, 메론
}
```

