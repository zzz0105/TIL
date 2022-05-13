# SQLD

## [최종 정리강의](https://www.youtube.com/channel/UCosmeBx3OuKP1YwGmT6ar2Q)

- SQL 연산 순서

  - from - where - group by - having - select - orderby

- 종류

  - DML: select, insert, delete, update
  - DDL: alter, create, modify, drop
  - DCL: grant, revoke
  - TCL: rollback, commit

- select

  - distinct
    - 중복된 값들이 존재할 때 원하는 정보를 집약시켜주는 기능
    - Distinct deptno, mgr
      - 사실상 Distinct (deptno, mgr) 이것과 같은 의미. deptno와 mgr에 대해 distinct가 들어가는 것. group by (deptno, mgr)과 비슷하다.
  - as
    - select절에서의 as
      1. as 생략 가능
      2. column명에 띄어쓰기가 있는 경우
         - ex. "직원 번호"
    - from절에서의 as
      1. as 사용 불가
  - concat 함수: 인수가 반드시 2개여야 한다. 
    - +: SQL server
    - ||: oracle

- 논리연산자

  - 종류

    - and: A와 B를 모두 만족
    - or: 하나 이상의 조건이 만족
    - not: 조건을 부정

  - 연산순위

    1. not
    2. and
    3. or

    ex. not <조건1> and <조건2> and not <조건3> or <조건4>

    ​		: 조건1과 조건3을 부정한다. 그 후 and를 계산하고 or을 계산한다.

- sql 연산자

  - between and

    - A between 1 and 2: A가 1이상 2이하인 것

  - in

    - A in (1,2,3): A는 1이거나 A는 2이거나 A는 3

  - **like**

    - 와일드 카드

      - _: 미지의 한 글자
      - %: 0 이상의 글자

      ex. _L%: 두번째 글자가 L인 것

    - escape

      - 와일드카드인 _와 %를 문자로 취급해주는 함수

      ex. name like 'A@_A' escape '@': _를 문자로 취급하게 된다.

      ex. name like '%#%%' escape '#': 문자 %를 포함한 것을 찾는다.

  - Rownum (oracle)

    - where 조건절에서 Rownum이 1인 경우 포함
      - Rownum은 적층구조. 범위형태로 주어야 한다. 

    ex. select from empno, cell where rownum<=3 order by sal desc

    - order by sal이 가장 마지막에 시행된다. 따라서 정렬 전에 rownum에 의한 조건절이 시행된다. 따라서 rownum이 3이하인 것을 뽑고 난 후에 그 행에 대해 내림차순으로 정렬된 것이 출력된다.

  - Top (sqlserver)

    - Top (n) <컬럼명>: select 절에서 컬럼명을 출력할 때 상위 n개의 행을 가져온다.

- **null**

  - 정의: 부재. 모르는 값.

  - 산술 연산

    - null + 2 -> null
    - null - 4 -> null
    - null x null -> null

  - 비교 연산

    - null = null -> 알 수 없음(unknown)
    - null = 2 -> 알 수 없음(unknown)

    where 조건절에 unknown이 들어오면 False라고 판단함

  - 정렬 상 의미

    - oracle에서는 ∞의 의미
    - sql server에서는 최소의 값. -∞

  - 함수

    - nvl(값1, 값2): 값1이 null이라면 값2, null이 아니라면 값1.
    - nvl2(값1, 값2, 값3): 값1이 null이면 값3. null이 아니라면 값2
    - isNull(값1, 값2): 값1이 null이라면 값2, null이 아니라면 값1.
    - nullif(값1, 값2): 2개의 값이 같으면 null 다르면 값1
    - coalesce(값1, 값2, ...): null 아닌 첫번째 값

- 정렬

  - 특성

    1. <u>가장 마지막에 실행</u>
    2. 쿼리문을 돌릴 때 성능이 느려질 가능성이 있다. 
    3. null값과의 관계
       - oracle에서는 ∞로, sql server에서는 -∞로 취급된다

  - 컬럼 번호 정렬

    - 출력되는 컬럼의 수보다 큰 값이 <u>허용되지 않는다.</u>

    - 출력되지 않는 컬럼명으로 정렬 가능하다.

      ex. select name order by sal

  - 인수 2개의 정렬

    ex. sal desc, name asc: sal이 같은 경우 name 오름차순으로 정렬

