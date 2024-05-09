<Day35 - 0508>
<Database 오라클 함수>

## 데이터 처리와 가공을 위한 오라클 함수

❤️ 오라클 함수의 종류

1. 내장 함수

   🤍 단일행 함수(single-row function) : 데이터가 한 행씩 입력되고 입력된 한 행당 결과가 하나씩 나오는 함수

   SELECT EMPNO, REPLACE(ENAME, 'A', '\*') ENAME FROM EMP;

   🤍 다중행 함수(multiple-row function): 여러 행이 입력되어 하나의 행의 결과로 반환되는 함수

   SELECT SUM(SAL) 합계 FROM EMP;

2. 사용자 정의 함수

❤️ 문자 데이터를 가공하는 문자함수

1. 대,소문자를 바꿔 주는 UPPER, LOWER, INITCAP 함수

   SELECT UPPER('abc'), LOWER('ABC'), INITCAP('abc') FROM DUAL;

   UPPER() : 소문자 -> 대문자
   LOWER() : 대문자 -> 소문자
   INITCAP() : 첫글자만 대문자로

   (참고)
   -- 이름을 대소문자 구분 없이 조회할 때 활용가능
   SELECT \* FROM EMP WHERE UPPER(ENAME) LIKE UPPER ('scott');

2. 문자열 길이를 구하는 LENGTH 함수
   LENGTH(컬럼명) : 문자열 길이
   영문자 1자 - 1바이트
   한글 1자 - 2바이트, 3바이트(UTF-8)
   LENGTHB(컬럼명) : 문자열의 바이트 수

   (참고)
   MySQL
   : LENGTH(..) - 문자열 바이트 수
   : CHAR_LENGTH(..) - 문자열 갯수

3. 문자열 일부를 추출하는 SUBSTR 함수
   SUBSTR(컬럼, 시작위치, 추출 길이)
   SUBSTR(컬럼, 시작위치) - 시작 위치 부터 끝까지
   시작위치

   - 1부터 시작
   - 양수 : 왼쪽부터 시작 위치
   - 음수 : 오른쪽부터 시작 위치

4. 문자열 데이터 안에서 특정 문자 위치를 찾는 INSTR 함수
   INSTR(컬럼, '찾는 키워드')
   INSTR(컬럼, '찾는 키워드', 검색 시작 위치(기본값은 1))

   - 1번 위치부터 시작
   - 키워드를 못 찾은 경우 0을 반환
   - LIKE와 비슷한 효과
     ENAME LIKE '%S%';

   (참고)

   indexOf(..)와 비슷

   - 특정 문자열의 위치를 찾는 함수
   - 0번 위치부터 시작
   - 특정 문자열을 못 찾은 경우 -1반환

5. 특정 문자를 다른 문자로 바꾸는 REPLACE 함수
   REPLACE(컬럼, '찾는 문자열', '치환될 문자열')

6. 데이터의 빈 공간을 특정 문자로 채우는 LPAD, RPAD 함수
   채워넣는다는 뜻 (방향성을 가지고 채워넣음)
   LPAD : 왼쪽 패딩
   LPAD (컬럼, 문자열, 자리수, '채워넣을 문자');
   RPAD : 오른쪽 패딩
   RPAD (컬럼, 문자열, 자리수, '채워넣을 문자');

   SELECT LPAD('100', 10, '0') FROM DUAL;
   SELECT RPAD('user', 10, '\*') FROM DUAL;

   -- 이름 3글자 빼고 나머지는 \*로 처리
   SELECT RPAD(SUBSTR(ENAME, 1, 3), LENGTH(ENAME), '\*') ENAME FROM EMP;

7. 두 문자열 데이터를 합치는 CONCAT 함수
   문자열 두개를 결합

   SELECT EMPNO, ENAME, JOB, CONCAT(CONCAT(ENAME,' : '), JOB) FROM EMP;

8. 문자열 데이터를 연결하는 || 연산자
   오라클에만 있는 연산자
   ENAME || ':'|| JOB

   SELECT EMPNO, ENAME, JOB, ENAME || ' : ' || JOB FROM EMP;

