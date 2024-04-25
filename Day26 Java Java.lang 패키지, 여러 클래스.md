<Day26 - 0424>
<JAVA java.lang 패키지, 여러 클래스>

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
   - toString() 메서드의 원형은 생성된 인스턴스 클래스의 이름과 주소 값을 보여줌
   - Object 클래스를 상속받은 모든 클래스는 toString()을 재정의할 수 있음
   - 클래스의 성격에 맞게 재정의 되는 경우가 많음
   - Gernerate에서 toString()을 눌러 재정의
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
   - JDK에서 제공하는 String 클래스와 Integer 클래스에는 equals() 메서드가 이미 재정의 되어 있으므로 이 클래스들을 사용하면 equals()가 재정의됨
   - String 클래스의 equals() 메서드는 같은 문자열의 경우 true를, 그렇지 않은 경우 false를 반환하도록 재정의되어 있음
   - 물리적 동일성(인스턴스 메모리 주소가 같음)뿐 아니라 논리적 동일성(논리적으로 두 인스턴스가 같음)을 구현할 때도 equals() 메서드를 재정의하여 사용함
   - Integer 클래스의 경우도 정수 값이 같은 경우 true를 반환하도록 equals() 메서드가 재정의되어 있음
   - 동일성 비교(주소비교): ==
   - 동등성 비교(문자비교) : equals and hashCode 메서드를 재정의
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

   - 기본 구현 : 객체의 주소값
   - 객체에 대한 검색 (객체를 찾기 위한 값)
   - 기본값은 유일한 값으로 쓰기 위한 객체의 주소값(System.identityHashCode(...))
   - hashCode()의 기본값은 중복이 되지 않는 코드로 작성되어 있음 (객체의 주소값)
   - hash : 같은 값에 대해서 같은 정수값을 생성하는 편의기능
   - final이 붙어 있지 않기 때문에 필요에 따라 재정의를 하는 경우도 많음

💜 (참고) 편의기능

- util 유틸패키지는 편의기능
- 명칭 + s 는 편의기능
- 객체는 만들지 않고 기능만 나열되어 있다
- static으로 정의되어 있다
- ... 점3개 -> 가변적인 형태의 매개변수가 정의되어 있다 (가변적!!)

💜동등성 비교 시에는 equals()와 hashCode() 메서드를 함께 재정의해서 사용해야 함 (equals()를 오버라이딩 할 때 hashCode()도 같이 오버라이딩을 해주어야 함)
이유 - equals()와 hashCode()의 반환값이 같아야 같은 객체로 이해하기 때문이다 (두 객체가 equals()에 의해 동일하다면, 두 객체의 hashCode() 값도 일치해야 함)

💛💛💛 컴파일러가 자동으로 추가해주는 내용 💛💛💛

1. 기본 생성자
2. 모든 생성자에서 첫줄에 super 추가
3. 참조 변수를 출력 -> 참조변수.toString()
4. 인터페이스의 객체화 조건에서 지역변수의 상수화 final
5. 인터페이스의 추상메서드 - public abstract
6. 인터페이스의 변수 정의(정적상수) : public static final
7. import java.lang.\*;
8. extends java.lang.Object

❤️ String 클래스

1. String을 선언하는 두 가지 방법

   - string str = "문자열"; // 문자열 상수를 가리키는 방식
   - string str = new String("문자열"); // 생성자의 매개변수로 문자열 생성
   - new 예약어를 사용하여 객체를 생성하는 경우는 "abc" 문자열을 위한 메모리가 할당되고 새로운 객체가 생성됨
   - 생성자를 이용하지 않고 바로 문자열 상수를 가리키는 경우에는 str2가 기존에 만들어져 있던 "test"라는 문자열 상수의 메모리 주소를 가리키게 됨. 그러므로 계속해서 같은 주소값을 가짐
   - 프로그램에서 사용되는 상수값을 저장하는 공간을 상수 풀(constant pool) 이라고 함

2. String 클래스의 final char[] 변수

   - 자바는 String클래스를 제공해 char[] 배열을 직접 구현하지 않고도 편리하게 문자열을 사용할 수 있음
     최근 : finally byte[]
     - 문자열은 불변하는 특징
   - 프로그램에서 두 개의 문자열을 연결하면 둘 중에 하나의 문자열이 변경되는 것이 아니라 두 문자열이 연결된 새로운 문자열이 생성됨 (기존 문자열은 제거)
   - 그렇기 때문에 새로 생성되어 주소가 바뀜
   - 매번 문자열을 추가하면 새로운 객체가 만들어짐 -> 성능 저하

3. StringBuffer와 StringBuilder 클래스 활용하기

   - 버퍼 : 임시메모리 (문자열을 매번 생성하는 것이 아니라 임시공간을 만들어 놓고 그 버퍼 안에서 생성)
   - StringBuffer와 StringBuilder는 내부에 변경가능한 ( final이 아닌) char[](JDK12에서 byte[]로 변경)를 변수로 가지고 있음

   * 언제 사용하나요 ? / StringBuffer와 StringBuilder 클래스 차이점

   - 문자열 가감이 많은 경우 성능 저하를 막기 위해 사용
   - StringBuffer : 쓰레드 안전성이 있음 (동시성 작업시 안전)
   - StringBuilder : 쓰레으 안전성이 없음 (동시성 작업시 영향을 받음)
   - StringBuffer 클래스는 문자열이 안전하게 변경되도록 보장하지만, StringBuilder 클래스는 보장 되지 않음

   * 어떻게 사용하나요?

   - StringBuffer/StringBuilder 클래스를 생성하고 여기에 문자열을 추가(append)
     StringBuffer sb = new StringBuffer(100);
     sb.append("ABC");
   - 그러면 append() 메서드가 실행될 때마다 메모리가 새로 생성되는 것이 아니라, 하나의 메모리에 계속 연결되는 것을 해시 코드 값을 통해 알 수 있음
   - 연산 전 메모리 주소와 연산 후 메모리 주소가 같기 때문
   - 문자열을 변경한 후에 buffer에 toString() 메서드를 호출하면 다시 문자열로 반환할 수 있음 (이때 문자열을 Buffer에서 꺼낼 때 새로운 주소가 할당됨) String str = sb.toString();
   - 반환값이 this : 동일한 객체를 반환 (StringBuffer 그 자체) -> 메서드 체이닝 기법 의도
     StringBuffer sb = new StringBuffer(100);
     String str = sb.append("ABC").append("DEF").append("GHI").toString();

