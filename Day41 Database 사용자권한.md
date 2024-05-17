<Day41- 0517>
<Database 사용자 권한, 롤 관리>

## 사용자, 권한, 롤 관리

❤️ 사용자 관리

1. 사용자란?

- 데이터베이스에 접속하여 데이터를 관리하는 계정

2. 데이터베이스 스키마란?
   (1) 데이터베이스에서 데이터 간 관계, 데이터 구조, 제약 조건 등 데이터를 저장 및 관리하기 위해 정의한 데이터베이스 구조의 범위
   (2) 오라클 데이터베이스에서는 스키마와 사용자를 구분하지 않고 사용하기도 합니다.
   (3) 사용자 : 데이터를 사용 및 관리하기 위해 오라클 데이터베이스에 접속하는 개체를 뜻
   (4) 스키마 : 오라클 데이터베이스에 접속한 사용자와 연결된 객체

3. 사용자 생성

   - CREATE USER
     -> 사용자 추가 시 접속 권한 X (CREATE SESSION)
     GRANT 시스템 권한 TO 사용자

   (참고)
   GRANT - 권한 부여
   REVOKE - 권한 취소

   REVOKE 취소할 시스템 권한 FROM 사용자

4. 사용자 정보 조회
5. 오라클 사용자의 변경과 삭제

- ALTER USER
- DROP USER
- DROP USER 사용자명; -> 스키마 삭제X
- DROP USER 사용자명 CASCADE; -> 스키마 함께 삭제

권한 관리하기

❤️ 시스템 권한

1. 사용자 생성과 정보 수정 및 삭제, 데이터베이스의 접근, 오라클 데이터베이스의 여러 자원과 객체 생성 및 관리 등의 권한을 포함
2. 데이터베이스의 관리 권한이 있는 사용자가 부여할 수 있는 권한
3. 소유자 ANY 키워드가 들어 있는 권한은 소유자에 상관없이 사용 가능한 권한

2) USER(사용자)

1. CREATE USER
2. ALTER USER
3. DROP USER

3) SESSION(사용자)

1. CREATE SESSION
2. ALTER SESSION

4) TABLE(테이블)

1. CREATE TABLE

5) INDEX(인덱스)
6) VIEW(뷰)
7) SEQUENCE(시퀀스)
8) SYNONYM(동의어)
9) PROFILE(프로파일)
10) ROLE(롤)

11) 시스템 권한 부여

- GRANT 시스템 권한(시스템 권한 ROLE..), ..TO 사용자;

- GRANT 시스템 권한, ..TO 사용자 WITH ADMIN OPTION;
  WITH ADMIN OPTION -> 사용자가 가지고 있는 권한은 다른 사용자에게 부여

12. 시스템 권한 취소

- REVOKE 시스템 권한 [시스템 권한 ROLE]... FROM 사용자;

❤️ 객체 권한

1. 특정 사용자가 생성한 테이블,인덱스,뷰,시퀀스 등과 관련된 권한

1) 객체 권한 분류

1. TABLE(테이블)
   ALTER, DELETE, INDEX, INSERT, REFERENCES, SELECT, UPDATE
2. VIEW(뷰)
3. SEQUENCE(시퀀스)
4. PROCEDURE(프로시저)
5. FUNCTION(함수)
6. PACKAGE(패키지)

2) 객체 권한 부여

- DML 관련 권한 : INSERT, UPDATE, DELETE, SELECT 권한
- GRANT 객체 권한/ALL PRIVILEGES ON 스키마. 객체이름 TO 사용자 또는 ROLE/PUBLIC - 모든 사용자
- GRANT 객체 권한/ALL PRIVILEGES ON 스키마. 객체이름 TO 사용자 또는 ROLE/PUBLIC - 모든 사용자 WITH GRANT OPTION;
- WITH GRANT OPTION : 사용자가 소유하고 있는 권한을 부여할 수 있는 권한

ALL PRIVILEGES : 모든 권한

3. 객체 권한 취소
   REVOKE 객체 권한, ... ON 스키마.객체이름 FROM 사용자명;

❤️ 롤 관리

1. 롤이란?

1) 여러 종류의 권한을 묶어 놓은 그룹
2) 오라클 데이터베이스를 설치할 때 기본으로 제공되는 사전 정의된 롤(predefined roles)과 사용자 정의 롤(user roles)로 나뉩니다.

CREATE 시스템 권한, ...TO ROLE 명칭;

2. 사전 정의된 롤

1) CONNECT롤
2) RESOURCE 롤
3) 보통 새로운 사용자를 생성하면 CONNECT롤과 RESOURCE롤을 부여하는 경우가 많음

3. 사용자 정의 롤

1) 롤 생성

- CREATE ROLE 롤이름;

2. 부여된 롤과 권환 확인

- USER_SYS_PRIVIS;
- USER_ROLE_PRIVIS;

3. 롤 취소
4. 롤 삭제
