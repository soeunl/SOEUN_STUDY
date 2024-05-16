<Day39- 0514>
<Database 객체 종류>

## 객체 종류

❤️ 데이터베이스를 위한 데이터를 저장한 데이터 사전

1. 데이터 사전이란?
   DICTIONARY 테이블
   동의어 DICT

   (1) 데이터베이스를 구상하고 운영하는 데 필요한 모든 정보를 저장하는 특수한 테이블
   (2) 데이터베이스가 생성되는 시점에 자동으로 만들어짐

2. 접두어

   (1) USER_XXXX - 현재 데이터베이스에 접속한 🤍사용자가 소유한 객체 정보
   (2) ALL_XXXX - 사용 가능한 🤍모든 객체 정보
   (3) DBA_XXXX - 데이터베이스 🤍관리를 위한 정보(데이터베이스 관리 권한을 가진 SYSTEM, SYS 사용자만 열람 가능)
   (4) V$_XXXX - 데이터베이스 🤍성능 관련 정보(X$\_XXXX 테이블의 뷰)

3. 요약

   (1) 데이터 사전은 오라클 데이터베이스를 구성하고 운영하는 데이터를 저장하는 특수한 테이블로서 오라클 사용자가 직접 접근할 수 없습니다.
   (2) SELECT문으로 데이터를 명령할 수 있도록 데이터 사전 뷰를 제공
   (3) 대표적인 데이터 사전 뷰 중 현재 접속한 사용자가 소유하는 테이블 목록을 보기 위해서는 USER_TABLES를 사용
   (4) 사용자가 소유하는 테이블을 포함해 다른 사용자가 소유한 테이블 중 현재 사용자에게 사용 허가가 되어 있는 테이블을 보기 위해서는 ALL_TABLES를 사용

❤️ 더 빠른 검색을 위한 인덱스

1. 인덱스란?
   INDEX : 목차 -> 빠르게 찾기 위한 물리적 주소
   검색이 많이 되는 항목에 인덱스 부여
   정렬이 필요한 항목에도 인덱스 부여

   (1) 색인이라는 뜻의 인덱스(index)
   (2) 책 내용을 찾는 것과 마찬가지로 오라클 데이터베이스에서 데이터 검색 성능 향상을 위해 테이블 열에 사용하는 객체를 뜻
   (3) 인덱스 사용 여부에 따라 데이터 검색 방식을 Table Full Scan, Index Scan으로 구분합니다.
   -Table Full Scan : 처음부터 끝까지 검색하여 원하는 데이터를 찾는 방식
   -Index Scan : 인덱스를 통해 데이터를 찾는 방식
   (4) SCOTT 계정이 소유한 인덱스 정보 알아보기(SCOTT 계정일 때)
   (5) SCOTT 계정이 소유한 인덱스 컬럼 정보 알아보기
   (6) 인덱스는 사용자가 직접 특정 테이블의 열에 지정할 수도 있지만 열이 기본키(primary key) 또는 고유키(unique key)일 경우에 자동으로 생성합니다.

❤️ 인덱스 생성

1. 사용법
   CREATE INDEX 인덱스명 ON 테이블명(컬럼명[ASC|DESC, 컬럼명... 오름차순이 기본 정렬방향])
2. EMP 테이블의 SAL열에 인덱스를 생성하기
3. 생성된 인덱스 살펴보기(USER_IND_COLUMNS 사용)

❤️ 인덱스 삭제

1. 사용법

(참고)

1. 인덱스 생성이 항상 좋은 결과로 이어지지는 않음. 정확한 데이터 분석에 기반을 두지 않는 인덱스의 무분별한 생성은 오히려 성능을 떨어트리는 원인이 되기도 함
2. 인덱스는 데이터 종류, 분포도, 조회하는 SQL의 구성, 데이터 조작 관련 SQL문의 작업 빈도, 검색 결과가 전체 데이터에서 차지하는 비중 등 많은 요소를 고려하여 생성함
3. 선택도가 낮을 수록 인덱스 적용이 좋고 선택도가 높을 수록 인덱스는 불리함

남, 여 50% -> 인덱스가 적합하지 않음

❤️ 테이블처럼 사용하는 뷰

1. 뷰란?

- 가상테이블(virtual table)로 부르는 뷰(view)는 하나 이상의 테이블을 조회하는 SELECT 문을 저장한 객체를 뜻

2. 뷰의 사용 목적(편리성)

   (1) 편리성 : SELECT문의 복잡도를 완화하기 위해
   (2) 보안성 : 테이블의 특정 열을 노출하고 싶지 않을 경우

3. 뷰 생성
   CREATE VIEW 뷰 명칭 AS SELECT 문;