- 숫자 함수

  - round: 반올림

    ex. round(138.94) -> 139	// 두번째 파라미터의 값이 0이라서 생략되어있다.

    ​	  round(123.57, 1) ->123.6 

  - ceil(oracle) / ceiling(sql server): 올림함수. round와 같이 두번째 파라미터는 어느 자리에서 연산할지.

- 문자열 함수

  - upper(문자열): 대문자로 변환
  - lower(문자열): 소문자로 변환
  - lpad(값, 총 문자길이, 채움문자): 지정한 길이만큼 왼쪽부터 특정 문자로 채워줌
    - 채움문자를 지정하지 않으면 공백으로 해당길이만큼 문자를 채운다
  - rpad(값, 총 문자길이, 채움문자): 지정한 길이만큼 오른쪽부터 특정 문자로 채워줌
    - 채움문자를 지정하지 않으면 공백으로 해당길이만큼 문자를 채운다
  - trim(문자열): 문자열의 양쪽 공백을 제거
  - ltrim(문자열, 제거할 문자열): 문자 왼쪽의 반복적인 문자를 제거를 한다. 
    - 옵션을 쓰지 않았을 때: 문자열의 왼쪽 공백 제거
  - rtrim(문자열, 제거할 문자열): 문자 오른쪽의 반복적인 문자를 제거를 한다. 
    - 옵션을 쓰지 않았을 때: 문자열의 오른쪽 공백 제거
  - substr(문자열, 시작위치, 길이): 문자열을 자른다.
    - 길이를 쓰지 않으면 끝까지. 위치는 맨 첫글자부터 1이다.
  - instr(문자열, 찾을 문자열, 시작 위치, 발생횟수): 문자열에서 찾고자 하는 문자열과 일치하는 위치를 반환
    - 시작위치와 발생횟수의 디폴트 값은 1이다.
  - replace(문자열 혹은 열 이름, 바꾸려는 문자열, 바뀔 문자열): 특정 문자열을 찾아 바꾸는 함수

- 날짜함수

  - to_char: 날짜, 숫자 등의 값을 문자열로 변환하는 함수. 데이터의 형변환을 일으키는 함수
  - to_date: 날짜 데이터 타입으로 변화해 주는 함수. 데이터의 형변환을 일으키는 함수
  - sysdate: 오라클에서 현재 시간을 출력해주는 함수
  - getdate: sql server에서 현재 시간을 출력해주는 함수

  날짜 데이터 + 100 -> 100일 이후. day로 인식한다.

- decode/case

  - decode: if와 비슷하다.

    ```sql
    decode(A, 1, 'a',   -- null은 생략 가능
              2, 'b',   
              3, 'c',   
                ,'d')  
    --A가 1이면 a, 2이면 b, 3이면 c, 이외에는 d를 출력  
    ```

  - case

    ```sql
    case 조건 when 결과1 then 출력1
    		 [when 결과2 then 출력2]	
    else 출력3	--else가 없는 경우 조건1, 조건2 만족하지 않을 때 null이 출력된다.
    end 컬럼명
    ```

- **집계함수**

  - null과의 관계

    - | A    | B    | C    |
      | ---- | ---- | ---- |
      | null | null | 1    |
      | 3    | 2    | 2    |
      | null | 2    | 3    |

      sum(A) = 3			sum(B) = 4		

      count(A) = 1		 count(*) = 3

      sum(A+B+C) = 7: 새로운 column을 만들고 풀어라. (A+B+C는 null 7 null로 나온다.)

      * sum(A+B+C)와 sum(A) + sum(B) + sum(C)는 다르다

- group by

  - 집약기능이 있다.
  - 그룹 수준으로 정보를 바꾼다.
  - having도 그룹에 대한 조건식이다.

