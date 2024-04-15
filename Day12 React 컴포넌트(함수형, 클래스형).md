<Day12 - 0403>
<React 컴포넌트(함수형 컴포넌트, 클래스형 컴포넌트)>

# 컴포넌트

- 컴포넌트에는 함수형 컴포넌트와 클래스형 컴포넌트가 있음

★ 컴포넌트란?

- 프로그래밍에 있어 ☆ 재사용이 가능한 각각의 독립된 모듈 ☆
- 유저가 사용하는 시스템에 대한 조작장치 (header bar, navbars, button 등)
- 실행 중인 소프트웨어의 활동 단위 (런타임 개체를 참조하고 가시성이 없는 단위)
- 쉽게 말해 함수라고 보면 됨

* 컴포넌트를 만들 때 반드시 가장 첫 글자는 대문자로 만들어야 함
* 폴더는 소문자로 시작하는 카멜케이스로 작성하고, 컴포넌트를 만드는 파일은 대문자로 시작하는 카멜케이스로 이름을 지어줌

★ 모듈이란?

- 만들어진 산출물의 구현 단위

1. ☆ 클래스형 컴포넌트 ☆

   import { Component } from 'react';

   class App extends Component {
   render() {
   const name = 'react';
   return <div className="react">{name}</div>;
   }}

   export default App;

2. ☆ 함수형 컴포넌트 ☆

   import './App.css';

   function App() {
   const name = '리액트';
   return <div className="react">{name}</div>
   }

   export default App;

- 함수형 컴포넌트에는 state가 없음
- React hook을 사용하면 함수형 컴포넌트에서도 state를 사용할 수 있지만, hook 없이 state를 사용할 수 없음

---

# 첫 컴포넌트 생성

0. ☆ 코드 작성하기 ☆
   <MyComponent.js>
   const MyComponent = () => {
   return <div>나의 새롭고 멋진 컴포넌트</div>;
   };

   export default MyComponent;

1. ☆ 모듈 내보내기(export) ☆
   export default MyComponent;

2. ☆ 모듈 불러오기(import) ☆
   <App.js>
   import MyComponent from './MyComponent';

   const App = () => {
   return <MyComponent />;
   };

   export default App; 3. ☆ props ☆

3. ☆ props ☆

- props는 properties를 줄인 표현으로 컴포넌트 속성을 설정할 때 사용하는 요소
- props 값은 해당 컴포넌트를 불러와 사용하는 ★부모 컴포넌트★에서 설정할 수 있음

3. ☆ JSX 내부에서 props 렌더링 ☆

   <MyComponent.js>
   const MyComponent = props => {
   return <div>안녕하세요. 제 이름은 {props.name}입니다.</div>;
   };

export default MyComponent;

4.  ☆ 컴포넌트를 사용할 때 props 기본값 설정: defaultProps ☆

    <App.js>
    import MyComponent from './MyComponent';

    const App = () => {
    return <MyComponent name="React" />;
    };

    export default App;
    props 기본값 설정: defaultProps

    <MyComponent.js>
    const MyComponent = props => {
    return <div>안녕하세요. 제 이름은 {props.name}입니다.</div>;
    };

    MyComponent.defaultProps = {
    name: '기본 이름'
    };

    export default MyComponent;

5.  ☆ children ☆

    - 컴포넌트 태그 안에 정의된 내용을 보여줌
      <MyComponent>....</MyComponent>

    <App.js>
    import MyComponent from './MyComponent';

    const App = () => {
    return <MyComponent>리액트</MyComponent>;
    };

    export default App;

    <MyComponent.js>
    const MyComponent = props => {
    return (
    <div>
    안녕하세요. 제 이름은 {props.name}입니다. <br />
    children 값은 {props.children}입니다.
    </div>
    );
    };

    MyComponent.defaultProps = {
    name: '기본 이름'
    };

    export default MyComponent;

6.  ☆ 비구조화 할당 문법을 통해 props 내부 값 추출하기 ☆

    <MyComponent.js>
    const MyComponent = props => {
    const { name. children } = props;
    return (
       <div>
       안녕하세요. 제 이름은 {name}입니다. <br />
       children 값은 {children}입니다.
       </div>
       );
       };

    MyComponent.defaultProps = {
    name: '기본 이름'
    };

    export default MyComponent

    - 함수 파라미터가 객체라면 그 값을 바로 비구조화해서 사용할 수 있음

    <MyComponent.js>

    const MyComponent = ({ name, children }) => {
    return (
    <div>
    안녕하세요. 제 이름은 {name}입니다. <br />
    children 값은 {children}입니다.
    </div>
    );
    };

    MyComponent.defaultProps = {
    name: '기본 이름'
    };

    export default MyComponent

