# SQL & ORM

## Database

### 데이터베이스

* 체계화된 **데이터**의 모임
* 몇 개의 **자료** 파일을 조직적으로 통합하여 자료 항목의 중복을 없애고 자료를 **구조화**하여 기억시켜 놓은 자료의 **집합체**
* 장점
  * 데이터 중복 최소화
  * 데이터 무결성(정확한 정보를 보장)
  * 데이터 일관성
  * 데이터 독립성(물리적/논리적)
  * 데이터 표준화
  * 데이터 보안유지



### 관계형 데이터베이스(RDB)

- 키와 값들의 간단한 관계(relation)를 표(table) 형태로 정리한 데이터베이스
- 관계형 모델에 기반
- 용어 정리
  - 스키마: 데이터베이스에서 자료의 구조, 표현방법, 관계 등 **전반적인 명세**를 기술한 것
  - 테이블: 열(칼럼/필드)과 행(레코드/값)의 모델을 사용해 조직된 데이터 요소들의 집합
  - 열: 각 열에는 고유한 데이터 형식이 지정됨
  - 행: 실제 데이터가 저장되는 형태
  - 기본키(Primary Key): 각 행의 고유 값. 반드시 설정해야 하며, 데이터베이스 관리 및 관리 설정 시 주요하게 활용 됨



### RDBMS

> 관계형 데이터베이스 관리 시스템

- 관계형 모델을 기반으로 하는 데이터베이스 관리시스템을 의미

  ex. MySQL, SQLite, ORACLE, MS SQL, PostgreSQL

#### SQLite

* 서버 형태가 아닌 파일 형식으로 응용 프로그램에 넣어서 사용 -> 기교적 가벼운 데이터베이스
* 구글 안드로이드 운영체제에 기본적으로 탑재. 임베디드 소프트웨어에도 많이 활용
* 고컬에서 간단한 DB 구성 가능. 오픈소스 프로젝트이므로 자유롭게 사용 가능

##### Sqlite Data Type

1. Null: 데이터 없음(=파이썬의 None)
2. INTEGER: 크기에 따라 0,1,2,3,4,6 또는 8바이트에 저장된 부호 있는 정수
3. REAL: 8바이트 부동 소수점 숫자로 저장된 부동 소수점 값
4. TEXT
5. BLOB: 입력된 그대로 정확히 저장된 데이터(별다른 타입 없이 그대로 저장)

+. Sqlite는 동적인 데이터타입을 가지고 있다. 한 테이블이 가질 수 있는 최대값은 900경이 넘는다

##### Sqlite Type Affinity

* Type Affinity: 특정 칼럼에 저장하도록 권장하는 데이터 타입

1. INTEGER(INT, INTEGER, TINYINT, SMALLINT, MEDIUMINT, BIGINT, UNSIGNED BIG INT, INT2, INT8)

2. TEXT(CHARACTER(20), VARCHAR(255), VARYING CHARACTER(255),NCHAR(55), NATIVE CHARACTER(70), NVARCHAR(100), TEXT, CLOB)

3. BLOB

4. REAL(REAL, DOUBLE, DOUBLE PRECISION, FLOAT)

5. NUMERIC(NUMERIC, DECIMAL(10,5), BOOLEAN, DATE,DATETIME)

   () 안에 있는 것: example typenames from the CREATE TABLE Statement.

   

## SQL(Structured Query Language)

- 관계형 데이터 관리시스템(RDBMS)의 **데이터 관리**를 위해 설계된 **특수 목적으로 프로그래밍 언어**
- 데이터베이스 스키머 생성 및 수정
- 자료의 검색 및 관리
- 데이터베이스 객체 접근 조정 관리



### SQL의 분류

