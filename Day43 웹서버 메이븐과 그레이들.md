<Day43- 0521>
<웹서버 메이븐과 그레이들>

## maven

❤️ 메이븐

- 빌드, 의존성(필요한 라이브러리 jar(Java Archive))관리, 배포, 테스트 툴

(참고)
npm(Node Package Manager)
yarn

1. 설치
   자바 설치O
   환경 변수 JAVA_HOME

D:\이소은\apache-maven-3.9.6\bin
path

2. 사용

1)  maven 프로젝트 생성
    mvn archetype:generate
    groupId : 소속된 그룹(도메인 방식)
    (예) org.project
    artifactId : 프로젝트 구분 명칭

        프로젝트 디렉토리 구조
        	클래스패스 : 클래스 파일을 인식할 수 있는 경로

        	🤍src/main/java : 실제로 작성하는 자바코드(.java)
        	🤍src/main/resources : 정적 자원 정의
        									- 설정 파일(xml, properties)
        									- css, js, 이미지

        	🤍src/test/java : 테스트 자바 코드(.java)
        	🤍src/test/resources : 테스트시 필요 정적 자원 정의

        pom.xml : maven 설정 파일
            (참고)
                node : package.json 파일과 동일한 역할

        	<properties>
        		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding> : 소스 인코딩
        		<maven.compiler.source>17</maven.compiler.source> : 소스 컴파일 자바 버전
        		<maven.compiler.target>17</maven.compiler.target> : 배포 파일(jar) 생성시 자바 버전
        	  </properties>

        	   - 의존성 설정
        	  <dependencies>

        	  </dependencies>

        		 사용자명/.m2  -> 메이븐 레포지토리 (공유)

        		 🤍scope
        			- compile (기본값) : 빌드시 포함, 배포시 포함
        			- runtime : 빌드시 포함 X, 실행할때는 필요한 라이브러리 (동적 로딩 - ★★★Class.forName(...))
        			- provided : 개발시에만 필요, 빌드 및 배포시에는 미포함 -> 플랫폼 내에서 제공되는 라이브러리
        								(예) servlet-api, servlet.jsp-api
        			- test  : 테스트 시에만 필요한 라이브러리

        mvn compile : java 파일 -> class 컴파일 (target 폴더)

        mvn clean : 컴파일 소스 전체 지우기(target 폴더 삭제)

        	(예) 기존 컴파일 소스 삭제 후 다시 컴파일
        		mvn clean compile

        mvn test : 테스트 케이스를 실행(전체)

        mvn package : 배포 파일 생성(jar)
        		compile -> test -> package(jar)
        			-> 테스트 미통과시 배포 X

        		(mvn) 기존 컴파일 소스 삭제 후 배포 실행
        			mvn clean package

        	jar 파일 실행

        	jar -jar 파일명.jar

        CTRL + SHIFT + B

버전 표기법
1 .18. 30
(Major) (Minor) (Patch)

Major - 기존 버전과 호환되지 않은 버전 (호환성 문제가 생길 수 있는 큰 변화)
Minor - 호환성에는 문제가 없는 기능 추가나 수정이 있을 때
Patch - 코드의 오류, 버그, 수정이 있는 경우 (오류에 대한 수정이나 기능 개선)

lombok.jar

maven central : 의존성 저장소

mvnrepository

lombok

@Getter
@Setter
@ToString
@EqualsAndHashCode

@Data - @Getter, @Setter, @ToString, @EqualsAndHashCode

생성자
@NoArgsConstructor : 기본생성자
@AllArgsConstructor : 모든 멤버 변수로 초기화하는 생성자
@RequiredArgsConstructor : 필수 멤버 변수를 생성자 매개변수로 추가 - @NonNull로 표시
멤버 변수를 final(상수)로 정의한 경우, 값을 대입하지 않은 경우도 초기화 필요

@ToString.Exclude : toString()에 추가 배제
@ToString.Include : toString()에 추가(포함)

@Builder : 빌더 패턴으로 자동 생성

빌더 패턴? -> 값을 설정 -> 객체를 내부에서 생성하는 패턴 - 내부에서 객체를 생성(외부에서 객체X) - 생성자 접근제어자가 private으로 되어있음

## Gradle

❤️ 그레이들(Gradle)

설정파일 build.gradle
-> 그루비, 코틀린 : DSL 특화 언어

DSL(Domain Specific Language)

- Domain : 전문가 영역
- 설정 영역

ext{
//
}
ext -> 전역변수를 설정하는 영역

1. 설치
   D:\이소은\gradle-8.7\bin
2. 그레이들 명령어

1) 버전 확인
   gradle --version

   명령어
   gradle tasks -> 그레이들에서 사용할 수 있는 모든 명령어가 나옴