7.  ☆ propTypes를 통한 props 검증 ☆

    <MyComponent.js>
    import PropTypes from 'prop-types';

    const MyComponent = ({ name, children }) => {
    ...
    }

    MyComponent.defaultProps = {
    name: '기본 이름'
    };

    MyComponent.propTypes = {
    name: PropTypes.string
    };

    export default MyComponent;

    <App.js>
    import MyComponent from './MyComponent';

    const App = () => {
    return <MyComponent name={3}>리액트</MyComponent>
    };

    export default App;

    - 컴포넌트에 설정한 props가 propTypes에서 지정한 형태와 일치하지 않는다면 브라우저 개발자 도구의 Console 탭에 경고 메세지를 출력하여 개발자에게 propTypes가 잘못되었다는 것을 알려줌

8.  ☆ isRequired를 사용하여 필수 propTypes 설정 ☆

    <MyComponent.js>
    import PropTypes from 'prop-types';

    const MyComponent = ({ name, favoriteNumber, children }) => {
     <div>
     안녕하세요. 제 이름은 {name}입니다. <br />
     children 값은 {children}입니다.
     <hr />
     제가 좋아하는 숫자는 {favoriteNumber}입니다.
     </div>
     }

    MyComponent.defaultProps = {
    name: '기본 이름'
    };

    MyComponent.propTypes = {
    name: PropTypes.string,
    favoriteNumber: PropTypes.number.isRequired
    };

    export default MyComponent;

    <App.js>
    import MyComponent from './MyComponent';

    const App = () => {
    return <MyComponent name="React" favoriteNumber={1}>리액트</MyComponent>
    };

export default App;

---

# 클래스형 컴포넌트에서 props 사용하기

- 클래스형 컴포넌트에서 props를 사용할 때는 render 함수에서 this.props를 조회하면 됨
- defaultProps와 propTypes는 똑같은 방식으로 설정할 수 있음

<MyComponent.js>
import { Component } from 'react';
import PropTypes from 'prop-types';

class MyComponent extends Component {
render() {
const { name, favoriateNumber, children } = this.props;
return (

<div>
안녕하세요. 제 이름은 {name}입니다. <br />
children 값은 {children}입니다.
<hr />
제가 좋아하는 숫자는 {favoriteNumber}입니다.
</div>
);
}
}

MyComponent.defaultProps = {
name: '기본 이름'
};

MyComponent.propTypes = {
name: PropTypes.string,
favoriteNumber: PropTypes.number.isRequired
};

export default MyComponent;

<MyComponent.js>
import { Component } from 'react';
import PropTypes from 'prop-types';

class MyComponent extends Component {
static defaultProps = {
name: '기본 이름'
};
static propTypes = {
name: PropTypes.string,
favoriteNumber: PropTypes.number.isRequired
};

render() {
const { name, favoriateNumber, children } = this.props;
return (

<div>
안녕하세요. 제 이름은 {name}입니다. <br />
children 값은 {children}입니다.
<hr />
제가 좋아하는 숫자는 {favoriteNumber}입니다.
</div>
);}}

export default MyComponent;

---

# state

- 리액트에서 state는 컴포넌트 내부에서 ☆ 바뀔 수 있는 값 ☆을 의미함
- props는 컴포넌트가 사용되는 과정에서 부모 컴포넌트가 설정하는 값이며, 컴포넌트 자신은 해당 props를 읽기 전용으로 사용할 수 있음

  ☆ 함수형 컴포넌트에서 useState(기본값)

  - 배열 값 -> 0 = 상태값 / 1 = 상태값 변경. 함수 -> 다시 렌더링
  - this.setState를 사용하여 state에 새로운 값을 넣을 수 있음
  - state 객체 안에 여러 값이 있을 때
  - state를 constructor에서 꺼내기
  - this.setState에 객체 대신 함수 인자 전달하기

  this.setState((prevState, props) => {
  return {
  // 업데이트하고 싶은 내용
  }
  });

---

# state를 사용할 때 주의사항

- 클래스 컴포넌트든 함수 컴포넌트든 state값을 바꾸어야 할 때는 setState 혹은 useState를 통해 전달받은 세터 함수를 사용해야 함
- 배열이나 객체 사본을 만들고 그 사본에 값을 업데이트한 후, 그 사본의 상태를 setState 혹은 세터 함수를 통해 업데이트함

컴포넌트 재 렌더링 기준 - 함수형 컴포넌트 다시 호출, 클래스형 컴포넌트 - render 함수 다시 호출

1. props값이 변경
2. state 값이 변경
3. 부모컴포넌트가 렌러링 되면 -> 자식 컴포넌트도 함께 렌더링
4. 클래스형 컴포넌트 this.forceUpdate() : 강제 렌더링
