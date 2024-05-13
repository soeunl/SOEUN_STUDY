<Day37- 0510>
<Database 조인>

## 여러 테이블을 하나의 테이블처럼 사용하는 조인

❤️ 조인 (JOIN)

- 테이블간의 관계
- 공통적인 값을 가지고 테이블을 연결하는 방식
- SELECT \* FROM EMP, DEPT WHERE EMP.DEPTNO = DEPT.DEPTNO; -> 동등조인, 등가조인, 내부조인(INNER JOIN)
- 테이블간의 공통적인 값을 가지고 연결
- 테이블명이 동일하지 않아도 됨. 값만 동일하면 됨
- 외래키가 없어도 됨

1.  집합 연산자와 조인의 차이점

2.  여러 테이블을 사용할 때의 FROM절

    FROM 테이블명, 테이블명 ...

    카디젼 프로덕트, 데카르드 곱 : 무작위 순서쌍

    EMP : DEPTNO
    DEPT : DEPTNO
    -> 직원이 속해 있는 부서 정보

    EMP.DEPNO = DEPT.DEPTNO

3.  테이블의 별칭 설정

    FROM 테이블명 "별칭"
    테이블명 별칭

        큰 따옴표("")는 한 단어로 구성된 경우는 생략 가능, 여러 단어로 구성된 경우는(띄어쓰기가 있는 경우) 생략 불가

❤️ 조인 종류

1. 등가 조인 ( 동등 조인, 내부(INNER) 조인)

   - 공통적인 값의 일치 조건을 가지고 테이블을 결합하는 방식
   - 동등 조인, 내부(inner) 조인
   - 컬럼명 일치할 필요 없음, 행이랑 열 같을 필요 없음
   - 일치하는 값만 있으면 됨
   - 일치하지 않는 값은 나오지 않음
   - SELECT E.EMPNO, E.ENAME, D.DNAME, D.LOC
     FROM EMP E, DEPT D WHERE E.DEPTNO = D.DEPTNO;

2. 비등가 조인

   - 등가 조인이 아닌 조인, 암묵적 조인
   - 같은 값을 가지고 테이블간 조인 x
   - 값이 같음의 여부를 가지고 조인하는 것이 아님
   - 범위에 대한 조회를 할때 암묵적으로 테이블이 결합됨
   - 특정 값이 아닌 범위로 조인하는 것이라 암묵적이라고 하는 것임 (테이블간의 관련성이 있으면 조인 되는 방식)
   - SELECT \* FROM SALGRADE;
     SELECT \* FROM EMP;
     SELECT
     E.EMPNO , E.ENAME , E.SAL, S.\*
     FROM EMP E, SALGRADE S
     WHERE E.SAL BETWEEN S.LOSAL AND S.HISAL;

3. 자체 조인 (셀프조인)

   - 같은 테이블 내의 값을 사용하는 방식
   - SELECT
     E1.EMPNO, E1.ENAME,
     E2.MGR "관리자 직원번호",
     E2.ENAME 관리자명
     FROM EMP E1, EMP E2
     WHERE E1.MGR = E2.EMPNO;

4. 외부 조인 (OUTER조인)

   - 한쪽 테이블은 전체 모든 데이터 조회
   - 나머지 테이블은 공통적인 값이 있는 테이블만 추가적으로 조회
   - SELECT \* FROM EMP_JOIN;
     INSERT INTO EMP_JOIN (EMPNO, ENAME, JOB, DEPTNO)
     VALUES (9998, '이이름', 'CLERK', 50);
     INSERT INTO EMP_JOIN (EMPNO, ENAME, JOB)
     VALUES (9999, '김이름', 'CLERK');

   - SELECT \* FROM EMP_JOIN E, DEPT_JOIN D
     WHERE E.DEPTNO = D.DEPTNO(+);
     // EMP 테이블의 데이터는 전체 다 나오고, DEPT는 공통적인 것만 나온다. (왼쪽 외부 조인)

   - SELECT \* FROM EMP_JOIN E, DEPT_JOIN D
     WHERE E.DEPTNO(+) = D.DEPTNO;
     // DEPT 테이블의 데이터는 전체 다 나오고, EMP는 공통적인 것만 나온다. (오른쪽 외부 조인)

   - 주 정보는 다 나오고 추가 정보는 있으면 나오고 없으면 나오지 않음(+)로 표시

