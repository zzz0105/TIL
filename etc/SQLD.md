# SQLD

## SQL 명령문

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