9. 특정 문자를 지우는 TRIM, LTRIM, RTRIM 함수
   TRIM : 양쪽 공백(여백) 제거
   SELECT TRIM(' ABC ') || 'DEF' FROM DUAL;

   LTRIM : 왼쪽 공백(여백) 제거
   RTRIM : 오른쪽 공백(여백) 제거

   TRIM(LEADING FROM 문자열) : 왼쪽 여백 제거
   TRIM(TRALLING FROM 문자열) : 오른쪽 여백 제거

   SELECT TRIM(BOTH FROM ' ABC ') || 'DEF' FROM DUAL;
   (BOTH FROM은 생략가능)

   SELECT TRIM(LEADING FROM ' ABC ') || 'DEF' FROM DUAL;

   SELECT TRIM(LEADING FROM '**_ABC_**', '_') || 'DEF' FROM DUAL;(왼쪽에 있는 _ 제거)

   SELECT TRIM(TRAILING FROM ' ABC ') || 'DEF' FROM DUAL;

   SELECT TRIM(TRAILING '\*' FROM '_ABC_') || 'DEF' FROM DUAL; (오른쪽에 있는 \* 제거)

❤️ 숫자 데이터를 연산하고 수치를 조정하는 숫자 함수

1. 특정 위치에서 반올림하는 ROUND
   뒤에 나오는 양수가 소숫점 자릿수
   (EX)1을 적으면 소숫점 두번째 자리에서 반올림하여 소숫점 첫번째 자리에 반영

   SELECT ROUND(123.4567, 1) FROM DUAL; -- 123.5

   SELECT ROUND(123.4567, 2) FROM DUAL; -- 123.46

   SELECT ROUND(123.4567, -1) FROM DUAL; -- 120
   (- 일때는 정수자리에서 반올림. .앞이 0이다)

2. 특정 위치에서 버리는 TRUNC 함수
   TRUNC : 절사

   SELECT TRUNC(12345.123456, 0) FROM DUAL; --12345
   SELECT TRUNC(12345.123456, 1) FROM DUAL; -- 12345.1
   SELECT TRUNC(12345.123456, -3) FROM DUAL; -- 12000

3. 지정한 숫자와 가까운 정수를 찾는 CEIL, FLOOR 함수
   CEIL : 올림
   FLOOR : 버림

   SELECT CEIL(123.4567) FROM DUAL; -- 124

   SELECT FLOOR(123.678) FROM DUAL; -- 123

4. 숫자를 나눈 나머지 값을 구하는 MOD 함수
   SELECT MOD(10, 3) FROM DUAL;

❤️ 날짜 데이터를 다루는 날짜 함수

1. DATE형 데이터는 다음과 같이 간단한 연산이 가능

   1. 날짜 데이터 + 숫자 : 숫자만큼 일수가 더해짐
   2. 날짜 데이터 - 숫자 : 숫자만큼 일수가 빼짐
   3. 날짜 데이터 - 날짜 데이터 : 날짜 사이 일수차이
   4. 날짜 데이터 + 날짜 데이터 : 오류 발생, 불가

2. SYSDATE 함수를 사용하여 날짜 출력하기
   SYSDATE : 현재 시스템의 날짜 시간

   SELECT
   HIREDATE,
   HIREDATE + 100,
   HIREDATE - 100,
   CEIL(SYSDATE - HIREDATE)
   FROM EMP;

3. 몇 개월 이후 날짜를 구하는 ADD_MONTHS 함수
   월 단위로 가감

   SELECT
   ADD_MONTHS(SYSDATE, 6) "6개월 후",
   ADD_MONTHS(SYSDATE, -6) "6개월 전"
   FROM DUAL;

4. 두 날짜 간의 개월 수 차이를 구하는 MONTHS_BETWEEN 함수
   SELECT HIREDATE, CEIL(MONTHS_BETWEEN(SYSDATE, HIREDATE)) FROM EMP;

5. 돌아오는 요일, 달의 마지막 날짜를 구하는 NEXT_DAY, LAST_DAY 함수
   NEXT_DAY(날짜, 요일) : 다음 요일의 날짜

   SELECT NEXT_DAY(SYSDATE, '목') "다음 목요일" FROM DUAL;
   SELECT NEXT_DAY(SYSDATE, '금') "다음 금요일" FROM DUAL;

   LAST_DAY(날짜) : 날짜에 해당하는 월의 마지막 일자

   SELECT LAST_DAY(SYSDATE) "마지막 일자" FROM DUAL;

   (참고)
   DAY : 요일

