<Day29 - 0429>
<Day30 - 0430>
<JAVA 컬렉션 프레임워크>

# 컬렉션 프레임워크

❤️컬렉션 프레임워크란?

- 컬렉션(Collections) : 데이터 군, 데이터 군집, 자료
- 프레임워크(Framework) : 표준화된 설계
- 데이터 군을 다루는데 필요한 클래스를 표준화해서 설계

❤️컬렉션 프레임워크 핵심 ★인터페이스

1. List (중복을 허용하면서 저장순서가 유지)

   - 순차 자료 구조에 대한 설계
   - 순서가 있는 자료 (대표적인 예 -> 배열)
   - 순서가 가장 중요
   - 데이터의 중복을 허용
   - 메서드의 특정 순서에 추가하고 제거하고 변경하는 매개변수가 정의된 메서드가 많음 (int index...)

   추가

   - boolean add(E e)
   - boolean add(int index, E e)
   - boolean addAll(Collection<? extends E>...)
   - blooean addAll(int index, Collection)

   조회

   - E get(int index)
   - int indexOf(Object e) : 특정 요소의 위치 번호 (왼쪽 -> 오른쪽), 없을 때는 -1
   - int lastindexOf(Object e) : 특정 요소의 위치 번호 (오른쪽 -> 왼쪽), 없을 때는 -1
   - boolean contains(Object e)
   - boolean containsAll(Collection<?>..)

   수정

   - E set(int index, E e) : 특정 위치에 있는 요소를 변경

   삭제

   - E remove(int index) : 특정 순서 위치에 있는 요소 제거
   - boolean remove (Object e)
   - boolean removeAll (Collection...)

   기타

   - int size() : 요소의 갯수
   - void clear : 요소 비우기
   - retailAll(Collection ..) : 매개변수에 있는 값만 유지하고 모두 제거(교집합)

   구현된 클래스

   - 1. ArrayList
        : 배열을 구현한 클래스
        : 스택 구현 시 활용 가능
        : 쓰레드 안정성 확보 X
        : 기본 생성 배열 갯수 10, 공간의 갯수가 부족하면 -> 배열이 2배 크기로 새로 생성 -> 데이터의 양을 충분히 예상할 수 있는 경우는 충분한 크기를 만들어야 성능이 좋음
        : 내부에 생성된 배열(기본 공간의 갯수 10개)의 공간이 다 차면 2배로 늘어난다(새로운 배열이 생성)
        : 배열은 물리적으로 붙어 있는 나열구조 -> 순차 조회는 매우 빠름
        : 순서 위치가 바뀌는 변경, 수정, 삭제 -> 새로운 배열이 매번 생성됨 -> 성능 저하가 올 수 있음 (수정과 삭제를 하지 않는 단순 조회일 때 성능이 가장 좋음)
        : List 구현 클래스 중 가장 많이 사용함
        : stack 인터페이스의 구현체

   - 2. LinkedList
        : 다음 요소, 이전 요소를 가지고 서로 연결 관계 (물리적 순서가 아닌 논리적 순서로 되어있음)
        : 수정, 삭제 등 순서 위치가 자주 변경되는 자료에서 유리
        : 순서가 변경될 수 있는 수정, 삭제시에 빠름
        : 다음 요소의 위치 주소만 변경하면 되므로 성능 저하 X
        : 논리적 순서이므로 위치를 계산하는 일을 더 하므로 ArrayList보다는 조회에서 불리함
        : 자바는 DoublyLinkedList 형태로 구현되어 있음, 다음 요소, 이전 요소의 주소를 모두 가지고 있는 형태

        : Queue 인터페이스의 구현체
        boolean offer(E e) : 끝에 요소 추가
        E poll() : 앞에서 요소 꺼내기

        : Deque 인터페이스 (스택 + 큐)
        boolean offerFirst(E e) : 요소 앞에 추가
        boolean offerLast(E e) : 요소 끝에 추가
        E pollFirst() : 가장 앞의 요소를 꺼내기
        E pollLast() : 가장 뒤의 요소를 꺼내기
        peek() : 조회만 하는 용도

   - 3. Stack
        : E pop() : 끝 요소 꺼내기
        : E push(E e) : 끝에 추가

   - 4. Vector
        : ArrayList와 동일 / 배열을 구현한 클래스
        : 쓰레드 안정성 확보 O
        : ArrayList와 동일하게 사용하지만 과거 기능의 호환성 유지를 위해 남겨둠

