<Day34 - 0507>
<Database SELECT문의 기본 형식>

## SELECT 문의 기본 형식

❤️ 실습용 테이블 살펴보기

1. EMP 테이블 -사원정보
2. DEPT 테이블 - 회사 부서 정보
3. SALGRADE 테이블 - 급여등급

❤️ 데이터를 조회하는 3가지 방법

1. 셀렉션 : 행 단위로 원하는 데이터를 조회하는 방식
2. 프로젝션 : 열 단위로 데이터를 조회하는 방식
3. 행과 열을 모두 선별할 경우 셀렉션과 프로젝션을 함께 사용할 수 있음
4. 조인 : 다른 테이블의 데이터를 공통적인 컬럼의 값을 통해 연결하여 조회하는 방식

(참고)
DML (Data Manipulation Language) : 데이터 조작어 - INSERT, UPDATE, DELETE
DQL (Data QUery Language) : 데이터 질의어 - SELECT : 쿼리

❤️ SQL의 기본 뼈대, SELECT절과 FROM 절

1. 형식
   - SELECT 조회할 컬럼1, 컬럼2 ... FROM 테이블명;
   - 모든 컬럼 : \*
2. SELECT
3. FROM

❤️ 중복 데이터를 삭제하는 DISTINCT
SELECT [ALL|DISTINCT] 조회할 컬럼1, 컬럼2 ... FROM 테이블명;

1. ALL : 기본값 - 따로 작성하지 않아도 ALL이 포함된 형태임 - 중복이 되어도 다 나온다.
2. DISTINCT : 중복을 제거하고 조회

❤️ 한눈에 보기 좋게 별칭 설정하기

1. 실습1

- 열에 연산식을 사용하여 출력하기
- 별칭을 지정하는 방식

2. 실습2

원하는 순서로 출력 데이터를 정렬하는 ORDER BY

1. 실습
2. 주의 사항

05 더 정확하고 다양하게 결과를 출력하는 WHERE절과 연산자

필요한 데이터만 쏙 출력하는 WHERE절

1. 문법
2. 실습

여러 개 조건식을 사용하는 AND, OR 연산자

1. AND 연산자
2. OR 연산자

연산자 종류와 활용 방법 알아보기

1. 산술 연산자
2. 비교 연산자
3. 등가 비교 연산자
4. 논리 부정 연산자
5. IN 연산자
6. BETWEEN A AND B 연산자
7. LIKE 연산자와 와일드 카드

   1. 문법
   2. -, %
   3. 와일드 카드 문자가 데이터의 일부일 경우 - ESCAPE 절 사용

8. IS NULL 연산자
9. 집합 연산자

1) UNION
2) UNION ALL
3) MINUS
4) INSERSECT
