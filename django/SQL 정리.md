- DDL (Data Definition Language) : CREATE, ALTER, DROP, (RENAME, TRUNCATE)
- DML (Data Manipulation Language) : INSERT, UPDATE, DELETE, MERGE, SELECT
- DCL (Data Control Language) : GRANT , REVOKE
- TCL (Transaction Control Language) : COMMIT, ROLLBACK, SAVEPOINT
  - dml 작업을 확정하거나 취소할 때 사용.

------

### **DDL**

- 데이터를 효율적으로 사용할 수 있도록 컴퓨터 안에 데이터를 저장하고 조직화 하는 방법을 구체화 하는 언어

- **CREATE** : create table (테이블 명) (컬럼, 컬럼, );

  ```
  CREATE TABLE 테이블_이름 (
      속성_이름 데이터_타입 [NOT NULL] [DEFAULT 기본값]               // 1
  
      [PRIMARY KEY (속성_리스트)]                                 // 2
      [UNIQUE (속성_리스트)]                                      // 3
      [FOREIGN KEY (속성_리스트) PREFERENCES 테이블_이름(속성_리스트)]  // 4
      [ON DELETE 옵션] [ON UPDATE 옵션]
      [CONSTRAINT 이름] [CHECK(조건)]                             // 5
  );
  ```

  1. **테이블을 구성하는 각 속성의 이름, 데이터 타입, 기본적인 제약 사항을 정의**한다.

  2. **기본키** : 테이블에 **하나**만 존재할 수 있다. (유일성, 최소성(꼭 필요한 속성으로 구성, 슈퍼키는(2개이상 구성) 최소성을 만족 못함.), 개체 무결성(Null 이 들어가면 안됨.))

  3. **대체키** : 테이블에 **여러 개** 존재할 수 있다. (유일한 속성이나 기본키가 아닌 키들, 기본키가 아니기에 NULL 값을 가질 수 있다.)

  4. **외래키** : 테이블에 **여러 개** 존재할 수 있다. (다른 테이블을 참조하는 키 (pk를 설정), 부모 테이블이 먼저 삭제 될 수 없다. 자식 삭제 후 부모 삭제해야함.)

  5. 데이터 무결성을 위한 **제약 조건** : 테이블에 **여러 개**의 제약조건이 존재할 수 있다.

     > 데이터 무결성 이란?저장된 데이터 값의 정확성을 의미관객수가 음수로 저장되면 무결성 위반유효성 검사를 하여 데이터 무결성을 유지CONSTRAINT CHK_ATD CHECK(attendance >= 0)

  - `[]`(대괄호에 감싸진 부분) 표시한 항목은 생략할 수 있다.
  - 모든 SQL 문은 **문장 끝에 세미콜론(`;`)을 표시**한다.
  - SQL 문에 사용되는 **키워드**(`CREATE TABLE`, `NOT NULL` 등)는 **대소문자를 구분하지 않는다**.
  - 속성 타입
    - 기본적으로 NULL 값이 허용.
    - 기본키는 개체 무결성(널, 중복 불가)을 지키기 위해 `NOT NULL` 필요
    - 속성에 기본 값을 지정하려면 `DEFAULT` 키워드를 사용.
    - BLOB (Binary Large Object) : 바이너리 값 그대로 저장.
  - `ON DELETE` / `ON UPDATE` **옵션**
    - NO ACTION : 참조하는 테이블의 데이터 삭제 불가
    - CASECADE : 참조하는 테이블 데이터 삭제시 참조하는 데이터도 같이 삭제
    - SET NULL : 참조하는 테이블 데이터 삭제시 NULL 로 속성값 변경 (NULL 허용 필요)
    - SET DEFAULT : 참조하는 테이블 데이터 삭제시 DEFAULT 값으로 변경 (DEFAULT 값 설정 필요.)

