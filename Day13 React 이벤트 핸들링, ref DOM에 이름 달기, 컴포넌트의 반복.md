<Day13 - 0404>
<React 이벤트 핸들링, ref: DOM에 이름 달기, 컴포넌트의 반복>

# 이벤트 핸들링

1. ☆ 리액트의 이벤트 시스템 ☆

- 이벤트 객체는 이벤트에 대한 정보가 담겨있음
- 리액트의 이벤트 시스템은 웹 브라우저의 HTML 이벤트와 인터페이스가 동일하기 때문에 사용법이 비슷함

(ex)

- onClick={...} -> 마우스 왼쪽
- onContextMenu -> 마우스 오른쪽 버튼
- onsubmit
- onSubmit = {...}
  (참고) 리액트의 submit은 양식을 제출하는 것이 아니라 수집하는 것임

- event
  - target
  - currentTarget === this

(참고) 리액트에서 지원하는 이벤트 종류

- Clipboard
- Composition
- Keyboard
- Focus
- Form
- Mouse
- Selection
- Touch
- UI
- Wheel
- Image
- Animation
- Transition

2. ☆ 이벤트를 사용할 때 주의사항 ☆

- 이벤트 이름은 카멜표기법으로 작성
- 이벤트에 실행할 자바스크립트 코드를 전달하는 것이 아니라, 함수 형태의 값을 전달
- DOM 요소에만 이벤트를 설정할 수 있음
  (div, input, ...)
- 컴포넌트에 자체적으로 이벤트를 설정할 수는 없지만, 전달받은 props를 컴포넌트 내부의 DOM 이벤트로 설정할 수 있음

3. ☆ 이벤트 핸들링 익히기 ☆

- onChange 이벤트 핸들링하기

① 컴포넌트 생성 및 불러오기
② onChange 이벤트 핸들링하기
③ state에 input 값 담기
④ 버튼을 누를 때 comment 값을 공백으로 설정
⑤ 이벤트에 실행할 자바스크립트 코드를 전달하는 것이 아니라, 함수 형태의 값을 전달

- ☆ 화살표 함수 형태로 메서드를 정의 ☆
- ☆ input 여러 개 다루기 ☆
- event 객체를 활용하는 것, e.target.name 값을 사용
- []는 변수명을 평가해서 접근할 때 사용

---

# ref: DOM에 이름 달기

1. ☆ ref는 어떤 상황에서 사용해야 할까? ☆

- HTML에서 DOM의 id는 유일(unique)해야 하는데, 어떤 상황에서는 중복 id를 가진 DOM이 여러개 생겨버릴 수 있음
- SPA (Single Page Application)
- ref는 전역적으로 작동하지 않고 컴포넌트 내부에서만 적용하기 때문에 이런 문제가 생기지 않음

① DOM을 꼭 직접적으로 건드려야 할 때
(어쩔 수 없이 DOM에 직접적으로 접근해야 하는데, 이를 위해 바로 ref를 사용)

- 특정 input에 포커스 주기
- 스크롤 박스 조작하기
- Canvas 요소에 그림 그리기

2. ☆ ref 사용 ☆

   - 콜백 함수를 통한 ref 설정
   - ref를 달고자 하는 요소에 ref라는 콜백 함수를 props로 전달해 주면 됨
   - 이 콜백 함수는 ref 값을 파라미터로 전달받음
   - 함수 내부에서 파라미터로 받은 ref를 컴포넌트의 멤버 변수로 설정해줌
   - input ref={(ref) => {this.input=ref}} />

   ① createRef를 통한 ref 설정
   input = React.createRef();
   <input ref={this.input} />
   - createRef를 사용하여 ref를 만드려면 우선 컴포넌트 내부에서 멤버 변수로 React.createRef()를 담아 주어야 함
   - 그리고 해당 멤버 변수를 ref를 담고자 하는 요소에 ref props로 넣어 주면 ref 설정이 완료됨
   - 설정한 뒤 나중에 ref를 설정해 준 DOM에 접근하려면 this.input.current를 조회하면 됨

   ② input에 ref 달기
   <input ref={(ref) => this.input=ref} ... />

   ③ 컴포넌트에 ref 달기

   - 컴포넌트 내부에 있는 DOM을 컴포넌트 외부에서 사용할 때 사용
   - 이 방식을 활용하면 MyComponent 내부의 메서드 및 멤버 변수에도 접근할 수 있음
   - 내부의 ref에도 접근할 수 있게 됨
     <MyComponent
     ref={(ref) => {this.myComponent=ref}}
     />

---

# useRef()

- currnet 속성을 접근
- 컴포넌트에서 사용할 지역변수
  (용도)
- 지역변수와 비슷하게 사용
- DOM을 선택할 때

---

# 컴포넌트

- 컨테이너 컴포넌트 : 데이터 처리, 이벤트 처리, 여러 프리젠테이셔널 컴포넌트를 포함

- 프리젠테이셔널 컴포넌트 : 보이는 화면 구성

- 모델 : 데이터 관련 로직

---

# 컴포넌트의 반복

1. ☆ 자바스크립트 배열의 map() 함수 ☆
  - 자바스크립트 배열 객체의 내장 함수인 map 함수를 사용하여 반복되는 컴포넌트를 렌더링할 수 있음
  - map 함수는 파라미터로 전달된 함수를 사용해서 배열 내 각 요소를 원하는 규칙에 따라 변환한 후, 그 결과를 새로운 배열로 생성함

  arr.map(callback, [thisArg])
  이 함수의 파라미터는 다음과 같음

  - callback : 새로운 배열의 요소를 생성하는 함수로 파라미터는 다음 세가지
    ★ currentValue : 현재 처리하고 있는 요소
    ★ index : 현재 처리하고 있는 요소의 index 값
    ★ array : 현재 처리하고 있는 원본 배열
    ★ thisArg(선택 항목) : callback 함수 내부에서 사용할 this 레퍼런스

2. ☆ key ☆
  - 리액트에서 key는 컴포넌트 배열을 렌더링했을 때 어떤 원소에 변동이 있었는지 알아내려고 사용함
  - key가 없을 때는 Virtual DOM을 비교하는 과정에서 리스트를 순차적으로 비교하면서 변화를 감지함
  - key가 있다면 이 값을 사용하여 어떤 변화가 일어났는지 더욱 빠르게 알아낼 수 있음
  - key 값은 언제나 유일해야 함. 따라서 데이터가 가진 고유값을 key 값으로 설정해야 함

---

# SPA와 MPA

- SPA(Single Page Application)
- MPA(Multi Page Application)

---

# react-icons 라이브러리 -> svg 이미지

yarn add react-icons

map => 변환 -> 새로운 배열 객체 반환
데이터 -> JSX

localStorage 객체

sessionStorage 객체

※ yarn create react-app exam03
※ react-icons
※ yarn add react-icons