2. Set (중복을 허용하지 않고 저장순서가 유지되지 않음)

   - 집합 자료 구조에 대한 설계
   - 중복이 없는 자료 (중복을 허용하지 X)
   - 순서 유지는 중요하지 않음
   - 중복 제거 기준 : 동등성 비교 - equals() and hashcode()

   추가

   - boolean add(E e)
   - boolean addAll(Collection..)

   삭제

   - boolean remove(Object e)
   - boolean removeAll(Collection..)

   기타

   - int size() : 요소의 갯수
   - void clear() : 전체 비우기
   - boolean contains(Object e)
   - boolean containsAll(Collection<?> ..)
   - boolean retainAll(Collection<?>) ..

   구현된 클래스

   - 1. HashSet
   - 2. TreeSet (정렬된 상태를 유지하기 때문에 단일 값 검색과 범위검색이 빠름)

   ★ 순서가 유지되지 않기 때문에 수정과 조회가 없음

3. Map (키는 중복될 수 없지만 값은 중복을 허용)

   - 키(key)와 값(value)의 쌍(pair)으로 이루어진 데이터의 집합
   - 사전 자료구조에 대한 설계
   - 순서는 유지되지 않음
   - 키는 중복을 혀용하지 않고 값은 중복을 허용함
   - 키 : 값을 찾기 위한 값 (중복 허용 X 집합자료)
   - 값 : 중복 허용 O
   - Interface Map<K,V> -> 여기서 K는 키(Key), V는 값(value)

   추가

   - V put(K key, V value) : key가 없을땐 추가, 있을땐 value값 수정
   - void putAll(Map..) : Map객체로 전체 추가시
   - V putIfAbsent(K key, V value) : key가 없을때만 value값 추가

   조회

   - V get(Object key) : key를 가지고 값 조회, 없을땐 null
   - V getOrDefault(Object key, V defaultValue) : key를 가지고 조회했을 때 값이 없으면 defaultValue로 대체

   ★ Set<Map.Entry<K,V>> entrySet() : 전체 키, 값의 쌍(Map.Entry) 조회

   수정

   - V put(K key, V value)
   - V replace(K key, V value)
   - boolean replace(K key, V value, V new Value) : 기존 값이 old value로 일치하는 경우에만 new Value로 변경

   삭제

   - V remove(Object key) : key를 가지고 제거
   - boolean remove(Object key, Object value) : key와 vale가 원래 삭제하려는 요소와 일치하는 경우에 삭제

   기타

   - size() : 요소의 갯수
   - Set<K> keySet() : Map에 포함되어 있는 키값만 추출
   - Collection<V> values() : Map에 포함되어 있는 값만 추출
   - boolean containsKey(Object key) : Map에 key가 포함되어 있는지 여부
   - boolean containsValue(Object value) : Map에 value가 포함되어 있는지 여부

   구현된 클래스

   - 1. HashMap : 순서 정렬은 되지 않음
   - 2. TreeMap : 키 값의 정렬기능이 추가
        : 기본 정렬 기준 : java.lang.Comparable / int compareTo(..)
        : 대안 기준 : java.util.Comparator / int compare(..)

- 컬렉션 프레임워크의 모든 컬렉션 클래스들을 List, Set, Map중 하나를 구현하고 있음
- 구현한 인터페이스의 이름이 클래스의 이름에 포함되어 있어서 이름만으로도 클래스의 특징을 쉽게 알 수 있도록 되어있음

❤️컬렉션 프레임워크의 주요 작업

- C(Create) : 데이터 추가
- R(Read) : 데이터 조회
- U(Update) : 데이터 변경
- D(Delete) : 데이터 삭제

2. Stack과 Queue

❤️Stack

- 스택(Stack)은 마지막에 저장한 데이터를 가장 먼저 꺼내게 되는 LIFO(Last In First Out)구조로 되어 있음
- 스택(Stack)은 동전 통과 같은 구조로 양 옆과 바닥이 막혀 있어 한 방향으로만 뺄수 있는 구조임
- 스택(Stack)에 0, 1, 2의 순서로 데이터를 넣으면 꺼낼 때는 2, 1, 0의 순서로 꺼내게 됨. 즉 넣은 순서와 꺼낸 순서가 바뀜
- 스택에는 ArrayList와 간은 배열기반의 컬렉션 클래스가 적합함

❤️ Queue

- 큐(Queue)는 처음에 저장한 데이터를 가장 먼저 꺼내게 되는 FIFO(First In First Out)구조로 되어 있음
- 큐(Queue)는 양 옆만 막혀 있고, 위 아래로 뚫려 있어서 한 방향으로는 넣고 한 방향으로는 빼는 파이프와 같은 구조로 되어 있음
- 큐(Queue)에 0, 1, 2의 순서로 데이터를 넣었다면 꺼낼 때 역시 0, 1, 2 순서로 꺼내게 됨. 순서의 변경 없이 먼저 넣은 것을 먼저 꺼내게 됨
- 큐는 ArrayList보다는 데이터의 추가/삭제가 쉬운 LinkedList로 구현하는 것이 더 적합함
- ArrayList와 같은 배열 기반의 컬렉션 클래스를 사용한다면 데이터를 꺼낼 때마다 빈 공간을 채우기 위해 데이터의 복사가 발생하므로 비효율적임