| 분류                                             | 개념                                                         | 예시                            |
| ------------------------------------------------ | ------------------------------------------------------------ | ------------------------------- |
| DDL-데이터 정의 언어(Data Definition Language)   | 관계형 데이터베이스 구조(테이블, 스키마)를 정의하기 위한 명령어 | CREATE, DROP, ALTER             |
| DML-데이터 조작 언어(Data Manipulation Language) | **데이터를 저장, 조회, 수정, 삭제(C,R,U,D) 등을 하기 위한 명령어** | INSERT, SELECT, UPDATE, DELETE  |
| DCL-데이터 제어 언어(Data Control Language)      | 데이터베이스 사용자의 권한 제어를 위해 사용하는 명령어       | GRANT, REVOKE, COMMIT, ROLLBACK |



#### SQL Keywords-(DML)

- INSERT: 새로운 데이터 삽입(추가)
- SELECT: 저장되어있는 데이터 조회
- UPDATE: 저장되어있는 데이터 갱신
- DELETE: 저장되어있는 데이터 삭제



### CRUD

#### CREATE - 테이블 생성 및 삭제

```bash
#데이터베이스 생성하기
$ sqlite tutorial.sqlite3	#쉘 환경 open
sqlite> .database	#.: sqlite 프로그램의 기능을 실행

#csv 파일을 table로 만들기
sqlite> .mode csv	#mode 활성화
sqlite> .import hellodb.csv examples	#example 테이블로 csv 파일 import
sqlite> .tables		#현재있는 테이블 목록 확인
examples

#(optional)터미널 view 변경
sqlite> .headers on		#table의 헤더도 표시
sqlite> .mode column	#보기 쉬운 표 형식으로 바뀐다

#특정 테이블의 schema 조회
sqlite> .schema classmates
```

```sql
--SELECT(조회): 특정 테이블의 레코드(행) 정보를 반환
SELECT * FROM examples;	--;: 하나의 명령어가 종료되는 시점
--examples의 모든 데이터를 조회하는 명령어.

--DB에서 테이블 생성
CREATE TABLE classmates (	
	id INTEGER PRIMARY KEY, --스키마 지정. 기본키는 INTEGER 형태로만 지정가능!!
	name TEXT NOT NULL,
    address TEXT
);

--DB에서 테이블 제거
DROP TABLE calssmates;

--테이블에 단일 행(레코드) 삽입(생성)
INSERT INTO 테이블이름 (칼럼1, 칼럼2, ...) VALUES (값1, 값2);
INSERT INTO classmates (id,name,address) VALUES (1,'길동','서울');

--예시
CREATE TABLE classmates (
    --PRIMARY KEY 속성의 칼럼을 작성x -> 자동으로 증가하는 PK 옵션 가진 rowid 칼럼을 정의
	name TEXT NOT NULL,		--꼭 필요한 정보일 때 공백으로 비워두면 안되므로 NOT NULL 설정!
    age INTEGER NOT NULL	
    address TEXT
);

INSERT INTO classmates --한번에 여러명 입력하기. 전체 값을 다 넣는 것이므로 칼럼들은 생략
VALUES
('짱구',30,'서울'),
('유리',25,'대전'),
('훈이',27,'대구'),
('맹구',29,'부산'),
('철수',28,'경기')
```



#### READ

##### SELECT와 함께 사용하는 clause(절)

- LIMIT
  - 쿼리에서 반환되는 행 수 제한
  - 특정 행부터 시작해서 조회하기 위해 **OFFSET** 키워드와 함께 사용하기도 함
    - OFFSET: 동일 오브젝트 안에서 오브젝트 처음부터 주어진 요소나 지점까지의 변위차(위치 변화량)을 나타내는 정수형. 0부터 시작한다.
- WHERE
  - 쿼리에서 반환된 행에 대한 특정 검색 조건을 지정
- SELECT DISTINCT
  - 조회 결과에서 중복 행을 제거
  - DISTINCT 절은 SELECT 키워드 **바로 뒤**에 작성

```sql
SELECT * FROM 테이블이름 WHERE 조건;

SELECT rowid, name FROM classmates;		--모든 컬럼 값이 아닌 특정 컬럼만 조회하기
SELECT rowid, name FROM classmates LIMIT 1;				--하나만 조회
SELECT rowid, name FROM classmates LIMIT 1 OFFSET 2;	--세번째의 행만 조회
SELECT * FROM classmates LIMIT 10 OFFSET 5;				--6번째 행부터 10개를 출력

SELECT rowid, name FROM classmates WHERE address='서울';	--address가 서울인 것 조회
SELECT DISTINCT age FROM classmates;		--중복값 없이 조회
```



