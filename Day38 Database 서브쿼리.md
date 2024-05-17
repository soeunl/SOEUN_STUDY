<Day38- 0513>
<Database 서브쿼리>

## SQL문 속 또 다른 SQL문, 서브 쿼리

❤️ 서브 쿼리

- 서브쿼리(subquery)는 SQL을 실행하는 데 필요한 데이터를 추가로 조회하기 위해 SQL문 내부에 사용하는 SELECT문을 의미
- 서브쿼리의 결과 값을 사용하여 기능을 수행하는 영역은 메인쿼리(main query)라고 부름
- 서브쿼리는 메인쿼리의 연산자와 함께 상호 작용하는 방식에 따라 크게 단일행 서브쿼리와 다중행 서브쿼리로 나뉨

```SQL
SELECT 조회할 열
	FROM 조회할 테이블
WHERE 조건식 ( SELECT 조회할 열 FROM 조회할 테이블 WHERE 조건식 )
```

1. 특징

(1) 서브 쿼리는 연산자와 같은 비교 또는 조회 대상의 오른쪽에 놓이며 괄호 ( )로 묶어서 사용함 (소괄호)

```SQL
SELECT \* FROM EMP
WHERE SAL <(SELECT MIN(SAL)FROM EMP WHERE DEPTNO =30)
```

(2) 특수한 몇몇 경우를 제외한 대부분의 서브쿼리에서는 ORDER BY 절을 사용할 수 없음
(3) 서브쿼리의 SELECT절에 명시한 열은 메인쿼리의 비교 대상과 같은 자료형과 같은 개수로 지정해야 함. 즉 메인쿼리의 비교 대상 데이터가 하나라면 서브쿼리의 SELECT절 역시 같은 자료형인 열을 하나 지정해야 함
(4) 서브쿼리에 있는 SELECT문의 결과 행 수는 함께 사용하는 메인쿼리의 연산자 종류와 호환 가능해야 함. 예를 들어 메인쿼리에 사용한 연산자가 단 하나의 데이터로만 연산이 가능한 연산자라면 서브쿼리의 결과 행 수는 반드시 하나여야 함
(5) 서브쿼리는 성능저하가 올 수 있어서 신중히 사용해야 함

❤️ 실행 결과가 하나인 단일행 서브 쿼리

1. 단일행 서브 쿼리(single-row subquery)는 실행 결과가 단 하나의 행으로 나오는 서브쿼리를 뜻함

2. 서브쿼리에서 출력되는 결과가 하나이므로 메인쿼리와 서브쿼리 결과는 단일행 연산자를 사용하여 비교함 - 비교연산자

3. 단일행 서브쿼리와 날짜형 데이터

- 단일행 서브쿼리는 서브쿼리 결과 값이 날짜(DATE) 자료형일 때도 사용할 수 있음

4. 단일행 서브쿼리와 함수
   (서브쿼리 안에서 함수를 사용한 경우)

```SQL
SELECT E.EMPNO, E.ENAME, E.JOB, E.SAL, D.DEPTNO, D.DNAME, D.LOC
FROM EMP E, DEPT D
WHERE E.DEPTNO = D.DEPTNO
	AND E.DEPTNO = 20
	AND E.SAL > (SELECT AVG(SAL) FROM EMP);
```

❤️ 실행 결과가 여러 개인 다중행 서브 쿼리

1. 다중행 서브쿼리(multiple-row subquery)는 실행 결과 행이 여러 개로 나오는 서브쿼리를 가리킴

2. 단일행 서브쿼리와 달리 서브쿼리 결과가 여러 개이므로 단일행 연산자는 사용할 수 없고 다중행 연산자를 사용해야 메인쿼리와 비교할 수 있음

3. IN 연산자 - 부서별 최대 급여 직원 목록

```SQL
SELECT * FROM EMP
WHERE SAL IN (SELECT MAX(SAL) FROM EMP GROUP BY DEPTNO);
```

4. ANY, SOME 연산자

- 쿼리 결과값이 하라나도 참이면 참 (Ex) 30번 부서의 최대 급여보다 적게 받는 직원 목록
- 서브쿼리 결과 값 중 하나만 조건식에 맞아떨어지면 메인쿼리의 조건식이 참이 되어 출력 대상이 됨

```SQL ANY
SELECT * FROM EMP
WHERE SAL = ANY (SELECT MAX(SAL) FROM EMP GROUP BY DEPTNO);
```

```SQL SOME
SELECT * FROM EMP
WHERE SAL = SOME (SELECT MAX(SAL) FROM EMP GROUP BY DEPTNO);
```

5. ALL 연산자

- 쿼리 결과값이 모두 참일때 참 (Ex) 30번 부서의 최대급여보다 많이 받는 직원 목록
- ALL 연산자는 서브쿼리의 모든 결과가 조건식에 맞아 떨어져야만 메인쿼리의 조건식이 true가 되는 연산자

6. EXISTS 연산자

