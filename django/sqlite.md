# sqlite



```
sqlite3 tutorial.sqlite3

.databases
.mode csv
/import hellodb.csv users_user



```

```
select : 데이터 조회
--모든 정보를 조회
sqlite>SELECT*FROM table;
특정한 테이블을 반환한다
-- 주석처리하는방법

sqlite> .headers on
sqlite> .mode column
sqlite> SELECT * FROM users_user;
id  first_name  last_name  age  country  phone
--  ----------  ---------  ---  -------  -------------
1   길동          홍          600  충청도      010-2424-1232
sqlite> .mode csv 다시 돌아감
1,"길동","홍",600,"충청도",010-2424-1232

--테이블생성
CREATE TABLE classmates(
    id INTEGER PRIMARY KEY,
    name TEXT
);

.tables
테이블목록조회
.schema classmates
특정테이블 조회

--테이블 삭제
DROP TABLE classmates;
```