❤️ Wrapper 클래스 (기본형에 기능을 부여하여 객체로 만들어 주는 역할)

- 기본 자료형을 위한 클래스
  기본 자료형
  정수 : byte, short, int, long
  실수 : float, double
  논리 : boolean
  문자 : char

      - 재료가 되는 값

1. Wrapper 클래스의 종류

   - 기본 자료형의 값은 기능이 없음
   - 기본 자료형의 값을 처리하는 편의 기능 클래스

   byte -> Byte 클래스
   short -> Short 클래스
   int -> Integer 클래스
   long -> Long 클래스

   float -> Float 클래스
   double -> Double 클래스

   boolean -> Boolean 클래스
   char -> Character 클래스

   Wrapper 클래스가 존재하는 이유? - 기본형에 기능을 부여하기 위해 (원 재료는 기능이 없으므로 거기에 기능을 부여하기 위해 기본 값을 감싸줌)
   Wrapper 클래스의 형태? - 기본 값을 감싸는 형태

2. Integer 클래스 사용하기

   (1) Integer 클래스의 메서드

   - Integer 클래스는 정수에 특화된 기능을 제공하기 위한 목적임
   - 작은 수는 하나의 객체 공유, 수가 커지면 새로운 객체 생성
   - parse : 변환 (정수에 특화된 기능)
   - static int parseInt(...) : 문자열 숫자 -> int형 숫자로 변환
   - static Integer intvalue() : Integer 클래스 내부의 int 자료형 값을 가져오기 위해 사용 / Integer 클래스도 연산을 가능하게 해줌
   - static Integer valueOf(String str) : 정수나 문자열을 바로 Integer 클래스로 반환받을 수 있음

3. 오토박싱과 언박싱

   - 연산(+, -, \*, /, ...) : 숫자만. 기본 자료형만 가능한 연산, 같은 자료형끼리만 가능 (자동 형변환이 되어 계산됨) 객체끼리는 연산이 안됨
   - 오토박싱(autoboxing) : 기본형을 객체형으로 바꾸는 것
   - 언박싱(unboxing) : 객체를 기본형으로 꺼내는 것
   - 자바의 연산 방식이 변경된 것이 아니라 컴파일러가 변경하는 것
   - 따라서 객체의 형 변환에 신경 쓰지 않고 편리하게 프로그래밍 할 수 있게 됨

❤️ Class 클래스 (클래스의 구성 정보를 담고 있는 객체)

- 클래스의 정보가 담겨 있는 객체가 자동 생성 (Class 클래스 객체)
- class의 구성 정보를 담고 있는 정보성 객체
- 정보 확인용 객체 -> 이를 통해 구성요소 중 하나인 애노테이션 확인
- 자바의 모든 클래스와 인터페이스는 컴파일되고 나면 class 파일로 생성됨
- 이 class 파일에는 클래스나 인터페이스에 대한 변수, 메서드, 생성자 등의 정보가 들어 있음
- getclass()를 통해 가지고 올 수 있음

(1) Class 클래스를 선언하고 클래스 정보를 가져오는 방법

- 모든 클래스의 정적 변수 class
- 모두 자동으로 생성되며, 클래스의 구성정보를 확인할 수 있음

- Object 클래스에 정의된 getClass()

```Java
String s = new String();
Class c = s.getClass(); // getClass() 메서드 반환형은 Class

```

- 클래스 파일 이름을 Class 변수에 직접 대입

```Java
Class c = String.class;

```

- Class.forName("클래스 이름") 메서드 사용하기

```Java
Class c = Class.forName("java.lang.String");

```

(2) Class 클래스를 활용해 클래스 정보 알아보기

- Class 클래스와 java.lang.reflect 패키지에 있는 클래스를 활용하면 클래스 이름만 알아도 클래스의 생성자, 메서드 등의 정보를 알 수 있음

(3) Class.forName()을 사용해 동적 로딩 하기

- 대부분의 클래스 정보는 프로그램이 로딩될 떄 이미 메모리에 있음
- 프로그램 실행 이후 클래스의 로딩이 필요한 경우 동적 로딩(dynamic loading) 방식을 사용함
- 자바는 Class.forName() 메서드를 동적 로딩으로 제공함

```Java
Class pClass = Class.forName("classex.Person");

```

- forName() 메서드를 사용할 때 유의할 점
  - forName("클래스 이름")의 클래스 이름이 문자열 값이므로 문자열에 오류가 있어도(Person의 P가 소문자라든가) 컴파일할 때는 그 오류를 알 수 없음
  - 결국 프로그램이 실행되고 메서드가 호출될 때 클래스 이름에 해당하는 클래스가 없다면 ClassNotFoundException이 발생함
  - 따라서 동적 로딩 방식은 컴파일 할 때 오류를 알 수 없음
