<Day41- 0517>
<Database PL, SQL 기초>

## PL/SQL 기초

❤️ PL/SQL 구조

- Oracle Procedual Language extension to SQL

🤍 PL/SQL 구조

1. 블록이란?

데이터베이스 관련 특정 작업을 수행하는 명령어와 실행에 필요한 여러 요소를 정의하는 명령어 등으로 구성되며, 이러한 명령어를 모아 둔 PL/SQL 프로그램의 기본 단위

2. 기본 형식

🤍DECLARE - [실행에 필요한 여러 요소 선언]; - 변수, 상수, 커서
🤍BEGIN - [작업을 위해 실제 실행하는 명령어]; - 코드를 주로 넣음
🤍EXCEPTION- [PL/SQL 수행 도중 발생하는 오류 처리]; - 예외처리
END;

3. Hello, PL/SQL 출력하기
4. PL/SQL 주석
   한줄 주석 : -- DBMS_OUTPUT.PUT_LINE(GREETING);
   여러줄 주석 : /\*
   DBMS_OUTPUT.PUT_LINE(GREETING);
   DBMS_OUTPUT.PUT_LINE(GREETING);
   \*/

❤️ 변수와 상수

1. 변수 선언과 사용

   (1) 변수이름 자료형 := 값 또는 값이 도출되는 표현식
   (2) 변수 선언 및 변수 값 출력하기

2. 상수 정의하기

   (1) 변수이름 CONSTANT 자료형 := 값 또는 값이 도출되는 표현식
   (2) 상수에 값을 대입한 후 출력하기

3. 변수의 기본값 지정하기

   (1) 변수이름 자료형 DEFAULT := 값 또는 값이 도출되는 표현식
   (2) 변수에 기본값을 설정한 후 출력하기

4. 변수에 NULL 값 저장 막기

   (1) 변수이름 자료형 NOT NULL := 값 또는 값이 도출되는 표현식
   (2) 변수에 NOT NULL을 설정하고 값을 대입한 수 출력하기

5. 변수 이름 정하기

❤️ 변수의 자료형

1. 스칼라 : 단일 값, 숫자, 문자열, 날짜, 논리형

   (1) 숫자 NUMBER
   (2) 문자열 CHAAR, VARCHAR2
   (3) 날짜 DATE
   (4) 논리 데이터 BOOLEAN (true, false, NULL)

   LOB : Large Object - CLOB, BLOB

2. 참조형

   (1) %TYPE : 특정 테이블의 열(컬럼) 1개의 자료형을 참조
   (2) %ROWTYPE : 특정 테이블의 모든 컬럼들을 참조
   (3) 변수 이름 테이블이름.열이름%TYPE
   (4) 참조형(열)의 변수에 값을 대입한 후 출력하기
   (5) 특정 테이블에서 하나의 열이 아닌 행 구조 전체를 참조할 때 %ROWTYPE을 사용
   (6) 변수이름 테이블이름%ROWTYPE
   (7) 참조형(행)의 변수에 값을 대입한 후 출력하기

3. 복합형

   - RECORD : 여러 변수와 자료형을 한꺼번에 선언하는 방식 / 레코드
   - TABLE : 키 - 값 / 컬렉션

   (1) 컬렉션, TABLE 자료형 : 한 가지 자료형의 데이터를 여러 개 저장(테이블의 열과 유사)
   (2) 레코드, RECORD 자료형 : 여러 종류 자료형의 데이터를 저장(테이블의 행과 유사)

❤️ 조건 제어문

1. 조건문

1) IF-THEN

- 변수에 입력한 값이 홀수인지 알아보기(입력 값이 홀수일 때)

2. IF-THEN-ELSE

- 변수에 입력된 값이 홀수인지 짝수인지 알아보기(입력 값이 짝수일 때)

3. IF-THEN-ELSIF

- 입력한 점수가 어느 학점인지 출력하기

2. CASE 조건문

1) 단순 CASE

- 입력 점수에 따른 학점 출력하기(단순 CASE 사용)

2. 검색 CASE

- 입력 점수에 따른 학점 출력하기(검색 CASE 사용)

❤️ 반복 제어문

1. 반복문 종류

1) 기본 LOOP
2) WHILE LOOP
3) FOR LOOP
4) Cursor For LOOP

2. 반복 중단 명령어 종류

1) EXIT
2) EXIT-WHEN
3) CONTINUE
4) CONTINUE-WHEN

3. 기본 LOOP
4. WHILE LOOP
5. FOR LOOP
6. CONTINUE문, CONTINUE-WHEN문
