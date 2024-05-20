<Day42- 0520>
<Database 커서와 예외처리>

## 커서와 예외 처리

❤️ 특정 열을 선택하여 처리하는 커서

1. 커서란?

   (1) SELECT문 또는 데이터 조작어 같은 SQL문을 실행했을 때 해당 SQL문을 처리하는 정보를 저장한 메모리 공간
   (2) 커서는 이 메모리의 포인터
   (3) 커서는 사용 방법에 따라 명시적(explicit) 커서와 묵시적(implicit) 커서로 나뉩니다.

2. SELECT INTO 방식

   (1) SELECT INTO를 사용한 단일행 데이터 저장하기
   SELECT 컬럼1, 컬럼2, ...INTO 변수1, 변수2 ...

3. 명시적 커서

   (1) 단계

   - 커서 선언(Declaration)
   - 커서 열기(open)
   - 커서에서 읽어온 데이터 사용(Fetch)
   - 커서 닫기(Close)

   (2). 작성법
   🤍DECLARE
   CURSOR 커서이름 IS SQL문; -- 커서 선언(Declaration)
   🤍BEGIN
   OPEN 커서 이름; -- 커서 열기(open)
   FETCH 커서이름 INTO 변수 -- 커서로부터 읽어온 데이터 사용(Fetch)
   CLOSE 커서이름; -- 커서 닫기(Close)
   🤍END;

   ```SQL
   DECLARE
   	V_DEPT DEPT%ROWTYPE;

   	CURSOR C1 IS -- 커서 선언
   		SELECT * FROM DEPT;
   BEGIN
   	OPEN C1; -- 커서 열기
   	LOOP
   	FETCH C1 INTO V_DEPT; -- 데이터 가져오기
   	-- 커서의 값중 %NOTFOUND가 참 -> 더이상 읽을 레코드가 없다.
   	EXIT WHEN C1%NOTFOUND;
   	DBMS_OUTPUT.PUT_LINE('DEPTNO : ' || V_DEPT.DEPTNO);
   	DBMS_OUTPUT.PUT_LINE('DNAME : ' || V_DEPT.DNAME);
   	DBMS_OUTPUT.PUT_LINE('LOC : ' || V_DEPT.LOC);
   	DBMS_OUTPUT.PUT_LINE('------------------------------');
   	END LOOP;
   	CLOSE C1; -- 커서 닫기
   END;
   ```

   (3). 하나의 행만 조회되는 경우
   (4). 여러 행이 조회되는 경우 사용하는 LOOP문
   (5). 여러 개의 행이 조회되는 경우(FOR LOOP문)
   -> OPEN, CLOSE, FETCH 생략 가능

   ```SQL
   DECLARE
   	CURSOR C1 IS -- 커서 선언
   		SELECT * FROM DEPT;
   BEGIN
   	FOR d IN C1 LOOP
   		DBMS_OUTPUT.PUT_LINE('DEPTNO : ' || d.DEPTNO);
   	DBMS_OUTPUT.PUT_LINE('DNAME : ' || d.DNAME);
   DBMS_OUTPUT.PUT_LINE('LOC : ' || d.LOC);
   DBMS_OUTPUT.PUT_LINE('----------------------------');
   	END LOOP;
   END;
   ```

   (6). 커서에 파라미터 사용하기
   CURSER 커서명(변수명 자료형,...) IS
   SELECT ... 변수는 SELECT문 내에서 사용 가능

   OPEN 커서명(값, ...);

4. 묵시적 커서

   (1). 다른 선언 없이 SQL문을 사용했을 때 오라클에서 자동으로 선언되는 커서
   (2). 사용자가 OPEN, FETCH, CLOSE를 지정하지 않음 PL/SQL문 내부에서 DML 명령어나 SELECT INTO문 등이 실행될 때 자동으로 생성 및 처리

❤️ 오류가 발생해도 프로그램이 비정상 종료되지 않도록 하는 예외 처리

1. 예외가 발생하는 PL/SQL
2. 예외를 처리하는 PL/SQL(예외 처리 추가)
3. 예외 발생 후의 코드 실행 여부 확인하기
4. 예외 종류
5. 예외 처리부 작성

EXCEPTION
WHEN 예외 이름1 [OR 예외 이름2 - ] THEN
예외 처리에 사용할 명령어;
WHEN 예외 이름3 [OR 예외 이름4 - ] THEN
예외 처리에 사용할 명령어;
...
WHEN OTHERS THEN
예외 처리에 사용할 명령어;

6. 사전 정의된 예외 사용
7. 오류 코드와 오류 메시지 사용
   - SQLCODE : 오류번호
   - SQLERRM : 오류 메세지
