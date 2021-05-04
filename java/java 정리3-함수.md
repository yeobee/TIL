# java 정리3-함수

## 함수

- 참조 타입 중 하나로써 function 타입에 속함
- 자바스크립트의 함수는 일급객체에 해당
  - 일급객체: 다음 조건들을 만족하는 객체
    - 변수에 할당가능
    - 함수의 매개변수로 전달가능
    - 함수의 반환 값으로 사용가능

### 선언식

- statement
- declaration

- function 함수명 (인자)

```
function add (num1,num2) {
	retrun num1+num2
}
add(7,2)
```



### 표현식

- 표현식 내에서 함수를 정의하는 방식
  - 표현식: 어떤 하나의 값으로 결정되는 코드의 단위
- 이름이 없는 함수를 '익명함수(anonymous function)'라고 명명
- 익명함수는 함수 표현식에서만 사용가능

```
const sub = function(num1,num2) {
	retrun num1-num2
}
sub(7,2)
```



### 기본인자(default arguments)

- 인자 작성시 '=' 문자 뒤 기본 인자 선언 가능



### 함수의 타입

- 함수도 하나의 값으로 평가됨
- 선언식,표현식 모두 타입은 function으로 동일(typeof)



### 호이스팅 -함수 선언식- 가능

- 함수 선언식으로 선언한 함수는 var로 정의한 변수처럼 hoisting 발생
- 함수 호출 이후에 선언 해도 동작

```
add(7,2)  // 9 

function add (num1,num2) {
	retrun num1+num2
}

```

### 호이스팅 - 함수 표현식 -불가능

- 반면 함수 표현식으로 선언한 함수는 hoisting 시 에러 발생
- 이는 함수를 변수에 할당함으로 변수로 평가되어 변수의 scope 규칙을 따르기때문

```
sub(7,2) // cannot access 'sub' before initialization

const sub = function(num1,num2) {
	retrun num1-num2
}

```



## Arrow Function

1. function 키워드 생략가능 -필수
2. 함수의 매개변수가 단하나 뿐이라면, '()' 생략가능 -선택
   1. 매개변수 없어서 ()만있으면 생략 불가능하다. 아니면 _언더바 로표현_
3. 함수 바디가 표현식 하나라면 '{}'와 return도 생략 가능- 선택

```
```

