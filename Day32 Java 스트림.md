<Day32 - 0502>
<JAVA 스트림>

# 스트림(Stream)

❤️스트림이란?

- java.util.stream
  : 데이터 소스가 무엇이든 간에 같은 방식으로 다룰 수 있게 데이터를 추상화 하고 데이터를 다루는데 자주 사용되는 메서드들을 정의해 놓음
  : 배열이든, 컬렉션이든 Stream 객체로 변환하면 동일한 방식으로 처리 가능

  : 스트림은 데이터 소스를 변경하지 않는다.
  : 스트림은 일회용이다.(새로 만들어야 함)
  : 스트림은 작업을 내부 반복으로 처리한다.(for문을 거의 사라지게 만들었음)

- 출처가 달라도 스트림 방식으로 처리하면 동일하게 처리할 수 있음🤍🤍🤍
- 스트림은 한번 쓰면 다시 못 씀. 일회용 객체임. 스트림을 한번 더 쓰고 싶다면 한번 더 생성해야 함

❤️스트림의 목적

- 1. 데이터 소스가 무엇이든지간에(배열이든 컬렉션이든)
- 2. 스트림 객체가 되면 동일한 방식으로 처리할 수 있도록 하는 것
- 3. 데이터 군을 다룰 때 많이 사용하는 기능을 모아 놓은 인터페이스(편의기능)

❤️스트림의 특징

- 1. 내부 반복
- 2. 원본 소스를 변경X
- 3. 일회용

❤️스트림만들기(생성)

1. 컬렉션에서 생성하는 방법
   Collection 인터페이스 - Stream<E> stream()

   - 스트림은 List, Set의 구현 객체만 생성 가능
   - Stream stream()
   - 일반 스트림만 생성 가능 : Stream<E>
   - 숫자 관련 편의 기능이 필요한 경우?
     IntStream mapToInt(IntUnaryOperator) : Stream<Integer> -> IntStream
     Longtream mapToLong(LongUnaryOperator) : Stream<Long> -> LongStream

2. 배열에서 생성하는 방법
   Arrays

   - static stream(....)
   - Arrays.stream(..)

   기본 자료형 스트림(기본 스트림)

   - int[] 배열 -> IntStream
   - long[] 배열 -> LongStream
   - double[] 배열 -> DoubleStream

   T[] 배열 (참조 자료형 배열) -> Stream<T>

   기본 자료형 스트림에서 일반 스트림 (Stream<T>)에 있는 기능이 필요한 경우가 있음
   (예) IntStream : sorted() 기본정렬기준(java.lang.Comparable ...)만 정의되어 있다. -> 오름차순만 가능, 내림차순 정렬X
   그러나 일반 스트림 (Stream<Integer>)에는 sorted()외에도 sorted(Comparator..) 가 함께 정의되어 있다.
   -> 기본 자료형 스트림은 정렬 기준을 변경 못하지만 일반 스트림은 기준을 변경할 수 있다.
   -> 일반 스트림(Stream<Integer>)의 기능을 사용하기 위해서 기본 자료형 스트림(IntStream)을 일반 스트림(Stream<Integer>)로 변환할 필요가 있다.
   -> boxed()메서드를 통해서 변경 가능

   IntStream ... box

3. 일반 : Stream, 기본 : IntStream, LongStream, DoubleStream
   - static of(T... )

(참고)
JDK8 부터
of(...) : 객체 생성 메서드
stream 객체를 나열식으로 만들 수 있음

❤️스트림의 연산

1. 중간연산

   - 스트림 중간 부분에 정의된 메서드
   - 반환값이 Stream인 형태인 경우(일반 스트림 - Stream<E>, 기본 자료형 스트림 - IntStream, LongStream, DoubleStream)
   - 최종 연산이 호출될때까지는 연산이 되지 않음
   - 최종연산이 호출되어야 수행되는 연산
   - 처리할 작업을 나열하듯이 정의 - 메서드 체이닝

2. 최종연산

   - 가장 끝에 추가된 메서드인 경우가 많음
   - 반환값이 Stream이 아닌 형태
   - 스트림이 소비되면서 연산이 수행되고 작업이 완료
   - 반환값이 Stream이 아닌 경우 (int, long, boolean, Optional ...)

3. 지연된연산 = 중간연산
   중간 연산은 최종 연산이 호출되어야 스트림을 소비하면서 연산이 진행됨. 중간연산을 지연된 연산이라고 하기도 함

💛Stream 문서를 보고 반환값에 stream이 들어 있으면 중간연산에 나열하여 사용할 수 있고, 반환값에 stream이 없으면 최종연산에 사용하여 연산을 함(마지막에 최종연산이 호출되어야 연산이 진행됨)🤍🤍🤍

❤️기본자료형을 다루는 스트림

IntStream
LongStream
DoubleStream

