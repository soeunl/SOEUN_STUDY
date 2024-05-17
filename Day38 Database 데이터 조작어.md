<Day38- 0513>
<Database 데이터 조작어>

## 데이터를 추가, 수정, 삭제하는 데이터 조작어

❤️ 테이블에 데이터 추가하기

🤍INSERT : 추가
🤍UPDATE : 수정
🤍DELETE : 삭제

1. 테이블 생성하기
   CREATE TABLE 테이블명 AS SELECT...

   (참고) DDL
   CTEATE 대상 - 생성
   ALTER 대상 - 수정
   DROP 대상 - 삭제
   DDL은 실행과 동시에 COMMIT 진행, 데이터 바로 반영, ROLLBACK 불가

   (참고2)
   DML은 COMMIT하면 영구 반영 된다. DML만 가능. COMMIT 전에는 ROLLBACK이 가능

2. 문법
   INSERT INTO 테이블명 (컬럼1, 컬럼2, ...) VALUES (값1, 값2...);
   INSERT INTO DEPT_TEMP (DEPTNO, DNAME, LOC)
   VALUES (50, 'WEB', 'SEOUL');

   - (컬럼1, 컬럼2,...) : 전체 데이터를 추가하는 상황, 컬럼의 순서가 동일한 경우 생략 가능
     INSERT INTO DEPT_TEMP VALUES (60, 'DATABASE', 'INCHEON');
   - 값 : 문자 -> '값'
   - 숫자 - 값

❤️ 테이블에 NULL 테이터 입력하기

- INSERT문으로 새로운 데이터를 추가할 때 특정 열에 들어갈 데이터가 확정되지 않았거나 굳이 넣을 필요가 없는 데이터인 경우에 NULL을 사용
- NULL을 INSERT문에 지정하는 방법은 NULL을 직접 명시적으로 입력해 주는 방법과 대상 열을 생략하여 암시적으로 NULL이 입력되도록 유도하는 방식이 있음

- NULL을 지정하여 입력하기
```SQL
INSERT INTO DEPT_TEMP (DEPTNO, DNAME, LOC) VALUES (70, 'WEB', NULL);

SELECT * FROM DEPT_TEMP;
```

- 빈 공백 문자열로 NULL을 입력하기
```SQL
INSERT INTO DEPT_TEMP (DEPTNO, DNAME, LOC) VALUES (80, 'MOBILE', '');

SELECT * FROM DEPT_TEMP;
```

- 열 데이터를 넣지 않는 방식으로 NULL 데이터 입력하기
```SQL
INSERT INTO DEPT_TEMP (DEPTNO, LOC) VALUES (90, 'INCHEON');

SELECT * FROM DEPT_TEMP;
```

- (참고) MYSQL : 비어있는 문자열 데이터
- (참고) 특정 필드가 비어 있는지 체크? 필드명 <> ''AND 필드명 IN NOT NULL;

❤️ 테이블에 날짜 데이터 입력하기

- 년/월/일 순서와 반대로 일/월/년 순서로 데이터를 입력하면 오류가 발생

- INSERT문으로 날짜 데이터 입력하기(날짜 사이에 / 입력)
```SQL
INSERT INTO EMP_TEMP (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO) 
	VALUES (1111, '성춘향', 'MANAGER', 9999, '2001/01/05', 4000, NULL, 20);

SELECT * FROM EMP_TEMP;
```

- INSERT문으로 날짜 데이터 입력하기(날짜 사이에 - 입력)
```SQL
INSERT INTO EMP_TEMP (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO) 
	VALUES (1111, '성춘향', 'MANAGER', 9999, '2001-01-05', 4000, NULL, 20);

SELECT * FROM EMP_TEMP;
```

- TO_DATE 함수를 사용하여 날짜 데이터 입력하기
```SQL
INSERT INTO EMP_TEMP (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
	VALUES (2111, '이순신', 'MANAGER', 9999, TO_DATE('07/01/2001', 'DD/MM/YYYY'), 4000, NULL, 20);
	
SELECT * FROM EMP_TEMP;
```

- SYSDATE를 사용하여 날짜 데이터 입력하기 (현재 시점으로 날짜를 입력할 경우에는 SYSDATE를 지정하여 간단히 처리할 수 있음)
```SQL
INSERT INTO EMP_TEMP (EMPNO, ENAME, JOB, MGR, HIREDATE, SAL, COMM, DEPTNO)
	VALUES (3111, '심청이', 'MANAGER', 9999, SYSDATE, 4000, NULL, 30);
	
SELECT * FROM EMP_TEMP;
```