- **ALTER**: 테이블 변경 ( 속성 추가 / 삭제, 제약조건 추가 / 삭제)

  - 속성 추가

    ```
    ALTER TABLE 테이블_이름
        ADD 속성_이름 데이터_타입 [NOT NULL] [DEFAULT 기본값];
    
    ALTER TABLE Movie ADD created_at DATETIME;
    ```

  - 속성 삭제

    ```
    ALTER TABLE 테이블_이름
      DROP 속성_이름 CASCADE|RESTRICT;
    // 제약조건이나 참조하는 속성이 존재할 때
    // cascade : 함께 삭제 / restrict : 삭제를 막는다.
    
    ALTER TABLE Movie DROP created_at RESTRICT;
    ```

  - 제약 조건 추가

    ```
    ALTER TABLE 테이블_이름
      ADD CONSTRAINT 제약조건_이름 제약조건_내용;
    
    ALTER TABLE Movie
      ADD CONSTRAINT CHK_ATD CHECK(attendance >= 0);
    ```

  - 제약조건 삭제

    ```
    ALTER TABLE 테이블_이름
      DROP CONSTRAINT 제약조건_이름;
    ```

  - 테이블 명 변경

    ```
    ALTER TABLE 테이블명 RENAME TO 새 테이블명;
    ```

  - 컬럼명 변경 (테이블 생성, 데이터 복사, 기존 테이블 삭제, 테이블명 변경)

- **DROP** : 테이블 삭제

  ```
  DROP TABLE 테이블_이름 CASCADE|RESTRICT;
  ```

- **TRUNCATE** : 데이터 베이스 초기화 (데이터 삭제)

  ```
  // sqlite 는 truncate table 이 없음.
  DELETE FROM 테이블_이름
  ```

- **COMMENTS** : 주석 한줄 '--' , 여러줄'/**/'

### **DML**

- 유저들이 데이터를 입력, 수정, 삭제, 병합 하려고 할 때 사용하는 언어

