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

7. 두 문자열 데이터를 합치는 CONCAT 함수

8. 문자열 데이터를 연결하는 || 연산자

9. 특정 문자를 지우는 TRIM, LTRIM, RTRIM 함수

❤️ 숫자 데이터를 연산하고 수치를 조정하는 숫자 함수

1. 특정 위치에서 반올림하는 ROUND
2. 특정 위치에서 버리는 TRUNC 함수
3. 지정한 숫자와 가까운 정수를 찾는 CEIL, FLOOR 함수
4. 숫자를 나눈 나머지 값을 구하는 MOD 함수

❤️ 날짜 데이터를 다루는 날짜 함수

1. DATE형 데이터는 다음과 같이 간단한 연산이 가능합니다.

   1. 날짜 데이터 + 숫자
   2. 날짜 데이터 - 숫자
   3. 날짜 데이터 - 날짜 데이터
   4. 날짜 데이터 + 날짜 데이터

2. SYSDATE 함수를 사용하여 날짜 출력하기
3. 몇 개월 이후 날짜를 구하는 ADD_MONTHS 함수
4. 두 날짜 간의 개월 수 차이를 구하는 MONTHS_BETWEEN 함수
5. 돌아오는 요일, 달의 마지막 날짜를 구하는 NEXT_DAY, LAST_DAY 함수

자료형을 변환하는 형 변환 함수

1. 자동 형 변환, 암시적 형변ㅅ환
2. 형변환 함수 - TO_CHAR, TO_NUMBER, TO_DATE
3. 날짜, 숫자 데이터를 문자 데이터로 변환하는 TO_CHAR 함수
4. 문자 데이터를 숫자 데이터로 변환하는 TO_NUMBER 함수
5. 문자 데이터를 날짜 데이터로 변환하는 TO_DATE 함수

NULL 처리 함수

1. NVL 함수
2. NVL2 함수

상황에 따라 다른 데이터를 반환하는 DECODE 함수와 CASE문

1. DECODE 함수
2. CASE 문