#### UPDATE

- 기존 행의 데이터를 수정.
- **SET** clause에서 테이블의 각 열에 대해 새로운 값을 설정

- 조건을 통해 특정 레코드 수정 => 중복 불가능한(UNIQUE) 값인 rowid를 기준으로 수정하자

```sql
UPDATE 테이블이름 SET 칼럼1=값1, 칼럼2=값2 WHERE 조건;
UPDATE classmates SET name='치타', address='제주도' WHERE rowid=5;
```



#### DELETE

- 테이블에서 행 삭제

- 중복 불가능한(UNIQUE) 값인 rowid 기준으로 삭제하자

- SQLite는 기본적으로 id를 재사용한다. 

  - 재사용 없이 다음 행 값을 사용하게 하려면?

    ->테이블을 생성하는 단계에서 AUTOINCREMENT를 통해 설정 가능.

    ​	id INTEGER PRIMARY KEY AUTOINCREMENT,

```sql
DELETE FROM 테이블이름 WHERE 조건;
DELETE FROM classmates WHERE rowid=5	--조건을 통해 특정 레코드 삭제하기
```



### WHERE

* 특정한 기준을 충족하는 행(row)에만 영향을 미치도록 지정

```sql
SELECT * FROM users WHERE age>=30;	--*: 전체
SELECT age, first_name FROM users WHERE age>=30 and last_name='김';
```



### Aggregate functions

- 집계함수. (값 집합에 대한 계산을 수행하고 **단일 값**을 반환. **여러행**으로부터 **하나의 결과값**을 반환하는 함수)

- <u>SELECT 구문</u>에서만 사용됨.

- Aggregate functions 종류. 

  - COUNT: 그룹의 항목 수를 가져옴

  - AVG: 모든 값의 평균을 계산

  - MAX: 그룹에 있는 모든 값의 최대값을 가져옴

  - MIN: 그룹에 있는 모든 값의 최소값을 가져옴

  - SUM: 모든 값의 합을 계산

    위 함수들은 기본적으로 해당 칼럼이 숫자(INTEGER)일 때만 사용 가능

```sql
SELECT COUNT(칼럼) FROM 테이블이름;	--레코드의 개수 조회하기

SELECT COUNT(*) FROM users;			--전체 사람들의 개수
SELECT AVG(age) FROM users WHERE age>=30;	--30살 이상인 사람들의 나이의 평균
SELECT first_name, MAX(balance) FROM users;	--계좌잔액이 가장 많은 사람과 그의 이름
```



### LIKE operator

- 패턴 일치를 기반으로 데이터를 조회하는 방법

- SQLite는 패턴 구성을 위한 2개의 wildcards 제공

  - %: 0개 이상의 문자. 이 자리에 문자열이 있을 수도, 없을 수도 있다.
  - _: 임의의 단일 문자. 반드시 이 자리에 한 개의 문자가 존재해야 한다.

  - wildcard character: 파일을 지정할 때, 구체적인 이름 대신에 여러 파일을 동시에 지정할 목적으로 사용하는 특수기호.(*, ? 등)
  - 주로 특정한 패턴이 있는 문자열 혹은 파일을 찾거나, 긴 이름을 생략할 때 쓰임.
    - 텍스트 값에서 알 수 없는 문자를 사용할 수 있는 특수문자로, 유사하지만 동일한 데이터가 아닌 여러 항목을 찾기에 매우 편리한 문자
    - 지정된 패턴 일치를 기반으로 데이터를 수집하는 데도 도움이 될 수 있음

```sql
SELECT * FROM 테이블 WHERE 칼럼 LIKE '와일드카드 패턴';	--패턴을 확인하여 해당하는 값을 조회

SELECT * FROM users WHERE age LIKE '2_';	--20대 조회
SELECT * FROM users WHERE phone LIKE '02-%'	--지역번호 02인 사람 조회
SELECT * FROM users WHERE first_name LIKE '%준'	--이름이 준으로 끝나는 사람 조회
SELECT * FROM users WHERE phone LIKE '%-5114-%'	--중간 번호가 5114인 사람 조회
```



