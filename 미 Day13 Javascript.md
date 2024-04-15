<Day13 - 0404>
<Javascript>

이벤트 처리

1. 이벤트 처리기를 등록하는 방법

   - document 객체에 "on이벤트명" 속성에 이벤트 핸들러 함수를 직접 대입

   - 이벤트 처리기의 문제점

2. 이벤트 리스너를 등록하고 삭제하는 방법

- addEventListener를 사용해서 얻을 수 있는 장점
- addEventListener("이벤트 명", 이벤트 핸들러 함수, 캡쳐링 여부 - false (기본값))
  캡쳐링 여부 - false (기본값) : 버블링 단계에서 이벤트 전파 - true : 캡쳐링 단계에서 이벤트 전파
- removeEventListener 메서드로 이벤트 리스너 삭제하기

참고)

    이벤트 -> 비동기 방식

    동기 -> 순서대로 실행

    A -> B -> C

    지연 실행
    setTimeout(function() {
    	// 지연 실행할 코드
    }, 지연시간(1/1000초)

    5000 -> 5초 지연
    -> 반환값 -> 이벤트 핸들러 등록 ID

    clearTimeout(이벤트 핸들러 등록 ID); - 지연실행 취소

    지연 반복 실행
    setInterval(function() {
    	// 지연 반복 실행 코드

    }, 지연시간(1/1000초));

    반환값 -> 이벤트 핸들러 등록 ID

    clearInterval(이벤트 핸들러 등록 ID) - 지연반복실행 취소

이벤트 객체

1. 이벤트 객체의 공통 프로퍼티

2. 마우스 이벤트 객체

- 마우스 이벤트 객체에서 좌표를 담당하는 프로퍼티
- mouseenter, mouseleave
- mouseover, mouseout

3. 키보드 이벤트 객체
   keyup : 키를 눌렀다가 뗄때 발생
   keypress : 누르면 계속 이벤트가 발생
   keydown : 누르면 한번만 이벤트가 발생

   change : 키를 조작할때
   : select, input[type='file']- 파일을 선택, input[type='number|range']

이벤트 전파

1. 이벤트의 단계

1) 캡쳐링 단계
2) 타깃 단계
3) 버블링 단계

addEventListener(이벤트 타입, 이벤트 핸들러, 캡쳐링 여부);
캡쳐링 여부 - 기본값이 false - false : 이벤트 전파가 버블링 단계에서 발생 - true : 이벤트 전파가 캡쳐링 단계에서 발생

2. 이벤트 전파

1) 이벤트 전파 취소하기
   stopPropagation() : 이벤트 전파 취소

2) 이벤트 전파의 일시 정지
   stopImmediatePropagation()

3) 기본 동작 취소하기
   preventDefault()

3. 이벤트 리스너 안의 this

- event
  .target // 실제 클릭한 요소
  .currentTarget // 이벤트가 바인딩된 요소 === this

1. 이벤트 리스너 안의 this는 이벤트가 발생한 요소 객체
2. this가 원하는 객체를 가리키도록 설정하는 방법

- bind 메서드를 사용하는 방법
- 익명 함수 안에서 실행하는 방법
- 화살표 함수를 사용하는 방법
- addEventListener의 두 번째 인수로 객체를 넘기는 방법
  - handleEvent

https://developer.mozilla.org/ko/docs/Web/API/Fetch_API/Using_Fetch
