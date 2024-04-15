<Day14 - 0405>
<React 라이프사이클 메서드>

# 라이프사이클 메서드의 이해

- 라이프사이클 메서드의 종류는 총 아홉 가지
- Will 접두사가 붙은 메서드는 어떤 작업을 작동하기 전★에 실행되는 메서드
- Did 접두사가 붙은 메서드는 어떤 작업을 작동한 후★에 실행되는 메서드
- 이 메서드들은 컴포넌트 클래스에서 덮어 써 선언함으로써 사용될 수 있음
- 라이프 사이클은 마운트, 업데이트, 언마운트 카테고리로 나눔
- 시점대로 호출되는 메서드가 있다고 보면 됨

1. ☆ 마운트 ☆

- DOM이 생성되고 웹 브라우저상에 나타나는 것을 마운트(mount)라고 함
- 화면에 처음 로딩 되었을 때 보이는 것

    ※ 마운트할 때 호출하는 메서드 ※

    ① constructor : 컴포넌트를 새로 만들 때마다 호출되는 클래스 생성자 메서드. 값을 초기화 할때 사용
        constructor(props) { ... }

    ② getDerivedStateFromProps : props에 있는 값을 state에 넣을 때 사용하는 메서드
    (prop는 객체 동결상태라 바뀌지 않음)
        static getDerivedStateFromProps(nextProps, prevState) {
        if (nextProps.value !== prevState.value) { // 조건에 따라 특정 값 동기화
        return { value: nextProps.value };
        }
        return null; // state를 변경할 필요가 없다면 null을 반환
        }

    ③ render : UI를 렌더링 하는 메서드
        render() { ... }

    ⑤ componentDidMount : 컴포넌트가 웹 브라우저상에 나타난 후 호출하는 메서드
        componentDidMount() { ... }

2. ☆ 업데이트 ☆

- 다시 렌더링 될 때 호출되는 것
- 컴포넌트는 다음과 같은 총 네 가지 경우에 업데이트됨

   ① props가 바뀔 때
   ② state가 바뀔 때
   ③ 부모 컴포넌트가 리렌더링될 때
   ④ this.forceUpdate로 강제로 렌더링을 트리거할 때

  - 컴포넌트는 다양한 이유로 업데이트 될 수 있음

   ① 부모 컴포넌트에서 넘겨주는 props가 바뀔때
   ② 컴포넌트 자신이 들고 있는 state가 setState를 통해 업데이트될 때
   ③ 부모 컴포넌트가 리렌더링될 때

  - 컴포넌트를 업데이트할 때는 다음 메서드를 호출함

   ① getDerivedStateFromProps
      - 이 메서드는 마운트 과정에서도 호출되며, 업데이트가 시작되기 전에도 호출됨
      - props의 변화에 따라 state 값에도 변화를 주고 싶을 때 사용

   ② shouldComponentUpdate
      - 컴포넌트가 리렌더링을 해야 할지 말아야 할지를 결정하는 메서드
      - true를 반환하면 다음 라이프사이클 메서드를 계속 실행하고, false를 반환하면 작업을 중지. 컴포넌트가 리렌더링되지 않음
      shouldComponentUpdate(nextProps, nextState) { ... }

   ③ render : 컴포넌트를 리렌더링

   ④ getSnapshotBeforeUpdate : 컴포넌트 변화를 DOM에 반영하기 바로 직전에 호출하는 메서드
      getSnapshotBeforeUpdate(prevProps, prevState) {
      if (prevState.array !== this.state.array) {
      const { scrollTop, scrollHeight } = this.list
      return { scrollTop, scrollHeight };
      }
      }
      - 이 메서드에서 반환하는 값은 componentDidUpdate에서 세 번째 파라미터인 snapshot 값으로 전달받을 수 있는데, 주로 업데이트하기 직전의 값을 참고할 일이 있을 때 활용

   ⑤ componentDidUpdate : 컴포넌트의 업데이트 작업이 끝난 후 호출하는 메서드
      componentDidUpdate(prevProps, prevState, snapshot) { ... }
      - 리렌더링을 완료한 후 실행
      - 업데이트가 끝난 직후이므로 DOM 관련 처리를 해도 무방
      - prevProps 또는 prevState를 사용하여 컴포넌트가 이전에 가졌던 데이터에 접근할 수 있음
      - getSnapshotBeforeUpdate에서 반환한 값이 있다면 snapshot 값을 전달받을 수 있음

3. ☆ 언마운트 ☆

- 컴포넌트가 제거될 때
- 마운트의 반대 과정, 즉 컴포넌트를 DOM에서 제거하는 것을 언마운트(unmount)라고 함

    ① componentWillUnmount : 컴포넌트가 웹 브라우저에서 사라지기 전에 호출하는 메서드.
    ② 컴포넌트를 DOM에서 제거할 때 실행
    ③ componentDidMount에서 등록한 이벤트 , 타이머, 직접 생성한 DOM이 있다면 여기서 제거 작업을 해야 함
      componentWillUnmount() { ... }