### ORDER BY

- 조회 결과 집합을 정렬.
- SELECT 문에 추가하여 사용
- 정렬 순서를 위한 2개의 keyword 제공
  - ASC - 오름차순(default)
  - DESC - 내림차순

```sql
SELECT * FROM 테이블 ORDER BY 칼럼 ASC;	--특정 칼럼을 기준으로 데이터를 정렬해서 조회
SELECT * FROM 테이블 ORDER BY 칼럼1, 칼럼2 DESC;

SELECT * FROM users ORDER BY age ASC LIMIT 10;	--나이 상위 10명
SELECT * FROM users ORDER BY age,last_name ASC LIMIT 10;--나이와 성 순으로 상위 10명
--age가 먼저 정렬이 되고, 그 안에서 last_name을 정렬한다.
SELECT last_name, first_name FROM users ORDER BY balance DESC LIMIT 10	--계좌 잔액 순으로 내림차순 정렬하여 성과 이름을 10개만 조회
```



### GROUP BY

- 행 집합에서 **요약 행** 집합을 만듦.
- SELECT 문의 optional 절
- 선택된 행 그룹을 하나 이상의 열 값으로 요약 행으로 만듦
- 문장에 WHERE 절이 포함된 경우 **반드시 WHERE 절 뒤에 작성**
- **AS**를 활용해서 COUNT에 해당하는 **칼럼 명을 바꿔서 조회**할 수 있다.

```sql
SELECT 칼럼1, aggregate_function(칼럼2) FROM 테이블 GROUP BY 칼럼1, 칼럼2
--지정된 기준에 따라 행 세트를 그룹으로 결합. 데이터를 요약하는 상황에 주로 사용

SELECT last_name, COUNT(*) FROM users GROUP BY last_name	--각 성씨가 몇 명씩 있는지 조회
SELECT last_name, COUNT(*) AS name_count FROM users GROUP BY last_name	--COUNT(*)을 name_count로 이름 바꿔서 출력
```



### ALTER TABLE

* 3가지 기능

  1. table 이름 변경
  2. 테이블에 새로운 column 추가
  3. column 이름 수정
  4. column 삭제

  ```sql
  ALTER TABLE 기존테이블이름 RENAME TO 새로운테이블이름;	--테이블의 이름 변경
  ALTER TABLE 테이블이름 ADD COLUMN 칼럼이름 데이터타입설정;--새로운 칼럼 추가
  
  ALTER TABLE news ADD COLUMN created_at TEXT;
  --기존 레크드들에는 새로 추가할 필드에 대한 정보x-> NOT NULL 형태의 컬럼은 추가 불가능
  --NOT NULL 설정 없이 추가 or 기본값(DEFAULT) 설정
  ALTER TABLE news ADD COLUMN subtitle TEXT NOT NULL DEFAULT '소제목';--기본값 설정
  
  ALTER TABLE news RENAME COLUMN title TO main_title;	--칼럼 이름 바꾸기
  ALTER TABLE news DROP COLUMN subtitle;				--칼럼 지우기
  ```

  

### SQL과 ORM

- SQL

```sql
SELECT * FROM articles_article
SELECT * FROM articles_article WHERE rowid=1;
DELETE FROM articles_article WHERE id=1;
```
- ORM

```python
Article.objects.all()
Article.objects.get(pk=1)
Article.objects.get(pk=1).delete()
```

+. 테이블은 앱이름_모델이름(소문자)으로 생성.  

+. 모델 활성화 까먹지 말기

```bash
$ python manage.py makemigrations articles	#변경사항에 대한 마이그레이션 만들기
$ python manage.py migrate					#변경사항을 데이터베이스에 적용
$ python manage.py sqlmigrate articles 0001 #migration이 실행하는 SQL 문장을 보여줌
```