```SQL
CREATE OR REPLACE VIEW VW_EMP
AS (SELECT E.EMPNO, E.ENAME, E.JOB, E.SAL, D.*, S.*
		FROM EMP E
			JOIN DEPT D ON E.DEPTNO = D.DEPTNO
			JOIN SALGRADE S ON E.SAL BETWEEN S.LOSAL AND S.HISAL
		WHERE E.DEPTNO IN (10, 20));

SELECT * FROM USER_VIEWS;

SELECT * FROM VW_EMP WHERE DEPTNO IN (10, 20);
// 하나의 가상의 테이블만 접근
```

(1) 권한부여
CREATE [OR REPLACE] VIEW : 뷰가 없으면 생성, 있으면 교체

SYSTEM 계정
GRANT CREATE VIEW TO SCOTT;

(2) 뷰 생성하기

(3) 생성한 뷰 확인하기
USER_VIEWS 사전

(4) 생성한 뷰 조회하기

(5) 뷰 삭제
DROP VIEW 뷰이름;

- 뷰는 실제 데이터가 아닌 데이터가 아닌 SELECT문만 저장하므로 뷰를 삭제해도 테이블이나 데이터가 삭제되는 것은 아님
- 편리성과 보안성이 뷰 사용의 목적임

❤️ 인라인 뷰를 사용한 TOP-N SQL문

1. 인라인 뷰(서브쿼리 사용)
2. 인라인 뷰(WITH절 사용)

ROWNUM : 레코드 순번 (모든 테이블마다 다 있다)

```SQL
SELECT ROWNUM, E. * FROM EMP E ORDER BY SAL DESC;

SELECT ROWNUM, E. * FROM (SELECT * FROM EMP ORDER BY SAL DESC) E
WHERE ROWNUM <= 3;
```

❤️ 규칙에 따라 순번을 생성하는 시퀀스

1. 시퀀스란?

   (1) 오라클 데이터베이스에서 특정 규칙에 맞는 연속 숫자를 생성하는 객체 - 회원번호, 게시글 번호, 주문번호

2. 시퀀스 생성

   (1) 사용법

   - 권한부여
     CREATE SEQUENCE 권한 부여 필요

     GRANT 권한 TO 사용자/스키마;

     GRAEATE SEQUENCE 시퀀이름
     INCREMENT BY 숫자 - 숫자씩 증가
     START WITH 숫자 - 숫자에서 부터 증가 시작
     MAXVALUE 숫자 - 최대 숫자 만큼 증가
     MINVALUE 숫자 - 최소 숫자 부터 시작
     CYCLE(최대 숫자 도달 시 다음 숫자는 MINVALUE 부터 시작) | NOCYCLE (기본값- 최대 숫자에 도달하면 오류 발생)

     CACHE 숫자 - 기본값(CACHE 20 -> 20개의 숫자를 미리 생성해 놓는다.) | NOCACHE

     ALTER SEQUENCE 시퀀스 이름; -> 시퀀스에 대한 변경을 할 때 사용

     DROP SEQUENCE 시퀀스 이름;

   (2) DEPT 테이블을 사용하여 DEPT_SEQUENCE 테이블 생성하기
   (3) DEPT_SEQUENCE 테이블에 DEPTNO가 10씩 증가할 수 있는 시퀀스 생성
   (4) 시퀀스 생성을 확인
   USER_SEQUENCE 사전 테이블

3. 시퀀스 사용

   (1) [시퀀스 이름.CURRVAL]과 [시퀀스 이름.NEXTVAL★★★]을 사용
   (2) CURRVAL은 시퀀스에서 마지막으로 생성한 번호를 반환
   (3) NEXTVAL는 다음 번호를 생성
   -> 시퀀스 객체.NEXTVAL★★★ -> 숫자 증가 -> 값 반환

4. 시퀀스 수정
5. 시퀀스 삭제

❤️ 공식 별칭을 지정하는 동의어

1. 동의어란?

   (1) 테이블-뷰-시퀀스 등 객체 이름 대신 사용할 수 있는 다른 이름을 부여하는 객체
   (2) 테이블 이름이 너무 길어 사용이 불편할 때 좀 더 간단하고 짧은 이름을 하나 더 만들어 주기 위해 사용함

   사전 테이블 DICTIONARY의 동의어 DICT

2. 사용법

3. 권한 부여하기(SQL\*PLUS)
   CREATE SYNONYM : 현재 사용자에서만 동의어 사용 가능
   CREATE PUBLIC SYNONYM : 모든 사용자에게 동의어 공유
   GRANT CREATE PUBLIC SYNONYM, CREATE SYNONTM TO SCOTT;

4. 동의어 생성
   CREATE SYNONYM 동의어 명칭 FOR 대상 테이블 또는 뷰;

5. 동의어 삭제
   DROP SYNONYM 동의어 명칭;