- SELECT : 테이블에서 원하는 데이터를 검색하기 위해 사용

  - **기본 검색**

    ```
    SELECT [ ALL|DISTINCT ] 속성_리스트
    FROM 테이블_리스트;
    ```

    - DISTINCT : 중복행 제거
    - 검색 하고 싶은 속성의 이름을 `,` 로 구분하여 나열
    - FROM 키워드와 함께 검색하고 싶은 속성이 있는 테이블의 이름을 `,` 로 구분하여 나열
    - SELECT의 결과도 테이블 형태 ( 다양하게 subquery 이용 가능)

    ```
    SELECT 영화제목, 개봉연도, 관객수
    FROM 영화;
    
    SELECT *
    FROM 영화;
    
    SELECT 감독
    FROM 영화;
    
    SELECT DISTINCT 감독
    FROM 영화;
    
    SELECT DISTINCT 감독 AS 감독이름
    FROM 영화;
    ```

  - **산술식 검색**

    - 산술식은 속성의 이름과 `+`, `,`, `/` 등의 산술 연산자와 상수로 구성한다.

    - **실제 테이블의 값이 변경되지 않으며**, **결과 테이블에서만 계산한 결과 값을 출력**한다.

      ```
      SELECT 영화이름, 관객수 + 10000 AS 조정 관객수
      FROM 영화;
      
      영화이름 | 조정 관객수
      -------------------
      뮬란    | 10032 (기존 32)
      
      SELECT 이름, 월급, 월급*12 AS "연봉"
      FROM 부서명록;
      
      이름 | 월급 | 연봉
      ----------------
      철수 | 300 | 3600
      영희 | 400 | 4800
      영수 | 500 | 6000
      ```

  - **조건 검색**

    - 특정 조건을 붙여서 검색을 할 수 있다.

    - 연산자는 기본적인 `= , != , <> , < , > , <=, >` 사용 가능

      ```
      SELECT [ ALL|DISTINCT ] 속성_리스트
      FROM 테이블_리스트
      [ WHERE 조건 ];
      
      SELECT 이름, 월급, 월급*12 AS "연봉"
      FROM 부서명록
      WHERE 이름=영수;
      
      이름 | 월급 | 연봉
      ----------------
      영수 | 500 | 6000
      ```

    - 비교 연산자 외 `IN, BETWEEN` 사용 가능

      ```
      WHERE col_1 = 100
      WHERE col2 IN (2, 7, 9)
      WHERE col4 BETWEEN 10 AND 20
      ```

    - 논리 연산자 `AND, OR`사용 가능

      ```
      WHERE col_1 = 100 AND col_2 = 1
      WHERE col_1 = 100 OR col_2 = 2
      ```

  - **LIKE 이용**

    - 검색 조건을 명확히 모르고 부분적 일치하는 데이터를 검색하고 싶을 때 사용
    - 단, 문자열을 이용하는 조건에서만 사용 가능
    - 와일드 카드
    - `%` : 0 개 이상의 문자(문자의 내용과 개수는 상관없음)
    - `_`: 1개 이상의 문자 (문자의 내용은 상관 없음)
      - `LIKE '봉%'` : 봉으로 시작하는 문자열 (길이는 상관 없음)
      - `LIKE '%봉'` : 봉으로 끝나는 문자열 (길이 상관 없음)
      - `LIKE '%봉%'` : 봉이 중간에 포함된 문자열
      - `LIKE '봉__'` : 봉으로 시작하는 3글자 문자열
      - `LIKE '_봉%'` : 두번째 글자가 봉인 문자열(길이 상관없음)
      - `LIKE 'get_value' ESCAPE '_'` : 찾으려는 글자에 _ 가 있는 경우

    ```
    SELECT 영화이름, 개봉연도, 관객수
    FROM 영화
    WHERE 감독 LIKE '봉%';
    ```

  - GLOB 연산

    - LIKE와 유사하나 유닉스의 와일드 카드를 사용하게 해줌. `, ?, [a-z], [A-Z], [0-9]`

  - **NULL 을 이용한 검색**

    - IS NULL 키워드를 사용해 특정 속성의 값이 널 값인지 비교할 수 있다.
    - IS NOT NULL 키워드를 통해 널이 아닌지 비교할 수 있다.
    - 속성 = NULL 형태로 표현하면 안되며 반드시 IS NULL 키워드 사용

    ```
    SELECT 영화이름
    FROM 영화
    WHERE 감독 IS NULL;
    ```

  - **정렬 검색**

    - 사용자가 원하는 순서로 출력하려면 ORDER BY 키워드를 사용

    ```
    SELECT [ ALL|DISTINCT ] 속성_리스트
    FROM 테이블_리스트
    [ WHERE 조건 ]
    [ ORDER BY 속성_리스트 [ ASC|DESC] ]
    [ LIMIT 표시할_개수];
    ```

    - ASC(기본 오름차순) / DESC (내림차순)
    - LIMIT 로 데이터의 개수를 제한할 수 있다.

  - **집계 함수를 이용한 검색**

    - 특정 속성 값을 통계적으로 계산한 결과를 사용하기 위해 집계(aggregation ) 함수를 이용할 수 있다.
    - 열 함수라고도 부른다.
      - COUNT : 속성값의 갯수
      - MAX : 최대값 / MIN : 최소값
      - SUM : 속성 값의 합계(숫자만) / AVG : 속성 값의 평균(숫자만)
    - 주의사항
      - NULL 속성은 제외 하고 계산
      - WHERE 절에서는 사용할 수 없다.
      - SELECT 나 HAVING 절에서만 사용 가능.

    ```
    SELECT AVG(관객수)
    FROM 영화;
    
    열 이름 없음
    ---
    18146875
    
    // 감독의 수를 중복 없이 검색
    // 봉 감독 영화가 5개 있을때 distinct 가 없으면 5명으로 집계됨.
    SELECT COUNT(DISTINCT 감독) AS '감독 수'
    FROM 영화;
    ```

  - **그룹별 검색**

    - 테이블에서 특정 속성의 값이 같은 튜플을 모아 그룹을 만들어 그룹별로 검색할 수 있다.
    - 그룹에 대한 조건을 추가 하려면 `GROUP BY` 키워드와 `HAVING`키워드를 함께 사용.

    ```
    SELECT [ ALL|DISTINCT ] 속성_리스트
    FROM 테이블_리스트
    [ WHERE 조건 ]
    [ GROUP BY 속성_리스트 [ HAVING 조건 ] ]
    [ ORDER BY 속성_리스트 [ ASC|DESC ] ];
    ```

    - 그룹별로 검색할 때는 SELECT 절에 그룹을 나누는 기준이 되는 속성을 함께 작성하는 것이 좋다.

      - 기준 속성이 없으면 어떤 그룹에 대한 검색 결과인지 확인하기 어렵기 때문

      ```
      SELECT COUNT(*) AS 총 영화 개수
      FROM 영화
      GROUP BY 감독;
      // 어느 감독의 영화 개수인지 확인하기 어려움.
      총 영화 개수
      ---
      3
      1
      2
      
      SELECT 감독, COUNT(*) AS 총 영화 개수
      FROM 영화
      GROUP BY 감독;
      
      감독 | 총 영화 개수
      ---
      봉준호 | 3
      샘 멘데스 | 1
      그레타 거윅 | 2
      
      SELECT *
      FROM COMPANY
      GROUP BY name
      HAVING count(name) < 2;
      ```

  - **조인(Join) 검색**

    - 두 개 이상의 테이블을 연결해서 하나의 테이블 처럼 만드는 것.

    - 각각의 테이블에 분산되어 있는 데이터를 하나로 묶어서 쿼리 할 수 있다.

    - JOIN으로 묶여진 결과는 하나의 큰 테이블처럼 생각할 수 있다.

    - 테이블을 접합할 수 있는 접합 컬럼(속성)이 필요하고 이 속성을 조인 속성이라고 부름 .

    - 일반적으로 외래키를 조인 속성으로 이용.

    - 조인 속성의 이름은 달라도 되지만 도메인은 반드시 같아야 한다.

    - INNER JOIN

      - 가장 흔하게 쓰이는 JOIN 방식

      - 두 테이블이 연결되는 방식은 교집합과 비슷.

      - 두 테이블 중 하나만 있으면 INNER JOIN에서는 제외

        ```
        SELECT {결과칼럼...} FROM {Table1} [as alias1]
        {INNER|LEFT|CROSS} JOIN {Table2} [as alias2]
        ON {연결조건}  / USING (일치칼럼)
        [GROUP BY 속성_리스트]
        [ORDER BY 속성_리스트]
        ```

        - ON alias1.colA = alias2.colB 형태로 연결 조건을 정의
        - 공통 칼럼 이름이 같고, 그 칼럼의 값이 같은 행끼리 연결 한다면 USING 컬럼명

    - LEFT JOIN

      - 두 테이블 중 값이 없으면 NULL을 채워서 연결.
      - 테이블 순서에 따라 결과 값이 달라짐.

      ```
      SELECT count(*) FROM albums
      LEFT JOIN artists USING (artistid);  -- 347
      
      SELECT count(*) FROM artists
      LEFT JOIN albums USING (artistid); -- 418
      ```

      - 세개 이상의 테이블을 붙일 때는 (A + B) + C 식으로 테이블을 합치면 됨.

        ```
        -- 아티스트의 각 앨범과 앨범 수록곡의 수
        SELECT a.name, title, count(b.trackid)
        FROM artists as a
        LEFT JOIN albums USING (artistid)
        LEFT JOIN tracks USING (albumid)
        GROUP BY b.albumid;
        ```

    - SELF JOIN

      - 특정한 조건에 해당하는 행을 찾기 위해서 자기 자신을 JOIN 하는 경우

        ```
        -- 각 직원의 풀네임과 그 직속 상관의 풀네임
        SELECT a.firstname || ' ' || a.lastname AS fullname,
               b.firstname || ' ' || b.lastname AS directReportsTo
        FROM employees a
        INNER JOIN employees b ON a.reportsto = b.employeeid
        ;
        ```

        - 문자열을 연결하기 위해 `||` 연산자 사용.

    - CROSS JOIN

      - JOIN이 수행될 때 ON이나 USING 으로 한정하는 절이 없으면 n * m 개의 행을 가진 모든 조합을 만들어 냄.
      - FROM 에서 두 개의 테이블을 컴마로 나열하기만 해도 같은 효과를 얻을 수 있다.

  - **서브 쿼리 검색**

    - 다른 SELECT 문 안에 내포된 SELECT 문

    - 괄호로 묶어 작성하며 ORDER BY 절을 사용할 수 없다.

    - 상위 질의문 보다 먼저 수행되며 이 결과물을 이용해 상위 질의문을 수행하여 최종 결과 테이블을 반환한다.

      ```
      // SELECT 에 사용 (스칼라 서브쿼리) 결과는 하나만 출력되어야 함.
      SELECT CD_PLANT,NM_PLANT,(SELECT AVG(UM) FROM TABLE_ITEM) AS UM
      FROM TABLE_PLANT;
      
      // FROM 에 사용 (인라인 뷰) 서브쿼리에서 조회된 값을 테이블 처럼 활용 가능.
      SELECT title, author, reg_date
      FROM (
          SELECT * FROM board
      )
      ORDER BY reg_date DESC;
      
      // WHERE에 사용
      Select CD_PLANT
      FROM TABLE_PLANT
      WHERE CD_PLANT IN (SELECT CD_PLANT FROM  TABLE_PLANT WHERE PLANT ='1000' AND COMPANY = '0327')
      ```

  - **Localtime 으로 조회**

    - 실제 DB는 UTC 기준으로 저장된다. (각 로컬 시간에 대한 계산이 용이하기 때문)

      ```
      SELECT title, datetime(updated_at, 'localtime') AS updated_at
      FROM articles_article;
      ```

