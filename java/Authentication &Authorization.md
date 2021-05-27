# Authentication &Authorization

### Authentication(인증)

- 인증,입증
- 자신이 주장하는 사용자가 누구인지 확인하는 행위
- who are U?
- 모든 보안 프로세스의 첫번째 단계(가장기본 요소)
- 401 Unauthorized
  - 미승인 이지만 의미상 이응답은(비인증)이다



### Authorization(권한/허가)

- 권한 부여, 허가
- 사용자에게 특정 리소스 또는 기능에 대한 액세스 권한을 부여하는 과정
- 보안 환경에서 권한 부여는 항상 인증을 따라야함
- 서류의 등급, 웹페이지에서 글을 조회 삭제 수정 할수 잇는 방법
- 403 Forbidden
  - 서버는 클라이언트가 누구인지는 알고있음



### 다양한 인증방식

1. session Based
2. Token Based
   1. JWT!!!!!!
3. Authentication platform



### JWT

- JSON 포맷을 활용하여 요소 간 안전하게 정보를 교환하기 위한 표준 포맷
- 암호화 알고리즘에 의한 디지털 서명이 되어있기 때문에 자체로 검증 가능하고 신뢰할 수 있는 정보 교환체계
- JWT 자체가 필요한 정보를 모두 갖기 때문에 이를 검증할 필요없다
- 상대적으로 HTML,HTTP 환경에서 사용하기 용기
  - session은 유저의 session 정보를 server에 보관해야함
  - jwt는 하지만 client side에 토근 정보를 저장하고 필요한 요청에 같이 넣오 보관



### JWT 구조

1. Header
   - 토큰의 유청과 Hashing algorithm으로 구성

2. Payload
   1. 토큰에 넣을 정보
   2. claim은 정보의 한조각을 의미하며 payload에는 여러개의 claim을 넣을수 있다
   3. 종류 에는 Registered, Private,

3. Signature
   1. Header와 Payload의 encoding 값을 더하고 거기에 private key로 hashing 하여 생성



| 인증 수단의 저장 위치   | server          | client          |
| ----------------------- | --------------- | --------------- |
| 인증 수단의 정보 민감성 | low             | high            |
| 유효기간                | y               | y               |
| 확장성                  | 상대적으로 낮음 | 상대적으로 높음 |