4. ☆ componentDidCatch 메서드 ☆

   ① 컴포넌트 렌더링 도중에 에러가 발생했을 때 애플리케이션이 먹통이 되지 않고 오류 UI를 보여 줄 수 있게 해 줌

   componentDidCatch(error, info) {
   this.setState({
   error: true
   });
   console.log({ error, info });
   }

   ② error는 파라미터에 어떤 에러가 발생했는지 알려줌
      .message : 에러 메세지

   ③ info 파라미터는 어디에 있는 코드에서 오류가 발생했는지에 대한 정보를 줌

   ④ 이 메서드를 사용할 때는 컴포넌트 자신에게 발생하는 에러를 잡아낼 수 없고 자신의 this.props.children으로 전달되는 컴포넌트에서 발생하는 에러만 잡아낼 수 있음

---

(참고)
   throw 에러 객체 -> 에러 발생
   Error 생성자로 생성한 객체
   throw new Error(메세지) -> 에러 발생, 실행 코드 중단

   에러객체.message : 메세지

   try {
   // 에러가 발생할 가능성이 있는 코드 (발생하면 throw ..)
   } catch(에러 객체) {
   // 에러 발생 시 처리할 대체 코드
   } finally {
   // 에러가 발생사든 하지 않든 무조건 실행되는 코드
   // 로그 기록
   }

   ★★★ 에러가 발생했을 때 중단되는 것을 방지하기 위해 에러처리 코드를 작성
   오류는 에러객체를 던져서 발생 -> 에러가 발생하면 서비스가 중단 -> 에러를 잡아야 함
   서비스 중단을 막기 위하여 에러처리를 한다 (try, catch가 바로 그 코드)

    에러 발생을 알려주는 법
    alert(err.message) -> 사용자
    console.err(err) -> 개발자
    // 대안적인 코드를 넣어야 한다

    미리캔버스, 캔바 -> 참고사이트

---

# 라이프사이클 메서드

    - ① render() 함수
            render() { ... }
            - 컴포넌트의 모양새를 정의
            - 라이프사이클 메서드 중 유일한 필수 메서드
            - 이 메서드 안에서 this.props와 this.state에 접근할 수 있으며, 리액트 요소를 반환함
            - 요소는 div 같은 태그가 될 수도 있고, 따로 선언한 컴포넌트가 될 수도 있음
            - 아무것도 보여 주고 싶지 않다면 null 값이나 false 값을 반환할 수 있음

    - ② constructor 메서드
            constructor(props) { ... }
            - 컴포넌트의 생성자 메서드로 컴포넌트를 만들 때 처음으로 실행됨
            - 이 메서드에서는 초기 state를 정할 수 있음

    - ③ getDerivedStateFromProps 메서드
            - props로 받아온 값을 state에 동기화시키는 용도로 사용하며, 컴포넌트가 마운트될 때와 업데이트될 때 호출됨

    - ④ componentDidMount 메서드
            componentDidMount() { ... }
            - 컴포넌트를 만들고 첫 렌더링을 다 마친 후 실행
            - 이 안에서 다른 자바스크립트 라이브러리 또는 프레임워크의 함수를 호출하거나 이벤트 등록, setTimeout, setInterval, 네트워크 요청 같은 비동기 작업을 처리

    - ⑤ shouldComponentUpdate 메서드
            shouldComponentUpdate(nextProps, nextState) { ... }
            - props 또는 state를 변경했을 때, 리렌더링을 시작할지 여부를 지정하는 메서드
            - 이 메서드에서는 반드시 true 값 또는 false 값을 반환해야 함
            - 이 메서드 안에서 현재 props와 state는 this.props와 this.state로 접근하고, 새로 설정될 props또는 state는 nextProps와 nextState로 접근할 수 있음

    - ⑥ getSnapshotBeforeUpdate 메서드
            - render에서 만들어진 결과물이 브라우저에 실제로 반영되기 직전에 호출됨
            - 주로 업데이트하기 직전의 값을 참고할 일이 있을 때 활용

    - ⑦ componentDidUpdate 메서드      
            componentDidUpdate(prevProps, prevState, snapshot) { ... }
            - 리렌더링을 완료한 후 실행
            - 업데이트가 끝난 직후이므로 DOM 관련 처리를 해도 무방함
            - prevProps 또는 prevState를 사용하여 컴포넌트가 이전에 가졌던 데이터에 접근할 수 있음
    - ⑧ componentWillUnmount 메서드
            componentWillUnmount() { ... }
            - 컴포넌트를 DOM에서 제거할 때 실행
            - componentDidMount에서 등록한 이벤트 , 타이머, 직접 생성한 DOM이 있다면 여기서 제거 작업을 함

    - ⑨ componentDidCatch 메서드
            - 컴포넌트 렌더링 도중에 에러가 발생했을 때 애플리케이션이 먹통이 되지 않고 오류 UI를 보여 줄 수 있게 해줌