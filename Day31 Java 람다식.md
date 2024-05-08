<Day31 - 0501>
<JAVA 람다식>

# 람다식

❤️람다식이란?

- 자바의 함수는 객체가 아니기 때문에 값으로 사용이 불가한데, 이를 매개변수로 이용하기 위해 인터페이스의 객체가 되는 조건을 이용하여 비슷하게 흉내내었다.
- 하지만 이것은 용도가 제한적이고 내가 정의한 기능을 사용하는 것이고 일회용 객체이기 때문에 형식을 단순화 하기 위해 도입된 것이 람다식이다.
- 근데 굳이 함수를 왜 매개변수로 쓰냐고 하면 ? - 필요에 의해 내부에서 사용자 정의 기능을 만들기 위해서이다 (함수형 프로그래밍)

- 메서드(함수)를 하나의 식으로 표현

  - 함수형 프로그래밍

    🤍함수란?
    : 하나의 기능(단일기능) -> 역할이 하나다

    🤍일등함수?
    : 함수 == 변수 / 함수가 값으로 사용 (매개변수나 반환값으로 사용 가능)

    🤍함수를 매개변수로 사용하는 이유?
    : 사용자 정의기능을 만들기 위해
    : 필요에 의해 내부에서 함수의 기능을 정의할때 사용함
    : 필요에 의한 하나의 기능만을 수행하며 용도가 매우 제한적임
    : 하나의 기능(단일기능) -> 역할이 하나. 중괄호 안쪽에 하나(?)

    🤍함수는 값으로 사용
    : 매개변수 - 사용자 정의 기능
    : 반환값 - (참고) 자바스크립트 - 클로저(외부의 값이 내부에 속박되는 상태) + 팩토리 함수(새로운 함수를 만드는 함수)

  💛자바의 함수는 실행코드임
  💛자바는 함수는 값으로 사용 불가 -> 인터페이스의 객체가 되는 조건을 이용하여 비슷하게 흉내냄(매개변수로 이용하기 위해) -> 형식을 단순화(용도가 제한적이고 특수한 상황에서 사용되고 내가 정의한 기능을 사용하는 것이고, 일회용 객체이기 때문에 형식을 단순화 하기 위해 람다식 도입)

❤️람다식 문법 살펴보기

- 메서드를 하나의 식으로 짧게 표현한 문법 / 용도가 제한적이므로 굳이 길게 작성 하지 않음 -> 최대한 짧게 쓰는 것이 가장 좋은 방식
- 추상메서드의 기능을 하나만 정의함. 역할을 하나만 수행하기 위해 (제한조건)
- 하나의 인터페이스 안에 하나의 추상메서드만 정의 (함수형 인터페이스)

1.  접근 제어자, 반환값 타입, 함수명을 생략
2.  매개변수 정의 부분과 함수 구현 부분({ }) 사이에 -> 추가
3.  매개변수의 자료형 생략 가능
4.  구현코드가 한줄일때는 { ... } 생략 가능, return 예약어도 생략 가능
5.  최대한 짧게 쓰는 방향(변수명도 한 글자로 하는 것이 권장)

```Java

기존 메서드 방식
public int square(int num) {return num * num;}

람다식 방식
int square = x -> x * x;  // square.square(10)

```

```Java

기존 메서드 방식
IntUnaryOperator oper = new IntUnaryOperator() {

   public int apply(int num) {
      return num * num;
   }
};

람다식 방식
IntUnaryOperator oper = x -> x * x;
int result = oper.apply(10);

```

❤️함수형 인터페이스(Functional Interface)

- 단일 기능🤍, 단일 역할🤍, 하나의 역할만 수행할 수 있는 형식상 제한 조건이 있음 : 추상메서드를 1개만 정의
- 명확한 형식 제어를 위한 애노테이션 @functionalInterface (꼭 붙여야 함)

❤️java.util.function패키지💜💜💜💜💜 꼭 암기하기

- 함수의 유형을 정의한 인터페이스
- 자주 사용하는 함수 유형의 인터페이스 정의

1. 매개변수가 X, 반환값 O (1개) - 투입되는 것은 없고 나가는 것만 있음
   Supplier<T>
   : T get()

2. 매개변수가 1개, 반환값 X - 투입되는 것만 있고 나가는 것은 없음
   Consumer<T>
   : void accept(T t)

3. 매개변수가 1개 반환값 O (1개) - 투입되는 것도 있고 나가는 것도 있음
   Function<T,R>
   : R apply(T t)

4. 매개변수가 1개, 반환값은 boolean(논리값) - 판별식
   Predicate<T>
   : boolean test(T t)

매개변수 2개 - Bi 접두어가 추가

1. 매개변수가 2개, 반환값 X
   BiConsumer<T, U>
   : void accept(T t, U u)

2. 매개변수가 2개, 반환값 O (1개)
   BiFunction<T,U,R>
   : R apply(T t, U u)

3. 매개변수가 2개, 반환값 boolean
   BiPredicate<T, U>
   : boolean test(T t, U u)

❤️매개변수와 반환값 타입이 같은 자료형인 경우

매개변수가1, 반환값1 -> 자료형이 모두 동일
UnaryOperator<T> ---> 상위 인터페이스 Function<T, T>
T apply(T t)

매개변수가 2개, 반환값1 -> 자료형이 모두 동일
BinaryOperator<T> ---> 상위 인터페이스 BiFunction<T, T, T>
T apply(T t1, T t2)

❤️기본형 타입의 함수형 인터페이스

- LongToIntFunction - long 매개변수 타입으로 들어오고 int 반환값 타입으로 나감
- ToLongFunction<T> - <T> 매개변수 타입으로 들어오고 Long 반환값 타입으로 나감
- DoubleToLongFunction - double 매개변수 타입으로 들어오고 long 반환값 타입으로 나감
- IntFunction<R> - int 매개변수 타입으로 들어오고 <R>반환값 타입으로 나감

❤️Function의 합성과 Predicate의 결합

- 함수의 결합

🤍Function (함수를 결합)

- ❗ andThen(Function ... )
  f.andThen(g) -> f -> g

- ❗ compose(..)
  g.compose(f) -> f -> g

🤍Predicate (조건식, 논리 연산과 관련)

- and : 둘다 참인 조건을 결합
- or : 둘중에 하나가 참인 조건을 결헙
- negate : 참을 거짓으로 거짓참으로 바꾸어주는 조건

❤️메서드 참조

- 람다식을 더욱 간결하게 표현
- 클래스명::메서드명
- 참조변수::메서드명

```Java
   Supplier<Book> s1 = () -> new Book();
   Supplier<Book> s2 = Book::new;

   ToIntFunction<String> func1 = s -> s.length();
   ToIntFunction<String> func2 = String::length;
```

(참고)
지네릭타입 : 참조자료형, 배열, 기본형X
Java.util.function 문서 많이 참고하기
