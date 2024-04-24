<Day25 - 0423>
<JAVA java.lang 패키지>

# java.lang 패키지

❤️ java.lang 패키지

- java.lang 패키지에는 기본적으로 많이 사용하는 클래스들이 포함

(예) String
java.lang.String

- 컴파일러가 패키지명 바로 아래쪽 import java.lang.\*;가 추가
- java.lang 패키지는 컴파일 할 때 import java.lang.\*; 문장이 자동으로 추가되어 java.lang 패키지 하위 클래스를 모두 사용할 수 있으므로 직접 써 줄 필요가 없음
- 즉, import문을 직접 쓰지 않아도 java.lang 패키지의 모든 하위 클래스를 참조할 수 있음
- 그러므로 lang 패키지의 모든 클래스는 그냥 사용 가능

❤️ Object 클래스

- Object 클래스는 모든 자바 클래스의 최상위 클래스
- 모든 클래스는 Object 클래스로 부터 상속을 받음
- 상속이 명시되어 있지 않아도 -> extends java.lang.Object 가 자동으로 추가(컴파일 과정에서 컴파일러가 자동으로 추가)

❤️ Object 클래스에 정의된 메서드

1. toString() 메서드

   - toString() 메서드는 이름 처럼 객체 정보를 문자열(String)로 바꾸어 줌
   - Object 클래스를 상속받은 모든 클래스는 toString()을 재정의할 수 있음
   - 클래스의 성격에 맞게 재정의 되는 경우가 많음
   - public String toString() {
     return getClass().getName() + "@" + Integer.toHexString(hashCode());
     }
   - getClass().getName() : 클래스명(패키지명을 포함한 전체 클래스명)
   - Integer.toHexString(hashCode()); : 객체의 주소값을 16진수로 변환한 문자열

2. equals() 메서드

   public boolean equals(Object obj) {
   return (this == obj);
   }

   - equals() 메서드의 원래 기능은 두 인스턴스의 주소 값을 비교하여 boolean 값(true/false)을 반환해 주는 것
   - 물리적 동일성(인스턴스 메모리 주소가 같음)뿐 아니라 논리적 동일성(논리적으로 두 인스턴스가 같음)을 구현할 때도 equals() 메서드를 재정의하여 사용함
   - 동일성 비교(주소비교): ==
   - 동등성 비교(문자비교) : equals를 재정의
   - equals는 객체의 출처가 달라도 안에 있는 값이 동일하면 동일하다고 판단함

   (참고)
   String 클래스에서 문자열 비교시 == 를 쓰면 안됨
   equals를 사용해야 함 (문자열 비교는 equals를 사용해야 함)

   (참고)

   자바스크립트

   동일성 비교 : 동일한 주소(===)
   A === B A와 B는 같다 데이터 일치 + 데이터 종류 일치 여부 체크(10 === "10" --> false) 동일성 주소비교 / 두개는 독립적인 100원

   동등성 비교 : 동등한 가치(==) 100원의 가치
   A == B A와 B는 같다 데이터 일치 여부만 체크( 10 == "10" -> true) 동등성 가치비교 / 100원의 가치

3. hashCode() 메서드 (검색의 용도)

   - 객체에 대한 검색 (객체를 찾기 위한 값)
   - 기본값은 유일한 값으로 쓰기 위한 객체의 주소값(System.identityHashCode(...))
   - hashCode()의 기본값은 중복이 되지 않는 코드로 작성되어 있음 (객체의 주소값)
   - final이 붙어 있지 않기 때문에 필요에 따라 재정의를 하는 경우도 많음

💛💛💛 컴파일러가 자동으로 추가해주는 내용 💛💛💛

1. 기본 생성자
2. 모든 생성자에서 첫줄에 super 추가
3. 참조 변수를 출력 -> 참조변수.toString()
4. 인터페이스의 객체화 조건에서 지역변수의 상수화 final
5. 인터페이스의 추상메서드 - public abstract
6. 인터페이스의 변수 정의(정적상수) : public static final
7. import java.lang.\*;
8. extends java.lang.Object

String 클래스

1. String을 선언하는 두 가지 방법
2. String 클래스의 final char[] 변수
3. StringBuffer와 StringBuilder 클래스 활용하기

Wrapper 클래스

- 기본 자료형을 위한 클래스

1. Wrapper 클래스의 종류

2. Integer 클래스 사용하기

1) Integer 클래스의 메서드

3. 오토박싱과 언박싱

Class 클래스

1. Class 클래스를 선언하고 클래스 정보를 가져오는 방법
2. Class 클래스를 활용해 클래스 정보 알아보기
3. Class.forName()을 사용해 동적 로딩 하기

class의 구성 정보를 담고 있는 정보성 객체
