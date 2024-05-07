<Day12 - 0403>
<React 이벤트 핸들링, 처리, 전파, 비동기처리 >

# 이벤트 핸들링

1. 리액트의 이벤트 시스템

- 웹 브라우저의 HTML 이벤트와 인터페이스가 동일하기 때문에 사용법이 비슷함

2. 이벤트를 사용할 때 주의사항

- 이벤트 이름은 카멜표기법으로 작성
- 이벤트에 실행할 자바스크립트 코드를 전달하는 것이 아니라, 함수 형태의 값을 전달
- DOM 요소에만 이벤트를 설정할 수 있음

3. 이벤트 핸들링 익히기

- onChange 이벤트 핸들링하기

  (1) state에 input 값 담기
  (2) 버튼을 누를 때 comment 값을 공백으로 설정
  (3) 이벤트에 실행할 자바스크립트 코드를 전달하는 것이 아니라, 함수 형태의 값을 전달
  (4) 화살표 함수 형태로 메서드를 정의
  (5) input 여러 개 다루기

- event 객체를 활용하는 것, e.target.name 값을 사용
- props - 부모가 넘겨주는 값
- state - 현재 컴포넌트 안에서 사용할 값

# 이벤트 처리

1. 이벤트 처리기를 등록하는 방법

- document 객체에 "on이벤트명" 속성에 이벤트 핸들러 함수를 직접 대입
- 이벤트 처리기의 문제점

2. 이벤트 리스너를 등록하고 삭제하는 방법

- addEventListener를 사용해서 얻을 수 있는 장점
- addEventListener("이벤트 명", 이벤트 핸들러 함수, 캡쳐링 여부 - false (기본값))
  캡쳐링 여부 - false (기본값) : 버블링 단계에서 이벤트 전파
- true : 캡쳐링 단계에서 이벤트 전파
- removeEventListener 메서드로 이벤트 리스너 삭제하기

# 이벤트 객체

1. 이벤트 객체의 공통 프로퍼티
2. 마우스 이벤트 객체

- 마우스 이벤트 객체에서 좌표를 담당하는 프로퍼티
  : mouseenter, mouseleave
  : mouseover, mouseout

3. 키보드 이벤트 객체
   : keyup => 키를 눌렀다가 뗄때 발생
   : keypress => 누르면 계속 이벤트가 발생
   : keydown => 누르면 한번만 이벤트가 발생

   : change => 키를 조작할 때
   -> select, input[type='file'] - 파일을 선택, input[type='number|range']

# 이벤트 전파

1. 이벤트의 단계

(1) 캡쳐링 단계
(2) 타깃 단계 - 이벤트 실행
(클릭전파)
(3) 버블링 단계
(클릭전파)

addEventListener(이벤트 타입, 이벤트 핸들러, 캡처링 여부);

- 캡쳐링 여부

* 기본값이 false
* false : 이벤트 전파가 버블링 단계에서 발생
* true : 이벤트 전파가 캡처링 단계에서 발생

2. ★★★ 이벤트 전파 ★★★

(1) 이벤트 전파 취소하기
stopPropagation() : 이벤트 전파 취소

(2) 이벤트 전파의 일시 정지
stopImmediatePropagation()

(3) 기본 동작 취소하기
preventDefault()

3. 이벤트 리스너 안의 this

- event
  .target (이벤트가 발생한 요소. 실제 클릭한 요소)
  .currentTarget (이벤트 핸들러가 등록된(부여된, 바인딩된) 요소) === this

(1) 이벤트 리스너 안의 this는 이벤트가 발생한 요소 객체★
(2) this가 원하는 객체를 가리키도록 설정하는 방법

- bind 메서드를 사용하는 방법
  :
- 익명 함수 안에서 실행하는 방법
- 화살표 함수를 사용하는 방법
- addEventListener의 두 번째 인수로 객체를 넘기는 방법
- handleEvent

# 비동기 처리

- 순서대로 실행되지 않음
- 순서가 보장되지 않음
- setTimeout
  function work(title, time) {
  setTimeout(function() {
  console.log(title);
  }, time)
  }

  work("A작업". 5000);
  work("B작업". 1000);
  work("C작업". 3000);

  이벤트 -> 비동기 방식

  동기 -> 순서대로 실행

  A -> b -> C

# 지연 실행

setTimeout(function() {
//지연 실행할 코드
}, 지연시간(1/1000초))

5000 -> 5초 지연
-> 반환값 -> 이벤트 핸들러 등록ID

clearTimeout(이벤트 핸들러 등록ID);

clearTimeout(timeoutind);

# 지연 반복 실행

- setInterval(function() {
  // 지연 반복 실행 코드
  }, 지연시간(1/1000초));

  반환값 -> 이벤트 핸들러 등록ID

  clearInterval(이벤트 핸들러 등록ID) - 지연반복실행 취소

# 데이터 영역 (정적 메모리. 한번 설정되면 변경되지 X)

- 변경되지 않는 부분
- 작성한 코드
- 상수
- 메서드 ..

동적 메모리

- 스택영역

- 힙 영역

메모리에 할당을 해야지만 계산이 가능하다
결과값도 공간이 있어야만 담을 수 있다
함수 연산이 끝나고 작업할 것이 없어지면 메모리는 사라진다