- join

  - natural join using
    - 중복된 컬럼이 사라진다. 제일 앞에 등장하는 것 하나만 출력됨.  
    - using의 경우 alias 사용 가능
  - left outer join
    - 'A left outer join B' = 'A col1 = B col1 (+)'
      - 이 때 col1이 조인키이다.
      - A, B 순서 같고 left라서 (+)가 오른쪽에 붙는다

  - join하면 할수록 column이 늘어난다.

  - 조인 순서
    - from A, B, C: A, B 조인한 후 하나의 테이블이 되었을 때 C와 조인한다.
  
- 서브 쿼리

  - select: scalar(단일 행 서브쿼리)
  - from: inline view(메인쿼리에 컬럼 사용 가능하다)
  - where: 거의 모든 서브쿼리(중첩서브쿼리)
  - group by: 서브쿼리가 들어가지 않는다
  - having: 거의 모든 서브쿼리(중첩서브쿼리)
  - order by: scalar
  - 상호연관 서브쿼리가 있을 때 select from A where (select from B...)
    - A 테이블 row를 하나 볼 때 전체 테이블 B를 본다. 
  - 함수
    - in
    - any/some
    - all
    - exist: 모든 문자 사용 가능. 존재하면 True, 0 rows인 경우 False

- 집합 연산자

  - union: 중복을 제거한 합집합
  - intersect: 교집합
  - minus
    - 차집합
    - sql 서버에서는 except라고 한다
  - unionall
    - 중복 데이터 존재. 정렬 작업이 없고 빠르다(나머지 셋은 정렬 작업 존재 -> 느림)

- DDL

  - TCL과 연관지어서 생각하기
  - Truncate(입주민 퇴거. 구조 남음. log data 남음) vs Drop(건물 철거. 구조 삭제)
  - Truncate(DDL) vs Delete(DML)

- DML

  - TCL과 연관지어서 생각하기
  - insert: 지정한 매개변수와 value의 개수가 다를 때 -> 오류상황
  - update
  - delete
  - merge -> 37회 기출 참고

- **제약조건**

  - pk: unique + notnull. 대표성 가지므로 하나만 있다
  - unique
  - notnull

- DCL

  - grant: 사용자(User)에게 접속권한, 오브젝트 생성권한, DBA 권한 등을 부여할 수 있는 명령어
  - revoke: 사용자(User)에게 부여한 권한을 다시 회수하는 명령어 
  - role 특징(role의 type은 object이다)
    - role을 사용하면 권한 부여와 회수를 쉽게 할 수 있다
    - 한 사용자가 여러 Role을 access할 수 있고, 여러 사용자에게 같은 Role을 부여할 수 있다
    - 사용자는 Role에 Role을 부여할 수도 있다
  - 37회 기출문제 on to

- view

  - sql 명령문 저장. 기존 테이블보다 저장 공간이 적게 필요함
  - **장점**
    - 독립성: 기존 table 구조가 변경되어도 view의 구조는 변경되지 않는다. view를 따로 업데이트하지 않아도 된다.
    - 편리성: 계속 테이블을 조작할 필요는 없다
    - 보안성: 원하는 정보만 가져올 수 있다

- **그룹함수**

  - 종류
    - rollup: 인수가 2개가 다른 순서로 들어오면 다른 결과가 나온다.
      - rollup(A,B) != rollup(B,A) 계층구조로 진행되기 떄문이다.
    - cube
      - cube(A,B) == cube(B,A)
    - groupingsets
    - grouping
  - 어떤 그룹함수를 썼는지 찾는 문제가 나왔을 때
    1. null을 모두 찾는다
    2. 총합 행이 있는지 찾는다.
       1. 있다면?
          - rollup: 한 쪽만 결과가 나오며 계층형태 가진다. 행의 수 적음
          - cube: 양 쪽으로 둘 다 결과가 나옴. 행의 수 많음
       2. 없다면?
          - groupingsets

- TCL

  - 종류
    - commit
    - rollback
  - DDL의 커밋 기능 없애기
    - auto commit off and Begin transaction

- **윈도우 함수**

  - Rows/Range 결과값 차이점
    - 같은 값 유무 파악. range는 같은 값이 나올 확률이 있다.
  - rank/dense rank
    - rank는 중복건너뛴다.(후순위 건너뜀) 1,1,3,4등
    - dense rank는 건너뛰기 없음. 1,1,2,3등
  - partition by/order by 의미

