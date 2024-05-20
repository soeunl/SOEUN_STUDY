<Day42- 0520>
<Database 레코드와 컬렉션>

## 레코드와 컬렉션

❤️ 자료형이 다른 여러 데이터를 저장하는 레코드

1. 레코드란?

- 각기 다른 데이터를 하나의 변수에 저장하는 데 사용
- 레코드에 포함된 변수는 레코드 이름과 마침표(.)로 사용할 수 있음

2. 형식
   TYPE 레코드 이름 IS RECORD(
   변수 이름 자료형 NOT NULL := (또는 DEFAULT) 값 또는 값이 도출되는 여러 표현식
   );

3. 레코드 정의해서 사용하기

4. 레코드를 사용한 INSERT

(1) DEPT_RECORD 테이블 생성하기
CREATE TABLE DEPT_RECORD AS SELECT\*FROM DEPT;

(2) 레코드를 사용하여 INSERT 하기
INSERT INTO DEPT_RECORD VALUES DEPT_DATA;

UPDATE
SET ROW = DEPT_DATA
WHERE DEPTNO = 99;

5. 레코드를 포함하는 레코드

(1) 레코드에 포함된 변수의 자료형을 지정할 때 다른 레코드를 지정할 수도 있음
(2) 레코드에 다른 레코드 포함하기 - 중첩 레코드

(참고)
단일 조회 값 -> 변수에 넣는 방법
SELECT 필드명, ...INTO 변수, ...FROM ... WHERE ..

❤️ 자료형이 같은 여러 데이터를 저장하는 컬렉션

- 컬렉션은 특정 자료형의 데이터를 여러 개 저장하는 복합 자료형

1. 연관배열

1) 인덱스라고 불리는 키(key), 값(value)으로 구성되는 컬렉션
   - 인덱스 : 정수(BINARY_INTEGER, PLS_INTEGER), 문자(VARCHAR2)
2) 중복되지 않은 유일한 키를 통해 값을 저장하고 불러오는 방식을 사용
3) 형식

TYPE 연관 배열 이름 IS TABLE OF 자료형 [NOT NULL]
INDEX BY 인덱스형;

4. 연관 배열 사용하기
5. 연관 배열 자료형에 레코드 사용하기

2) 컬렉션 메서드

- 편의 메서드

(참고)💙💙💙
변수 자료형 (시험에 나옴) ★★★

1. 스칼라(scalar) : 단일값
   - NUMBER, CHAR, VARCHAR2, DATE, BOOLEAN
2. LOB(Large OBject) : CLOB, BLOB
3. 참조형 : 테이블, 컬럼%TYPE -> 테이블의 컬럼의 자료형을 참조
   테이블%ROWTYPE -> 테이블의 모든 컬럼을 참조
   - %TYPE : 테이블 열의 자료형
     DEPT.DEPTNO%TYPE -> DEPT 테이블의 DEPTNO 컬럼의 자료형
   - %ROWTYPE : 테이블의 전체 자료형
     DEPT%ROWTYPE -> DEPT 테이블의 전체 컬럼
4. 복합형 :
   - RECORD : 변수를 여러개 묶어서 정의하는 자료형
   - TABLE(컬렉션) : 키-값의 구조