❤️ 조인(JOIN) 보강 내용

- 관계형 데이터베이스
- 데이터의 무결성을 위해 사용(통일성, 중복X)★★★
- 동일한 값을 가지고 특정 테이블을 찾는다.
- 데이터 중복 방지를 위해 사용
- 동일한 값이 있으면 사용 가능하다.
- 컬럼명이 달라도 조인이 가능하다.

❤️ SQL-99 표준 문법으로 배우는 조인

- 등가조인(INNER JOIN)

  1. NATUAL JOIN

  - 공통적인 값을 가진 컬럼명이 서로 동일, 1개만 있는 경우
  - 알아서 동일한 명칭이 있으면 JOIN 됨
  - 공통적인 이름의 컬럼이 단 1개일때
  - 조인하는 컬럼명이 동일하고 한개만 존재
  - SELECT \* FROM EMP;
    SELECT \* FROM DEPT;
    SELECT
    E.EMPNO, E.ENAME, E.JOB,
    D.DEPTNO, D.DNAME, D.LOC
    FROM EMP E NATURAL JOIN DEPT D; // DEPTNO 동일 컬럼

  2. [INNER]JOIN ~ USING

  - 공통적인 이름의 컬럼이 1개 이상일때
  - 공통적인 값을 가진 컬럼명이 서로 동일한 것이 1개 이상인 경우 -> 선택
  - USING(공통 컬럼)
  - SELECT \* FROM EMP;
    SELECT \* FROM DEPT;
    SELECT
    E.EMPNO, E.ENAME, E.JOB,
    D.DEPTNO, D.DNAME, D.LOC
    FROM EMP E NATURAL JOIN DEPT D;
    SELECT \* FROM EMP JOIN DEPT USING (DEPTNO); //JOIN앞에 INNER가 생략되어 있음

  3. [INNER]JOIN ~ ON

  - 값은 같지만 공통적인 이름의 컬럼이 없을 때
  - 공통적인 값을 가진 컬럼명이 서로 동일하지 않은 경우
  - SELECT \* FROM EMP E JOIN DEPT D ON E.DEPTNO = D.DEPTNO;

  4. OUTER JOIN

  - (1) 왼쪽 외부조인 (LEFT [OUTER] JOIN)
  - SELECT \*FROM EMP_JOIN E
    LEFT JOIN DEPT_JOIN D ON E.DEPTNO = D.DEPTNO;

  - (2) 오른쪽 외부조인 (RIGHT [OUTER] JOIN)
  - SELECT \* FROM EMP_JOIN E
    RIGHT JOIN DEPT_JOIN D ON E.DEPTNO = D.DEPTNO;

  - (3) FULL OUTER JOIN
  - (참고) MYSQL은 지원하지 X

  - SELECT \* FROM EMP_JOIN E
    FULL JOIN DEPT_JOIN D ON E.DEPTNO = D.DEPTNO;

  5. 세 개 이상의 테이블을 조인할 때

❤️ SQL

DDL - Date Definition Language : 데이터 정의어

- 데이터의 구조 정의하는 언어
- 실행하자마자 COMMIT이 바로 실행 -> 실행하자마자 바로 영구 반영

DML - Data Manipulation Language : 데이터 조작어

- INSERT, UPDATE, EDLETE, SELECT - DQL
- COMMIT, ROLLBACK이 적용될 수 있음
- 바로 COMMIT이 되지 않기 때문에 복구 가능
- COMMIT과 관련

DCL - Data Control Language : 데이터 제어어

- GRANT, REVOKE - COMMIT, ROLLBACK - TCL
