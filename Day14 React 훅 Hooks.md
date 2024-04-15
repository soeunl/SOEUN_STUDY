<Day14 - 0405>
<React 훅 Hooks>

# Hooks

## use로 시작하는 함수

1. ☆ UseState ☆

   import { useState } from 'react';
   const [value, setValue] = useState(0);

   - useState는 가장 기본적인 Hook이며, 함수 컴포넌트에서도 가변적인 상태를 지닐 수 있게 해줌
   - 함수 컴포넌트에서 상태를 관리해야 한다면 이 Hook을 사용하면 됨
   - 첫 번째 원소는 상태 값, 두 번째 원소는 상태를 설정하는 함수
      const[items, setItems] = useState(기본값);
   - 상태를 설정하는 함수에 파라미터를 넣어서 호출하면 상태값이 변경되고 컴포넌트가 리렌더링 됨
      setItems(값);
      setItems((기존 상태값) => ...);

2. ☆ useEffect ☆

   import { useState, useEffect } from 'react';

   - 리액트 컴포넌트가 렌더링될 때마다 특정 작업을 수행하도록 설정할 수 있는 Hook
   - 클래스형 컴포넌트의 componentDidMount(상태값 변경)와 componentDidUpdate(상태가 바뀌었을 때 호출)를 합친 형태로 보아도 무방 (두 가지의 역할을 다 한다)
   - 마운트될 때만 실행하고 싶을 때 함수의 두 번째 파라미터로 비어 있는 배열을 넣어 주면 됨
   - useEffect는 기본적으로 렌더링되고 난 직후마다 실행되며, 두 번째 파라미터 배열에 무엇을 넣는지에 따라 실행되는 조건이 달라짐
   - 컴포넌트가 언마운트되기 전이나 업데이트되기 직전에 어떠한 작업을 수행하고 싶다면 useEffect에서 뒷정리(cleanup) 함수를 변환해 주어야 함
   - usecallback과 같이 사용

3. ☆ useReducer ☆

   import { useReducer } from 'react';
   function reducer(state, action) {
	return { ... }; 
   // 불변성을 지키면서 업데이트한 새로운 상태를 반환
   }

   - 리듀서는 현재 상태, 그리고 업데이트를 위해 필요한 정보를 담은 액션(action) 값을 전달받아 새로운 상태를 반환하는 함수
   - 복잡한 로직에 사용
   - useState보다 더 다양한 컴포넌트 상황에 따라 다양한 상태를 다른 값으로 업데이트해 주고 싶을 떄 사용하는 Hook
   - 리듀서 함수에서 새로운 상태를 만들 때는 반드시 불변성을 지켜 주어야 함
   - 리덕스(redux)에서도 비슷하게 사용 : 전역 상태 관리
   - 바깥에서 한번만 정의

4. ☆ useMemo ☆

   import { useState, useMemo } from 'react';

   - 메모제이션 기법, 캐싱
   - 함수 컴포넌트 내부에서 발생하는 연산을 최적화
   - 렌더링하는 과정에서 특정 값이 바뀌었을 때만 연산을 실행하고, 원하는 값이 바뀌지 않았다면 이전에 연산했던 결과를 다시 사용하는 방식
   - 연산결과에 사용
   - 내부에 최초의 계산 결과 값 한번만 저장하고 필요할 때 계속 호출해서 사용
   - 함수호출할 때 값을 이용

   function factorial(num) {
   if (num<1) {
   return 1;
   }
   return num ＊ factorial(num-1)
   }

5. ☆ useCallback ☆

   - useCallback은 useMemo와 상당히 비슷한 함수
   - 주로 렌더링 성능을 최적화해야 하는 상황에서 사용됨
   - 이 Hook을 사용하면 만들어 놨던 함수를 재사용할 수 있음
   - useCallback의 첫 번째 파라미터에는 생성하고 싶은 함수를 넣고, 두 번째 파라미터에는 배열을 넣으면 됨
   - 함수형 업데이트를 사용하는 것이 좋다
   - 함수를 정의할 때 계속 이용

6. ☆ useRef ☆

   - useRef Hook은 함수 컴포넌트에서 ref를 쉽게 사용할 수 있도록 해줌
   - 컴포넌트 로컬 변수를 사용해야 할 때도 useRef를 활용할 수 있음
   - 로컬 변수란 렌더링과 상관없이 바뀔 수 있는 값을 의미함

---

   (참고)
   부모컴포넌트가 렌더링 되면 자식 컴포넌트도 자동으로 갱신됨
   React.memo(컴포넌트) - 자식 컴포넌트에서 변화가 없을때는 갱신되지 않도록 해주는 기능. 성능을 위해