(참고) 자료형 변환 함수

- TO_NUMBER(..) : 형식화된 문자열 숫자 -> 숫자
- TO_DATE(..) : 형식화된 문자열 날짜 -> 날짜
- TO_CHAR(..) : 숫자, 문자 -> 형식화된 문자열

❤️ 서브 쿼리를 사용하여 한 번에 여러 데이터 추가하기

1. 서브 쿼리로 여러 데이터 추가하기
  
   - 테이블이 이미 있는 경우, 데이터만 일괄 추가 /서브쿼리 형태/ 컬럼명 등이 일치해야함
   ```SQL
   INSERT INTO DEPT_TEMP2 (SELECT \* FROM DEPT);
   ```

2. INSERT문에서 서브쿼리를 사용할 때 유의할 점
   - VALUES 절은 사용하지 않음
   - 데이터가 추가되는 테이블의 열 개수와 서브쿼리의 열 개수가 일치해야 함
   - 데이터가 추가되는 테이블의 자료형과 서브쿼리의 자료형이 일치해야 함

❤️ 테이블에 있는 데이터 수정하기

- 특정 테이블에 저장되어 있는 데이터 내용을 수정할 때 UPDATE문을 사용

1. UPDATE 문의 기본 사용법
```SQL
UPDATE [변경할 테이블] - (1)
SET    [변경할 열1]=[데이터], [변경할 열2]=[데이터], ... , [변경할 열n]=[데이터] - (2)
WHERE [데이터를 변경할 대상 행을 선별하기 위한 조건]; - (3)
```
2. 데이터 전체 수정하기
   (참고) ROLLBACK
3. 데이터 일부분 수정하기
```SQL
UPDATE DEPT_TEMP2
	SET DNAME = 'DATABASE', 
	     LOC = 'SEOUL'
WHERE DEPTNO = 40;

SELECT * FROM DEPT_TEMP2;
```

❤️ 서브쿼리를 사용하여 데이터 수정하기

1. 서브쿼리로 데이터 일부분 수정하기
```SQL
UPDATE DEPT_TEMP2
	SET (DNAME, LOC) = (SELECT DNAME, LOC FROM DEPT WHERE DEPTNO = 40)
WHERE DEPTNO = 40;

SELECT * FROM DEPT_TEMP2;
```
2. 열 하나하나를 수정하는 경우
```SQL
UPDATE DEPT_TEMP2
	SET DNAME = (SELECT DNAME FROM DEPT WHERE DEPTNO = 40),
	     LOC = (SELECT LOC FROM DEPT WHERE DEPTNO = 40)
WHERE DEPTNO = 40;

SELECT * FROM DEPT_TEMP2;
```

3. UPDATE문의 WHERE절에 서브쿼리 사용하기
```SQL
UPDATE DEPT_TEMP2
	SET LOC = 'SEOUL'
WHERE DEPTNO = (SELECT DEPTNO FROM DEPT_TEMP2 WHERE DNAME='OPERATIONS');

SELECT * FROM DEPT_TEMP2;
```

❤️ 테이블에 있는 데이터 삭제하기

1. DELETE문의 기본 형식
```SQL
DELETE [FROM] [테이블 이름] - (1)
WHERE [삭제할 대상 행을 선별하기 위한 조건식]; - (2)
```
   - DELECT FROM 테이블명 WHERE 조건식;
   - DELETE FROM 또는 DELETE 키워드 뒤에 데이터를 삭제할 대상 테이블 이름을 지정
   - 삭제 대상이 될 데이터를 선정하기 위해 WHERE절 및 조건식을 지정할 수 있음
   - DELETE문에서 WHERE절을 사용하지 않으면 테이블 전체 데이터가 삭제되므로 주의

2. WHERE절을 사용하여 데이터 일부분만 삭제하기
```SQL
DELETE FROM EMP_TEMP2
WHERE JOB = 'MANAGER';

SELECT * FROM EMP_TEMP2;
```

```SQL
DELETE FROM EMP_TEMP2
WHERE EMPNO IN (SELECT E.EMPNO FROM EMP_TEMP2 E, SALGRADE S
		WHERE E.SAL BETWEEN S.LOSAL AND S.HISAL AND S.GRADE = 3
					AND S.GRADE = 3
					AND DEPTNO = 30);

SELECT * FROM EMP_TEMP2;
```

3. 테이블에 있는 전체 데이터 삭제하기
```SQL
DELETE FROM EMP_TEMP2;

SELECT * FROM EMP_TEMP2;
```
