<Day36 - 0509>
<Database 다중행 함수와 데이터 그룹화>

## 하나의 열에 출력 결과를 담는 다중행 함수

❤️ 다중행 함수와 데이터 그룹화

🤍 하나의 열에 출력 결과를 담는 다중행 함수

- 단일행 함수는 각각의 행 하나하나마다 적용되는 함수 / 행 하나하나에 반영
  SELECT EMPNO, REPLACE(ENAME, 'A', '\*') ENAME FROM EMP;
- 다중행 함수는 여러 행의 값을 모두 쓰고 결과를 만들어 내는 함수
  SELECT SUM(SAL) FROM EMP;

- 여러 행을 바탕으로 하나의 결과 값을 도출해 내기 위해 사용하는 함수
- SUM 함수를 사용하여 급여 합계 출력하기
- SUM 함수를 사용하여 사원 이름과 급여 합계 출력하기(오류 발생)
- 자주 사용하는 다중행 함수
- 거의 대부분 통계 관련 함수 : 집계함수

1. 합계를 구하는 SUM 함수

- 데이터의 합을 구하는 함수
- 추가 수당 합계 구하기
- 레코드 갯수가 맞지 않으면 오류가 남
- SUM 함수와 DISTINCT, ALL 함께 사용하기
- ALL : 모든 값(기본값)
- DISTINCT : 유일한값

SELECT SUM(SAL), SUM(DISTINCT) FROM EMP;

2. 데이터 개수를 구해 주는 COUNT 함수

- 데이터 개수를 출력하는 데 사용
- NULL이 데이터로 포함되어 있을 경우, NULL 데이터는 반환 갯수에서 제외

SELECT COUNT(JOB), COUNT(DISTINCT JOB), COUNT(COMM),
COUNT(\*)
FROM EMP;

(참고)
전체 데이터 갯수 : COUNT(\*)

3. 최댓값과 최솟값을 구하는 MAX, MIN 함수
   MAX(..) : 최댓값
   MIN(..) : 최솟값

- 부서 번호가 10번인 사원들의 최대 급여 출력하기
- 부서 번호가 10번인 사원들의 최소 급여 출력하기
- 부서 번호가 20인 사원의 입사일 중 제일 최근 입사일 출력하기 - MAX
- 부서 번호가 20인 사원의 일사일 중 제일 오래된 입사일 출력하기 - MIN

SELECT MAX(HIREDATE), MIN(HIREDATE) FROM EMP;

4. 평균 값을 구하는 AVG 함수

- 부서 번호가 30인 사원들의 평균 급여 출력하기
- DISTINCT로 중복을 제거한 급여 열의 평균 급여 구하기

SELECT AVG(SAL), AVG(DISTINCT SAL) FROM EMP;

🤍 결과 값을 원하는 열로 묶어 출력하는 GROUP BY절

- 집합 연산자를 사용하여 각 부서별 평균 급여 출력하기

SELECT DEPTNO, JOB, ROUND(AVG(SAL)) 평균급여 FROM EMP GROUP BY DEPTNO, JOB;
(어떤 부서의 어떤 직책의 급여 평균이 얼마인지 계산)

SELECT DEPTNO, ROUND (AVG(SAL)) FROM EMP GROUP BY DEPTNO;
(각 부서별 급여의 평균 계산)

1. GROUP BY 절의 기본 사용법

- 여러 데이터에서 의미 있는 하나의 결과를 특정 열 값으로 묶어서 출력할 때 데이터를 '그룹화' 한다고 표현

- 문법
- GROUP BY절에 명시하는 열은 여러 개 지정할 수 있음
- GROUP BY를 사용하여 부서별 평균 급여 출력하기
- 부서 번호 및 직책별 평균 급여로 정렬하기

2. GROUP BY절을 사용할 때 유의점

- 다중행 함수를 사용하지 않은 일반 열은 GROUP BY절에 명시하지 않으면 SELECT 절에서 사용할 수 없다는 것
- GROUP BY절에 없는 열은 SELECT절에 포함할 수 없음
- 레코드와 기준에 맞지 않는 열에는 사용이 불가 (예) 사원 이름

🤍 GROUP BY절에 조건을 줄 때 사용하는 HAVING절

1. HAVING 절은 SELECT문에 GROUP BY절이 존재할 때만 사용할 수 있음
2. GROUP BY절을 통해 그룹화된 결과 값의 범위를 제한하는 데 사용
3. GROUP BY 절과 HAVING절을 사용하여 출력하기

- HAVING절의 기본 사용법
  SELECT DEPTNO, JOB, ROUND (AVG(SAL))
  FROM EMP
  GROUP BY DEPTNO, JOB
  HAVING AVG(SAL) <= 1000;

  SELECT DEPTNO, JOB, ROUND (AVG(SAL))
  FROM EMP
  WHERE DEPTNO IN (10, 20)
  GROUP BY DEPTNO, JOB
  HAVING AVG(SAL) <= 1000;

  SELECT DEPTNO, JOB, ROUND (AVG(SAL))
  FROM EMP
  GROUP BY DEPTNO, JOB
  HAVING AVG(SAL) >= 1000 AND AVG(SAL) <= 3000;

- HAVING절을 사용할 때 유의점
  ① WHERE절은 출력 대상 행을 제한하고, HAVING절은 그룹화된 대상을 출력에서 제한 (HAVING 절은 집계 함수만 사용 가능)
  ② HAVING절 대신 WHERE절을 잘못 사용했을 경우

🤍 그룹화와 관련된 여러 함수

1. ROLLUP 함수를 적용한 그룹화
   오라클에만 있는 통계함수
   중간중간 요약정보가 나옴

   SELECT DEPTNO, JOB,
   SUM(SAL) 합계,
   ROUND(AVG(SAL)) 평균,
   MAX(SAL) 최대급여,
   MIN(SAL) 최소급여,
   COUNT(\*) 직원수
   FROM EMP GROUP BY ROLLUP(DEPTNO , JOB) ORDER BY DEPTNO, JOB;

2. CUBE 함수를 적용한 그룹화
   ROLLUP보다 통계가 더 많이 나옴
   모든 가능한 조합별로 통계를 내줌

   SELECT DEPTNO, JOB,
   SUM(SAL) 합계,
   ROUND(AVG(SAL)) 평균,
   MAX(SAL) 최대급여,
   MIN(SAL) 최소급여,
   COUNT(\*) 직원수
   FROM EMP GROUP BY CUBE(DEPTNO , JOB) ORDER BY DEPTNO, JOB;