2) 프로젝트 생성

- gradle init [--type 타입명]
- build.gradle : 프로젝트에 필요한 의존성과 빌드처리 내용을 작성하는 파일
- settings.gradle : 프로젝트에 대한 설정정보를 작성하는 파일

(참고)
메이븐
mvn archetype:generate

3. java-application 타입으로 생성 시 프로젝트 구조

4. 프로젝트 빌드

- gradle build
- 프로젝트를 컴파일(빌드)한다.
- build.gradle에 apply plugin: 'java'가 추가된 경우 .jar파일로 패키징까지 된다.
- 컴파일된 파일들은 'app > build' 폴더 안에 생성되며, ㅎ.jar파일은 'build > libs'에 패키징된다.
- 컴파일 - 테스트 - 배포
- 테스트가 실패하면 배포 X (중간에 하나라도 되어있지 않으면 배포가 되지 않음)

- gradle clean build -> 지우고 새로 만들기

(참고)
메이븐 mvn package : compile test 배포

5. 프로젝트 실행

- gradle run
- 컴파일 후 메인클래스를 실행한다.
- 스프링부트의 경우 gradle bootRun을 통해 앱을 구동할 수 있다.

6. 프로젝트 패키징

- gradle jar
- 프로그램을 .jar로 패키징
- 'build > libs'에 생성된다.
- apply plugin: 'java'가 추가된 경우 build명령으로 해결가능
- 테스트 X 배포

(참고)
gradle bootJar : 스프링 부트에서..

7. 프로젝트 클린

- gradle clean
- build 디렉토리 삭제

8. gradle-wrapper

- gradle' 명령어로 프로젝트를 빌드할 수 있지만, gradle-wrapper의 실행명령으로도 task를 실행할 수 있다.
- 새로운 환경에서 gradle을 설치하지 않고도 빌드가 가능
  - gradle 명령어의 경우 기본적으로 gradle이 로컬에 설치가 되어있어야 한다.
  - 또한 gradle 명령어로 빌드를 할 경우 로컬에 설치된 gradle 버젼으로 빌드되기 때문에, 개발 당시 버젼과 다를경우 문제를 일으킬 수도 있다.
- gradlew build를 사용하면 사용자가 프로젝트를 만든 사람과 동일한 버전으로 빌드를 할 수 있으며, 심지어 gradle이 설치되지 않아도 빌드가 가능하다.

3. build.gradle

maven
<dependency>
...
<scope></scope>
</dependency>

scope

- compile : 컴파일시에 포함, 배포시 포함
- runtime : 컴파일시에 X, 실행중 포함
- provied : 개발시에만 필요, 배포시에 배제
- test : 테스트시에 필요

## JDBC(Java DataBase Connectivity) API

❤️ JDBC(Java DataBase Connectivity) API

- 자바 데이터베이스 연결 기술 명세서 - 인터페이스로 구성
- 구현체는 각 DB 업체가 구성 (데이터베이스 드라이버)

- java.sql 패키지 - JDBC API

1. Oracle JDBC 드라이버 설치

DriverManager 클래스 -> Connection
DataSource 인터페이스 -> Connection : 커넥션 풀

2. 연동 과정

1) java.sql.\* 패키지 임포트
2) JDBC 드라이버 로딩
3) 데이터베이스 접속을 위한 Connection객체 생성
4) 쿼리문을 실행하기 위한 Statement/PreparedStatement/CallableStatement 객체 생성
5) 쿼리 실행
6) 쿼리 실행 결과 값(int, ResultSet) 사용
7) 사용된 객체(ResultSet, Statement/PreparedStatement/CallableStatement, Connection) 종료

3. JDBC 드라이버 로딩 및 DBMS 접속

1) JDBC 드라이버 로딩하기
2) Connection 객체 생성하기
3) 데이터베이스 연결 닫기

❤️ 데이터베이스 쿼리 실행

1. Statement 객체로 데이터 접근하기

1) ResultSet executeQuery(String sql)
2) int executeUpdate(String sql)
3) close()

2. PreparedStatement 객체로 데이터 접근하기

1) 동적인 쿼리에 사용
2) 하나의 객체로 여러 번의 쿼리를 실행할 수 있으며, 동일한 쿼리문을 특정 값만 바꾸어서 여러 번 실행해야 할 때, 매개변수가 많아서 쿼리문을 정리해야 할 때 유용

3. CallableStatement 객체로 데이터 접근하기

1) 프로시저 실행시 사용

3. 쿼리문 실행 결과 값 가져오기

1) ResultSet 객체의 메서드

커넥션 풀
Tomcat JDBC
