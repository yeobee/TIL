# Vue Server& Client

## Server- 정보제공

- 클라이언트에게 정보,서비스를 제공하는 컴퓨터 시스템
- Django를 통해 응답한 template
- DRF를 통해 응답한 Json



## Client- 정보요청&표현

- 서버에게 그 서버가 맞는 서비스를 요청하고
- 서비스 요청을 위해 필요한 인자를 서버가 원하는 방식에 맞게제공
- 서버로 부터 반환되는 응답을 사용자에게 적절한 방식으로 표현 하는 기능을 가진 시스템 



### SOP same-origin policy

- 동일 출처 정책
- 특정 출처에서 불러온 문서나 스크립트가 다른 출처에서 가져온 리소스와 상호작용 하는 것을 제한하는 보안방식
- 두 URL의 Protcocol, Port, Host가 모두 동일한 출처라고 할수 있음



### CORS Cross-Origin Resource Sharing

- 교차 출처 리소스(자원) 공유
- 추가 HTTP header를 사용하여, 특정 출처에서 실행중인 웹 애플리케이션이 다른 출처의 자원에 접근 할 수 있는 권한을 부여 하도록 브라우저에 알려주는 체제
- 리소스가 자신의 출처와 다를때 교차 출처 http요청을 실행
- 다른 출처의 리소스를 불러오려면 그 출처에서 올바른 CORS header를 포함한 응답을 반환해야함



### Access-Control-Allow-origin 응답헤더

- 이 응답이 주어진 출처(origin)으로 부터 요청 코드와 공유가 될수있는 지를 나탐냄
- ex
- Access-Control-Allow-origin: * 



- 브라우저 리소스에 접근하는 임의의 origin으로 부터 요청을 허용한다고 알리는 응답에 포함
- '*' 는 모든 도메인에서 접근 할수 있음을 의미
- '*' 외에 특정 origin 하나를 명시할 수있음



### CORS 시나리오 예시

- vue.js 에서 A서버 요청
- A서버는 Access-Control-Allow-origin에 특정한 origin을 포함 시켜 응답
- 서버는 CORS Policy와 직접적인 연관이없고 그저 요청에 응답함
- 브라우저는 응답에 Access-Control-Allow-origin를 확인한 후 허용 여부를 결정
- 프레임워크 별로 이를 지원하는 라이브러리가 존재
- django는 django-cors-headers 라이브러리를 통해 응답헤더 및 추가 설정 가능



### CORS

- 브라우저 & 웹 어플리케이션 보호
  - 악의적인 사이트의 데이터를 가져오지 않도록 사전차단
  - 응답으로 받는 자원에 대한 최소한의 검증
  - 서버는 정상적으로 응답하지만 브라우저에서 차단

- Server의 자원 관리
  - 누가 해당 리소스에 접근 할 수 있는지 관리 가능

- CORS 표준에 의해 추가된 HTTP Header를 통해 이를 통제