- 계층형 질의

  - **prior 자식데이터 = 부모데이터**
    - prior은 연산자
    - 예시
      - level1 KING empno
        level 2 James mgr
        level 3 Scott
        -> 현재 James의 mgr이 KING의 empno이다.
        -> level2의 입장에서 prior 값은 level1.
        => **prior empno = mgr**
  - **부모 데이터에서 자식으로 가는 경우: 순방향**
  
- 절차형 PL/SQL

  - <u>Exception 생략 가능</u>
  - Procedure vs trigger vs userdefined function
    - Procedure는 반드시 값이 나오지 않는다
    - trigger는 commit, rollback 불가. DML 많이 쓴다
    - userdefined function는 반드시 값이 나온다

- 데이터모델링

  - 복잡한 현실세계(업무)를 데이터 모델화시킨다.
  - [참고]소프트웨어 개발 방법론
    1. 데이터 구조화론: 업무에만 집중한다. 절차도에 따른 프로그래밍
       	ex. 책 판다 - 돈 받는다 - 매출 상승.
    2. <u>관계형 데이터베이스</u>: 데이터 자체와 관계에 집중. 핵심적 정보를 연결지어 유기체적으로 모든 업무를 포괄할 수 있도록 함
       	ex. 프로세스가 다른 업무들도 진행하면 정보를 따로 쓰게된다. data 중복 & data quality  감소 -> 관계형 데이터 베이스 도입
    3. ~~객체지향 데이터베이스~~

- 엔티티

  - 업무 상 관리하고자하는 대상
  - 특징
    - 속성을 2개 이상 가져야 함
    - 관계는 1개 이상 가져야 한다
    - 업무에서 사용되어야 한다.  업무 프로세스에 이용되어야 한다
  - 분류
    - 유무형에 따른 분류
      - 유형
      - 개념
      - 사건
    - 발생시점에 따른 분류
      - 기본
      - 중심
      - 행위

- 속성

  - 관리하고자하는 대상인 인스턴스의 집합
  - 분류
    - 기본
    - 설계
    - 파생

- 도메인

  - 지정해줄 수 있는 것: 유형, 크기, 제약조건
  - 어떤 값을 가져야하나
  - 물리적 데이터 모델링 - check, primary key 등이 도메인에 해당

- 관계

  - IE 표기법
    - 표처럼 생김. 맨 위에는 pk를 써주고 나머지 일반 속성들은 그 아래에 써준다
    - 필수관계는 |, 선택관계는 o|로 표기한다.(상대 쪽에 표기함)
  - Barker 표기법
    - 둥근 박스를 쓰고, 식별자는 #, 나머지는 o으로 표기한다
    - 필수관계는 실선, 선택관계는 점선으로 표기(자신에게 표기)

- 식별자

  - 식별자/비식별자 관계

    |                        | 식별                                          | 비식별                           |
    | ---------------------- | --------------------------------------------- | -------------------------------- |
    | **관계**               | 강한 관계                                     | 약한 관계                        |
    | **단점**               | SQL 구분이 복잡해짐                           | 느리다.                          |
    | 단점 이유              | PK가 계속 상속해서 내려가므로 PK 속성 수 증가 | 불필요한 조인 관계가 많이 생겨서 |
    | 표기(ERD. IE에만 존재) | 실선                                          | 점선                             |

  - ERD 서술 특징

    - 시선 때문에 좌상 -> 우하로 움직여야 한다
    - 관계명 반드시 표기하지 않아도 된다
    - UML은 객체지향에서만 사용된다

  - 주식별자의 특징

    - 유일성: 인스턴스를 유일하게 구분
    - 최소성: 주식별자를 구성하는 속성의 수는 유일성을 만족하는 최소의 수가 되어야 함
    - 불변성: 지정된 주식별자의 값은 자주 변하지 않아야 함 (변하면 이전 기록 말소됨)
    - 존재성: NOT NULL 조건. 

    다 만족하면 후보키, 대표로 선정된 것이 PK이다. 
    PK + 대체키 = 후보키
