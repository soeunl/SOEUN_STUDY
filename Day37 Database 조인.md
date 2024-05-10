<Day37- 0510>
<Database 조인>

## 여러 테이블을 하나의 테이블처럼 사용하는 조인

❤️ 조인

- 공통적인 값을 가지고 테이블을 연결하는 방식
- SELECT \* FROM EMP, DEPT WHERE EMP.DEPTNO = DEPT.DEPTNO; -- 동등조인, 등가조인, 내부조인

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

1. 등가 조인

   - 공통적인 값의 일치 조건을 가지고 테이블을 결합하는 방식
   - 동등 조인, 내부(inner) 조인
   - SELECT E.EMPNO, E.ENAME, D.DNAME, D.LOC
     FROM EMP E, DEPT D WHERE E.DEPTNO = D.DEPTNO;

2. 비등가 조인

   - 등가 조인이 아닌 조인, 암묵적 조인
   - 같은 값을 가지고 테이블간 조인 x
   - 범위에 대한 조회를 할때 암묵적으로 테이블이 결합됨
   - SELECT \* FROM SALGRADE;
     SELECT \* FROM EMP;
     SELECT
     E.EMPNO , E.ENAME , E.SAL, S.\*
     FROM EMP E, SALGRADE S
     WHERE E.SAL BETWEEN S.LOSAL AND S.HISAL;

3. 자체 조인

   - 같은 테이블 내의 값을 사용하는 방식
   - SELECT
     E1.EMPNO, E1.ENAME,
     E2.MGR "관리자 직원번호",
     E2.ENAME 관리자명
     FROM EMP E1, EMP E2
     WHERE E1.MGR = E2.EMPNO;

4. 외부 조인

   - 한쪽 테이블은 전체 모든 데이터 조회
   - 나머지 테이블은 공통적인 값이 있는 테이블만 추가적
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

❤️ SQL-99 표준 문법으로 배우는 조인

- 등가조인(INNER JOIN)

  1. NATUAL JOIN

  - 알아서 동일한 명칭이 있으면 JOIN 됨
  - 공통적인 이름의 컬럼이 단 1개일때
  - SELECT \* FROM EMP;
    SELECT \* FROM DEPT;
    SELECT
    E.EMPNO, E.ENAME, E.JOB,
    D.DEPTNO, D.DNAME, D.LOC
    FROM EMP E NATURAL JOIN DEPT D; // DEPTNO 동일 컬럼

  2. JOIN ~ USING

  - 공통적인 이름의 컬럼이 1개 이상일때 
  - USING(공통 컬럼)
  - SELECT \* FROM EMP;
    SELECT \* FROM DEPT;
    SELECT
    E.EMPNO, E.ENAME, E.JOB,
    D.DEPTNO, D.DNAME, D.LOC
    FROM EMP E NATURAL JOIN DEPT D;
    SELECT * FROM EMP JOIN DEPT USING (DEPTNO); //JOIN앞에 INNER가 생략되어 있음

  3. JOIN ~ ON

  4. OUTER JOIN

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

## SQL문 속 또 다른 SQL문, 서브 쿼리

❤️ 서브 쿼리

1. 특징

1) 서브 쿼리는 연산자와 같은 비교 또는 조회 대상의 오른쪽에 놓이며 괄호 ( )로 묶어서 사용합니다.
2) 특수한 몇몇 경우를 제외한 대부분의 서브쿼리에서는 ORDER BY 절을 사용할 수 없습니다.
3) 서브쿼리의 SELECT절에 명시한 열은 메인쿼리의 비교 대상과 같은 자료형과 같은 개수로 지정해야 합니다. 즉 메인쿼리의 비교 대상 데이터가 하나라면 서브쿼리의 SELECT절 역시 같은 자료형인 열을 하나 지정해야 합니다.
4) 서브쿼리에 있는 SELECT문의 결과 행 수는 함께 사용하는 메인쿼리의 연산자 종류와 호환 가능해야 합니다. 예를 들어 메인쿼리에 사용한 연산자가 단 하나의 데이터로만 연산이 가능한 연산자라면 서브쿼리의 결과 행 수는 반드시 하나여야 합니다.

## 실행 결과가 하나인 단일행 서브 쿼리

1. 단일행 서브 쿼리(single-row subquery)는 실행 결과가 단 하나의 행으로 나오는 서브쿼리를 뜻합니다.
2. 서브쿼리에서 출력되는 결과가 하나이므로 메인쿼리와 서브쿼리 결과는 다음과 같이 단일행 연산자를 사용하여 비교
3. 단일행 서브쿼리와 날짜형 데이터
4. 단일행 서브쿼리와 함수

실행 결과가 여러 개인 다중행 서브 쿼리

1. 다중행 서브쿼리(multiple-row subquery)는 실행 결과 행이 여러 개로 나오는 서브쿼리를 가리킵니다.
2. 단일행 서브쿼리와 달리 서브쿼리 결과가 여러 개이므로 단일행 연산자는 사용할 수 없고 다중행 연산자를 사용해야 메인쿼리와 비교할 수 있습니다.
3. IN 연산자
4. ANY, SOME 연산자
5. ALL 연산자
6. EXISTS 연산자

비교할 열이 여러 개인 다중열 서브쿼리

1. 서브쿼리의 SELECT절에 비교할 데이터를 여러 개 지정하는 방식
2. 다중열 서브쿼리 사용하기

FROM절에 사용하는 서브쿼리와 WITH절

1. 인라인 뷰(inline view)
2. WITH절 사용하기
3. 상호 연관 서브쿼리

SELECT 절에 사용하는 서브쿼리

1. 스칼라 서브쿼리(scalar subquery)
2. SELECT절에 서브쿼리 사용하기
3. SELECT 절에 명시하는 서브쿼리는 반드시 하나의 결과만 반환하도록 작성