- **INSERT** : 테이블에 원하는 튜플을 삽입하기 위해 사용

  - 직접 삽입

    - INTO 키워드와 함께 튜플을 삽입할 테이블 이름을 제시한 후, 속성 이름을 나열하며 나열한 순서대로 VALUES 키워드 다음의 값들이 차례로 삽입된다.
    - INTO 절의 속성 이름과 VALUES 절의 속성 값은 순서도 동일하고 갯수도 같아야 한다.
    - INTO 절의 속성 이름 리스트를 생략할 수 있는데, 생략한 경우에는 테이블을 정의할 때 속성의 순서대로 VALUES 절의 속성 값이 삽입된다.
    - VALUES 절에 나열되는 속성 값은 문자나 날짜 타입의 경우에는 작은 따옴표로 묶어야 한다.

    ```
    INSERT
    INTO 테이블_이름[(속성_리스트)]
    VALUES (속성값_리스트)[, (속성값_리스트)];
    ```

  - 서브 쿼리를 이용한 삽입

    - SELECT 문을 이용해 다른 테이블에서 검색한 데이터를 튜플로 삽입할 수 있다.

    ```
    INSERT
    INTO 테이블_이름[(속성_리스트)]
    SELECT 문;
    
    INSERT INTO COMPANY_BKP
    SELECT * FROM COMPANY
    WHERE ID IN (SELECT ID
                 FROM COMPANY);
    ```

