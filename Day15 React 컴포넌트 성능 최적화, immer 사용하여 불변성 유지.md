<Day15 - 0408>
<React 컴포넌트 성능 최적화, immer를 사용하여 불변성 유지>

# 컴포넌트 성능 최적화

const [todos, setTodos] = useState(cteateBulkTodos()); -> 매번 렌더링 될때마다 cteateBulkTodos 함수가 호출됨

1. ☆ 느려지는 원인 분석 ☆

① 컴포넌트는 다음과 같은 상황에서 리렌더링이 발생
   - 자신이 전달받은 props가 변경될 때
   - 자신의 state가 바뀔 때
   - 부모 컴포넌트가 리렌더링될 때
   - forceUpdate 함수가 실행될 때

2. ☆ React.memo를 사용하여 컴포넌트 성능 최적화 ☆

☆ React.memo ☆

- 컴포넌트의 리렌더링을 방지할 때는 shouldComponentUpdate라는 라이프사이클을 사용하면 됨
- 그러나 함수 컴포넌트에서는 라이프사이클 메서드를 사용할 수 없음
- 그 대신 ☆React.memo☆라는 함수를 사용할 수 있음
- 컴포넌트의 props가 바뀌지 않았다면, 리렌더링하지 않도록 설정하여 함수 컴포넌트의 리렌더링 성능을 최적화해 줄 수 있음

☆☆☆ React.memo로 항상 감싸기 (변경이 있을 때만 로딩되도록 하기 위해)

3. ☆ onToggle, onRemove 함수가 바뀌지 않게 하기 ☆

- 함수가 계속 만들어지는 상황을 방지하는 방법은 두 가지

① useState의 함수형 업데이트 기능을 사용하는 것
② useReducer를 사용하는 것

4. ☆ useState의 함수형 업데이트 ☆

- setTodos를 사용할 때, 새로운 상태를 파라미터로 넣는 대신 상태 업데이트를 어떻게 할지 정해주는 업데이트 함수를 넣어줄 수도 있음 
- 이를 ☆☆함수형 업데이트☆☆라고 함

const [number, setNumber] = useState(0);
// prevNumber는 현재 number 값을 가리킴
const onIncrease = useCallback(
() => setNumber(prevNumber => prevNumber + 1),
);

- setNumber(number+1)을 하는 것이 아니라, 어떻게 업데이트할지 정의해 주는 업데이트 함수를 넣어줌
- 그러면 useCallback을 사용할 때 두 번째 파라미터로 넣는 배열에 number를 넣지 않아도 됨

5. ☆ useReducer 사용하기 ☆

const [ state, dispatch함수 ] = useRedcuer( reducer함수, 초기state, 초기함수 )

반환되는 두 가지 값은 state와 dispatch 함수

state : 최신 state 스냅샷
dispatch함수 : 최신 state 스냅샷을 업데이트(값을 수정)할 수 있게 해주는 함수 (useState()에서 setState()함수와 비슷한 역할)

userReducer() 함수는 3개의 인수를 받음
① reducer함수 : dispatch함수가 작동하는 방식을 정의
② 초기state : 말 그대로 State의 초기 설정값을 정의
③ 초기함수 : 초기state를 설정하기 위해 실행해야 하는 함수. 예를 들어, http 리퀘스트를 받은 후에 초기 state를 설정해야 하는 상황일 때 유용

- useState의 함수형 업데이트를 사용하는 대신 useReducer를 사용해도 onToggle, onRemove가 계속 새로워지는 문제를 해결할 수 있음
- state가 엄청 많은 경우, state를 조작하는 수단이 너무 많은 경우, 어떤 state가 다른 state로부터 종속된 부분이 많은 경우 도움이 됨
- 두 번째 파라미터에 undefined를 넣고 세 번째 파라미터에 초기 상태를 만들어 주는 함수를 넣으면, 컴포넌트가 맨 처음 렌더링될 때만 함수가 호출됨
- useReducer를 사용하는 방법은 상태를 업데이트 하는 로직을 모아서 컴포넌트 바깥에 둘 수 있다는 장점이 있음

---

# react-virtualized를 사용한 렌더링 최적화

 yarn add react-virtualized

- 보이는 부분만 가지고 오는 것
- react-virtualized를 사용하면 리스트 컴포넌트에서 스크롤되기 전에 보이지 않는 컴포넌트는 렌더링하지 않고 크기만 차지하게끔 할 수 있음
- 만약 스크롤되면 해당 스크롤 위치에서 보여 주어야 할 컴포넌트를 자연스럽게 렌더링 시켜줌

---

# immer를 사용하여 불변성 유지하기

불변성 유지 : 기존값은 유지하면서 새로운값 만들기

- 알아서 새로운 객체로 만들어 준다

1. ☆ immer를 설치하고 사용법 알아보기 ☆

① 설치
   - yarn add immer

② immer 사용법
   import { produce } from 'immer';
   const nextState = produce(originalState, draft => {
   // 바꾸고 싶은 값 바꾸기
   draft.somewhere.deep.inside = 5;
   })

   - produce라는 함수는 두 가지 파라미터를 받음. 첫 번째 파라미터는 수정하고 싶은 상태이고, 두 번째 파라미터는 상태를 어떻게 업데이트할지 정의하는 함수임
   - 두 번째 파라미터로 전달되는 함수 내부에서 원하는 값을 변경하면, produce 함수가 불변성 유지를 대신해 주면서 새로운 상태를 생성해 줌
   - 이 라이브러리의 핵심은 '불변성에 신경 쓰지 않는 것처럼 코드를 작성하되 불변성 관리는 제대로 해주는 것'
   - 단순히 같은 곳에 위치하는 값을 바꾸는 것 외에 배열을 처리할 때도 매우 쉽고 편리함
   - immer를 사용하여 컴포넌트 상태를 작성할 때는 객체 안에 있는 값을 직접 수정하거나, 배열에 직접적인 변화를 일으키는 push, splice 등의 함수를 사용해도 무방함

2. ☆ useState의 함수형 업데이트와 immer 함께 쓰기 ☆

- immer에서 제공하는 produce 함수를 호출할 때, 첫 번째 파라미터가 함수 형태라면 업데이트 함수를 반환함