❤️ 자료형을 변환하는 형 변환 함수

1. 자동 형 변환, 암시적 형변환
   '2024-05-09' : 문자 -> DATE 형변환
   '1000' : 문자 -> 연산시 -> NUMBER 형으로 변환
   -> 형식을 오라클이 충분히 파악 가능한 경우에 가능
   SELECT'1000' + 200 FROM DUAL;

2. 형변환 함수 - TO_CHAR, TO_NUMBER, TO_DATE
   TO_CHAR(..) : 숫자, 날짜 -> 형식화된 문자열

   SELECT EMPNO, ENAME, TO_CHAR(SAL, '$999,999')FROM EMP;

   숫자 : TO_CHAR(SAL, '$999,999')
   날짜 : TO_CHAR(HIREDATE, 'YYYY.MM.DD')

   TO_NUMBER(..) : 문자로 되어 있는 형식화된 숫자(1,000) -> 숫자
   SELECT TO_NUMBER ('1,000,000', '999,999,999') + 200 FROM DUAL;

   TO_DATE(..) : 문자로 형식화된 날짜 -> 날짜
   TO_DATE(문자열 날짜, 형식)

   SELECT TO_DATE('90-05-08', 'YY/MM/DD')FROM DUAL; -- 2090
   SELECT TO_DATE('90-05-08', 'RR/MM/DD')FROM DUAL; -- 1990

   SELECT \* FROM EMP
   WHERE HIREDATE
   BETWEEN TO_DATE('01/01/1981', 'MM/DD/YYYY')
   AND TO_DATE('12/31/1981', 'MM/DD/YYYY');

   형식
   YYYY -> 4자리 연도 : 2024
   YY -> 2자리 연도 24
   (예) 90-05-09: -> 2090-05-09 (2090년이 되어버림)

   RRRR -> 4자리 연도
   RR -> 2자리 연도
   (예) 90-05-09 : 1990-05-09 (가장 가까운 연도로 바뀜)

   MM -> 월
   DD -> 일

   HH24 : 24시간 표기 시간
   HH12 / HH : 12시간 표기 시간

   MI : 분
   SS : 초

   - 날짜, 숫자 데이터를 문자 데이터로 변환하는 TO_CHAR 함수
   - 문자 데이터를 숫자 데이터로 변환하는 TO_NUMBER 함수
   - 문자 데이터를 날짜 데이터로 변환하는 TO_DATE 함수

❤️ NULL 처리 함수

1. NVL 함수
   NVL (컬럼, 기본값)

   SELECT
   EMPNO, ENAME, SAL, COMM,
   SAL \* 12 + NVL(COMM, 0) 연봉
   FROM EMP;

2. NVL2 함수
   삼항조건 연산자와 비슷
   NVL2(컬럼, NULL이 아닐 때 값, NULL일때 값)

   SELECT
   EMPNO, ENAME, SAL, COMM,
   SAL \* 12 + NVL(COMM, 0) 연봉,
   NVL2(COMM, 'O', 'X') "커미션 유무"
   FROM EMP;

❤️ 상황에 따라 다른 데이터를 반환하는 DECODE 함수와 CASE문
switch ~ case 와 유사한 문법

1.  DECODE 함수
    오라클 전용 함수

    SELECT
    EMPNO, ENAME, JOB, SAL,
    DECODE(JOB,
    'MANAGER', SAL _ 1.1,
    'SALESMAN', SAL _ 1.05,
    'ANALYST', SAL,
    SAL \* 1.03) "내년 급여"
    FROM EMP;

2.  CASE 문
    표준함수

    SELECT EMPNO, ENAME, JOB, SAL,
    CASE JOB
    WHEN 'MANAGER' THEN SAL _ 1.1
    WHEN 'SALESMAN' THEN SAL _ 1.05
    WHEN 'ANALYST' THEN SAL
    ELSE SAL \* 1.03
    END "내년 급여"
    FROM EMP;

    SELECT EMPNO, ENAME, SAL,
    CASE
    WHEN SAL >= 3000 THEN 'HIGH'
    WHEN SAL >= 2000 THEN 'MID'
    ELSE 'LOW'
    END 소득레벨
    FROM EMP;

단일행 함수