- **UPDATE** : 테이블에 저장된 데이터를 수정하기 위해 사용.

  - 특정 속성의 값을 수정
  - SET 키워드 다음에 값을 어떻게 수정할지 작성
  - WHERE 절을 생략하면 모든 튜플을 수정함.

  ```
  UPDATE 테이블_이름
  SET 속성_이름1=값1, 속성_이름2=값2, ...
  [ WHERE 조건 ];
  ```

- **DELETE** : 테이블에 저장된 데이터를 삭제하기 위해 사용.

  - WHERE 이 없으면 모든 튜플을 삭제하여 빈 테이블을 만든다.

  ```
  DELETE
  FROM 테이블_이름
  [ WHERE 조건 ];
  ```

- Trigger : Insert, Update, Delete 문이 실행될 때 자동으로 실행되게 명명된 데이터베이스 개체

- 주로 데이터가 변경 될 때마다 기록하고자 하는 경우 사용

  ```
  CREATE TRIGGER [IF NOT EXISTS] trigger_name
     [BEFORE|AFTER|INSTEAD OF] [INSERT|UPDATE|DELETE]
     ON table_name
     [WHEN condition]
  BEGIN
     statements;
  END;
  
  CREATE TRIGGER update_articles_updatetime
      BEFORE UPDATE
      ON articles_article
  BEGIN
      UPDATE articles_article SET updated_at = datetime('now') WHERE id = OLD.id;
  END;
  ```

  - 작성된 trigger 전체 목록 확인

    ```
    SELECT * FROM sqlite_master WHERE type = 'trigger';
    ```

### **TCL**

- DBMS를 사용할 수 있는 권한 및 유저가 생성한 각종 객체를 사용할 수 있는 권한을 관리하는 언어;

- COMMIT : 작업 결과 반영

  ```
  BEGIN;
   실행할 SQL 구문
   실행할 SQL 구문
  COMMIT;
  ```

- ROLLBACK : 작업 취소 및 원래대로 복구

- GRANT : 사용자에게 권한 부여

- REVOKE : 사용자 권한 취소