- 서브쿼리의 레코드가 있으면 참, 없으면 거짓
- 서브쿼리에 결과 값이 하나 이상 존재하면 조건식이 true, 존재하지 않으면 모두 false가 되는 연산자
  (Ex) 30번 부서가 부서테이블에 목록하면 직원 목록을 출력

-- 30번 부서의 최소 급여보다 더 많이 받는 직원 목록
SELECT \* FROM EMP
WHERE SAL > (SELECT MIN(SAL) FROM EMP WHERE DEPTNO=30);

SELECT \* FROM EMP
WHERE SAL > ANY (SELECT SAL FROM EMP WHERE DEPTNO=30);

SELECT SAL FROM EMP WHERE DEPTNO=30 ORDER BY SAL DESC;

-- 30번 부서의 최소 급여보다 적게 받는 직원 목록
SELECT \* FROM EMP
WHERE SAL < (SELECT MAX(SAL) FROM EMP GROUP BY DEPTNO=30);

SELECT \* FROM EMP
WHERE SAL < ANY (SELECT SAL FROM EMP WHERE DEPTNO=30);

SELECT SAL FROM EMP WHERE DEPTNO=30 ORDER BY SAL DESC;

-- 30번 부서의 최대 급여보다 더 많이 받는 직원 목록
SELECT \* FROM EMP
WHERE SAL > (SELECT MAX(SAL) FROM EMP WHERE DEPTNO=30);

SELECT \* FROM EMP
WHERE SAL > ALL (SELECT SAL FROM EMP WHERE DEPTNO=30);

SELECT SAL FROM EMP WHERE DEPTNO=30 ORDER BY SAL DESC;

-- EXISTS 사용
SELECT \* FROM EMP
WHERE EXISTS (SELECT \* FROM DEPT WHERE DEPTNO = 30);

SELECT \* FROM EMP
WHERE EXISTS (SELECT \* FROM DEPT WHERE DEPTNO = 40);

SELECT \* FROM EMP
WHERE NOT EXISTS (SELECT \* FROM DEPT WHERE DEPTNO = 50);

❤️ 비교할 열이 여러 개인 다중열 서브쿼리

1. 서브쿼리의 SELECT절에 비교할 데이터를 여러 개 지정하는 방식

2. 다중열 서브쿼리 사용하기

```SQL
SELECT * FROM EMP
WHERE (DEPTNO, SAL) IN (SELECT DEPTNO, MAX(SAL) FROM EMP GROUP BY DEPTNO);
```

❤️ FROM절에 사용하는 서브쿼리와 WITH절

1. 인라인 뷰(inline view)
   : 가상 테이블, 서브 쿼리 결과를 가지고 가상 테이블 생성
   : FROM절에 사용하는 서브쿼리는 인라인 뷰(inline view)라고 부름
   : 인라인 뷰는 특정 테이블 전체 데이터가 아닌 SELECT문을 통해 일부 데이터를 먼저 추출해 온 후 별칭을 주어 사용할 수 있음

```SQL
   SELECT \* EMPNO, ENAME, D.DNAME
   FROM(SELECT EMPNO, ENAME, JOB, SAL, DEPTNO
   FROM EMP WHERE DEPTNO IN (10, 20)) E,
   (SELECT \* FROM DEPT) D
   WHERE E.DEPTNO = D.DEPTNO AND E.SAL >= 2000;
```

2. WITH절 사용하기

```SQL
[별칭1] AS (SELECT문 1),
[별칭2] AS (SELECT문 2),
...
[별칭n] AS (SELECT문 n)
SELECT FROM 별칭1, 별칭2, 별칭3 ...
```

```SQL
   WITH
   E AS (SELECT EMPNO, ENAME, JOB, SAL, DEPTNO
   FROM EMP WHERE DEPTNO IN (10, 20)),
   D AS (SELECT \* FROM DEPT)
   SELECT E.EMPNO, E.ENAME, D.DNAME
   FROM E,D
   WHERE E.DEPTNO = D.DEPTNO AND E.SAL >= 2000;
```

3. 상호 연관 서브쿼리
   : 메인 쿼리의 결과 데이터를 서브 쿼리에서 사용
   : 메인쿼리에 사용한 데이터를 서브쿼리에서 사용하고 서브쿼리의 결과 값을 다시 메인쿼리로 돌려주는 방식인 상호연관 서브쿼리(correlated subquery)

```SQL
   SELECT \* FROM EMP E1
   WHERE
   SAL > (SELECT MIN(SAL) FROM EMP E2 WHERE E1.DEPTNO = E2.DEPTNO);
```

❤️ SELECT 절에 사용하는 서브쿼리

1. 스칼라 서브쿼리(scalar subquery)
   스칼라 : 단일값, 단일행 서브쿼리
   SELECT절에 하나의 열 영역으로 결과를 출력할 수 있음
2. SELECT절에 서브쿼리 사용하기

```SQL
   SELECT EMPNO, ENAME,
   (SELECT DNAME FROM DEPT D WHERE D.DEPTNO = E.DEPTNO) DNAME,
   FROM EMP E;
```

3. SELECT 절에 명시하는 서브쿼리는 반드시 하나의 결과만 반환하도록 작성!