-> 숫자(정수, 실수) 관련 편의 기능 제공 (일반 스트림은 숫자가 아닌 다른 자료형도 다루므로 숫자에 한정한 기능은 제공X)
-> 오토박싱, 언박싱이 발생 X -> 성능상 이점
-> 숫자 관련 편의 기능 추가(예 - 통계 관련 기능)
-> 통계에 관련된 기능이 탑재
-> 연산 성능 향상

❤️일반 스트림 -> 기본 자료형 스트림으로 변환 메서드
mapTo.. 로 만든다

mapToInt : IntStream
mapToLong : LongStream
mapToDouble : DoubleStream

❤️기본 자료형 스트림 -> 일반 스트림 변환 메서드
boxed()로 만든다

(예) IntStream -> Stream<Integer>
LongStream -> Stream<Long>

IntStream에는 정렬 기능 sorted() 메서드가 1개만 정의 <-- 기본 정렬 기준 정렬(java.lang.Comparable..)
-> 그러면 기본 정렬 기준 외에 다른 기준으로 정렬은 안되나?

그런데 일반 스트림 Stream에서는 sorted()와 sorted(Comparator..)가 정의되어 있다.

그러면 IntStream을 일반 스트림인 Stream<Integer>로 변환하면 sorted(Comparator...) 통해서 정렬을 바꿀수 있지 않을까?

(참고)
IntStream
static IntStream range(시작번호, 종료 번호(미만))
rangeClosed(시작번호, 종료 번호(이하))
IntSummaryStatistics summaryStatistics()

❤️스트림 활용

1. 🤍생성하기
   Collection::stream() : 일반 스트림
   Arrays.stream(...) : 일반스트림 + 기본 자료형 스트림

   Stream.of(T.... ) : 일반스트림, 기본 자료형 스트림

1) 특정 범위의 정수
   기본 자료형 스트림
   range(....)
   rangeClosed(...)

2) 임의의 수
   java.util.Random
   무한 스트림 - 갯수 제한이 필요
   IntStream ints(); : 정수범위 난수
   LongStream longs() :
   DoubleStream doubles() : 실수 범위 난수

3) 람다식 - iterate(), generate()

   - 무한스트림

4) 두 스트림의 연결 - concat()

2. 🤍스트림의 중간 연산

1)  skip(), limit()

limit() : 갯수 제한
skip() : 건너 뛰기

2. filter(), distinct()
   filter(Predicate<T> ...) : 스트림을 걸러주는 기능

distinct() : 중복 제거 - 중복 제거 기준 : equals() and hashCode()

3. sorted()
   - 정렬 : 기본 정렬 기준 java.lang.Comparable int compareTo(...)
   - sorted(Comparator ....)
     - 대안적인 기준 : java.util.Comparator :: int compare(....)
4. map()
   map(Function<T,R> ...) : 변환 메서드
5. peek()

   - forEach와 매개변수가 동일
   - Stream peek(Consumer<T> ... ) : 중간 연산 : 중간에 값을 확인할 경우 많이 사용
   - void forEach(Consumer<T> ...) : 최종 연산 : 최종적으로 출력할때 사용

6. mapToInt(), mapToLong(), mapToDouble()

Optional 클래스

- JDK8
- null에 대한 다양한 처리 방법을 제공하는 클래스
- Wrapper 클래스

class Optional<T> {
...
private final T value;
...
}

1. Optional 객체 생성하기
   static Optional<T> of(T t) : t가 null이면 오류 발생
   static Optional<T> ofNullable(T t) : t가 null이어도 오류 발생 X
2. Optional 객체의 값 가져오기

   T get() : null 이면 오류 발생
   T orElse(T other) : null이 아니면 값 반환, null이면 other 반환
   T orElseGet(Supplier<T ... > )
   T orElseThrow() : null이면 예외 발생
   T orElseThrow(Supplier<T ... > )

3. OptionalInt, OptionalLong, OptionalDouble

- 기본형을 처리하는 Optional 클래스
- 오토박싱, 언박싱이 발생 X -> 성능상의 이점

3. 스트림의 최종 연산

- 최종 연산이 호출되어야 중간 연산도 수행, 스트림을 소비

1. forEach()

2. allMatch(), anyMatch(), noneMatch(), findFirst(), findAny()

boolean allMatch(Predicate ... ) : 전부 참인 경우 참
boolean anyMatch(Predicate ...) : 어떤 것이든 하나라도 참이면 참
boolean noneMatch(Predicate ...) : 전부 거짓일때 참
T findFirst() : 가장 첫번째 스트림의 요소를 반환

3. count(), sum(), average(), max(), min()

4. reduce()

5. collect()
   Collector

   java.util.stream.Collectors 6) toList(), toSet(), toMap(), toCollection(), toArray() - toMap() : - toCollection() : List, Set의 하위 클래스 객체 7) joining()

6. groupingBy(), partitioningBy()