3. Iterator, ListIterator, Enumeration

- Iterator : 반복자 패턴 인터페이스
- (참고) : Enumeration 동일한 반복자 패턴 인터페이스, Iterator보다 먼저 등장

  Collection
  Iterator<E> iterator()

      Iterator
         - boolean hasNext() : 다음 요소가 있는지 체크
         - E next() : 다음 커서로 이동 요소를 조회

      ListIteraotr
          - List에 특화되어 있는 iterator / List 인터페이스에 정의
          - 순서에 대한 메서드가 정의
          - 순방향 조회 : hasNext(), next(), nextIndex()
          - 역방향 조회 : hasPrevious(), Previous(), PreviousIndex()

4. Comparator와 Comparable

(1) Comparable : 기본 정렬 기준 인터페이스

- java.lang.Comparable
- 기본 정렬 기준 : Natural Ordering

- int compareTo(T o)
  : 반환값이 양수이면 현재 객체를 뒤로 배치, T를 o 뒤에 배치
  : 반환값이 음수이면 현재 객체를 앞으로 배치, T를 o 앞에 배치
  : 반환값이 0이면 배치 하지 않음
  : 현재 객체의 정수 - 비교 객체의 정수 : 오름차순
  : 비교 객체의 정수 - 현재 객체의 정수 : 내림차순
  : return isbn - o.isbn; // 오름차순
  return o.isbn - isbn; // 내림차순

(2) Comparator : 대안적인 정렬 기준 인터페이스

- java.util.Comparator
  : int compare(T o1, T o2)

  - o1 정수 - o2 정수 : 오름차순
  - o2 정수 - o1 정수 : 내림차순

  - naturalOrder() : 기본 정렬 기준을 사용한 정렬(java.lang.Comparable, int compareTo(..))
  - reverserOrder() : 기본 정렬 기준의 반대

❤️ Arrays

- java.util.Arrays
- 배열의 편의 기능 모음

❤️ Collections

- java.util.Collections
- 컬렉션의 편의 기능 모음

(참고)

프레임워크 : 개발 방식의 틀을 정해 놓은 것 (틀이 정해져 있음)
(예) : 스프링 웹 MVC 프레임워크

라이브러리 : 편의 기능을 모은 것

자료 : 데이터 군집(Collection)
자료구조 : 자료를 어떻게 처리할 것인지 방법

- 순차 자료구조(List)
  -> 스택 자료구조 (Stack)
  -> 큐 자료구조 (Queue)
- 집합 자료구조(Set)
- 사전 자료구조(Map)

(참고2)

- 집합 : HashSet, TreeSet - 중복 제거 기준

  - equals() and hashCode()

- 정렬 : TreeSet - 기본 정렬 기준 (Natual Order)
  - java.lang.Comparable
  - int compareTo (T o)

(참고3) 💛💛💛💛💛

- 기준이 필요한 경우? => 애매할때, 정렬할때
- 정렬기준을 제공해야 정렬할 때 문제가 없음

- 기본 정렬 기준 : Natural Order
- 정렬기준 => java.lang.Comparable<T>

- java.lang.Comparable<T>에서 int compareTo(T o)로 기준을 정의함
- 기본적으로 오름차순을 많이 하지만 꼭 오름차순으로 고정은 아님
- 하지만 이런 기본적인 기준들이 보통 finall로 정의되어 있어서 상속과 변경이 불가함 (아닌 것도 있어서 final을 내가 붙일 수도 있음. String 클래스나 Integer클래스는 final이 정의되어 있음 wrapper클래스)

- 보통 기본정렬기준은 변경하지 않는데, 변경이 필요한 경우가 생기면 대안정렬기준을 사용
- 이럴 때 대안정렬기준을 사용 => java.util.Comparator
- java.util.Comparaotr에서는 compare(T o1, T o2)로 기준을 정함
- 하지만 java.util.Comparator에는 reverseOrder()라는 편의기능이 있어서 이것을 사용함

(참고4)

- Unsigned : 양수
- Unsigned Byte = 0 ~ 255
- deep : 다차원배열
- 자바에서 범위를 정의할 때 뒷 부분은 포함되지 않음

- Collection에는 list나 set의 구현객체가 모두 가능
- max는 정렬 후 가장 끝 값
- min은 정렬 후 가장 앞쪽 값
