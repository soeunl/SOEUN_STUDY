<Day16 - 0409>
<React URL 파라미터와 쿼리스트링, 중첩된 라우트, 부가기능, 코드스플리팅>

# URL 파라미터와 쿼리스트링

1. ☆ URL 파라미터 - 경로 변수 ☆

- 주소의 경로에 유동적인 값을 넣는 형태
- 주로 ID또는 이름을 사용하여 특정 데이터를 조회할 때 사용
- useParams()
- useParams 라는 Hook을 사용하여 객체 형태로 조회할 수 있음
- URL 파라미터의 이름은 라우터 설정을 할 때 Route 컴포넌트의 path props를 통하여 설정함
- (예) /profile/이름
- URL 파라미터는 /profiles/:username과 같이 경로에 :를 사용하여 설정함. 만약 URL 파라미터가 여러개인 경우엔 /profiles/:username/:field와 같은 형태로 설정할 수 있음

2. ☆ 쿼리스트링 ☆

- 주소의 뒷부분에 ? 문자열 이후 key=value로 값을 정의하며 &로 구분을 하는 형태
- 키워드 검색, 페이지네이션, 정렬 방식 등 데이터 조회에 필요한 옵션을 전달할 때 사용
- (예) /articles?page=1&keyword=react
- useLocation()
- 쿼리스트링을 사용할 때는 URL 파라미터와 달리 Route 컴포넌트를 사용할 때 별도로 설정해야 하는 것은 없음

★ useLocation Hook ★

- useLocation Hook은 location 객체를 반환하며 이 객체는 현재 사용자가 보고있는 페이지의 정보를 지니고 있음
  ★★★ useLocation Hook에는 다음과 같은 값들이 있음
- pathname : 현재 주소의 경로 (쿼리스트링 제외)
- search : 맨 앞의 ? 문자 포함한 쿼리스트링 값
- hash : 주소의 # 문자열 뒤의 값 (주로 History API가 지원되지 않는 구형 브라우저에서 클라이언트 라우팅을 사용할 때 쓰이는 해시 라우터에서 사용함)
- state : 페이지로 이동할 때 임의로 넣을 수 잇는 상태 값
- key : location 객체의 고유 값, 초기에는 default 이며 페이지가 변경될때 마다 고유의 값이 생성됨
  ★★★

- 쿼리스트링은 ☆location.search☆ 값을 통해 조회할 수 있음
- 리액트 라우터에서는 ☆useSearchParams☆라는 Hook을 통해서 쿼리스트링을 더욱 쉽게 다룰 수 있게 됨
- useSearchParams는 배열 타입의 값을 반환하며, 첫번째 원소는 쿼리파라미터를 조회하거나 수정하는 메서드들이 담긴 객체를 반환함
- get 메서드를 통해 특정 쿼리파라미터를 조회할 수 있고, set 메서드를 통해 특정 쿼리파라미터를 업데이트 할 수 있음
- 두번째 요소는 쿼리파라미터를 객체형태로 업데이트할 수 있는 함수를 반환함

★ URLSearchParams 생성자 ★
: URL의 쿼리 문자열을 대상으로 작업할 수 있는 유틸리티 메서드를 정의함

- const [searchParams, setSearchParams] = useSearchParams();
- setSearchParams는 실제 주소까지 변경할 수 있음
- 쿼리파라미터를 사용할 때 유의점은 쿼리파라미터를 조회할 때 값은 무조건 ★문자열 타입★이라는 것
- true 또는 false 값을 넣게 된다면 값을 비교할 때 꼭 'true'와 같이 따옴표로 감싸서 비교를 해야 하며, 숫자를 다룰때는 parseInt를 사용하여 숫자 타입으로 변환해야 함

---

# 중첩된 라우트

- Articles 컴포넌트에서 리액트 라우터에서 제공하는 Outlet 이라는 컴포넌트를 사용해주어야 함
- 이 컴포넌트는 Route의 children으로 들어가는 JSX 요소를 보여주는 역할
- Outlet 컴포넌트가 사용된 자리에 중첩된 라우트가 보여지게 됨

---

# 공통 레이아웃 컴포넌트

- 중첩된 라우트와 Outlet은 페이지끼리 공통적으로 보여줘야 하는 레이아웃이 있을때도 사용할 수 있음

1. index props

- Route 컴포넌트에는 index라는 props가 있음
- 이 props는 path="/"와 동일한 의미를 가짐
- index props는 상위 라우트의 경로와 일치하지만, 그 이후에 경로가 주어지지 않았을 때 보여지는 라우트를 설정할때 사용
- path="/"와 동일한 역할을 하며 이를 좀 더 명시적으로 표현하는 방법

---

# 리액트 라우터 부가기능

1. useNavigate

- 페이지 이동
- Link 컴포넌트를 사용하지 않고 다른 페이지로 이동을 해야 하는 상황에 사용하는 Hook
- navigate 함수를 사용할 때 파라미터가 숫자 타입이라면 앞으로 또는 뒤로 이동
  = navigate(-1) : 뒤로 한번 이동
  // history.back()
  = navigate(1) : 앞으로 한번 이동(뒤로가 한번 한 후 동작)
- 다른 페이지로 이동을 할 때 ★replace★ 옵션을 사용하면 페이지 이동 기록이 남지 않음

  const goArticles = () => {
  navigate('/articles', { replace: true });
  };

  location.assign(..), location.herf
  location.replace(..)

2. NavLink

- NavLink 컴포넌트는 링크에서 사용하는 경로가 현재 라우트 경로와 일치하는 경우 특정 스타일 또는 CSS 클래스를 적용하는 컴포넌트
- 이 컴포넌트를 사용할 때 style 또는 className을 설정할 때 { isActive: boolean }을 파라미터로 전달받는 함수 타입의 값을 전달함

<NavLink
style={({isActive}) => isActive ? activeStyle : undefined }
/>

3. NotFound 페이지 만들기

- 사전에 정의되지 않은 경로에 사용자가 진입했을 때 보여주는 페이지
- \*는 와일드카드 문자, 아무 텍스트나 매칭한다는 의미
- 라우트 요소의 상단에 위치하는 라우트들의 규칙을 모두 확인하고, 일치하는 라우트가 없다면 이 라우트가 화면에 나타나게 됨

4. Navigate 컴포넌트

- Navigate 컴포넌트는 컴포넌트를 화면에 보여주는 순간 다른 페이지로 이동을 하고 싶을 때 사용하는 컴포넌트. 즉, 페이지를 리다이렉트 하고 싶을 때 사용함

  if (!isLoggedIn) {
  return <Navigate to="/login" replace={true} />;
  }

---

# 코드 스플리팅

1. React.lazy와 Suspense를 통한 컴포넌트 코드 스플리팅

- 지연로딩 지원 사용할 때 로드함
- React.lazy 함수를 사용하면 dynamic import를 사용해 컴포넌트를 렌더링할 수 있음
- React는 SPA(Single-Page-Application)이므로 한 번에 사용하지 않는 컴포넌트까지 불러오는 단점이 있음
- React는 React.lazy를 통해 컴포넌트를 동적으로 import를 할 수 있기 때문에 이를 사용하면 초기 렌더링 지연시간을 어느정도 줄일 수 있게 됨

import Component from './Component';

/_ React.lazy로 dynamic import를 감싼다 _/
const Component = React.lazy(() => import('./Component'));

- 이 React.lazy로 감싼 컴포넌트는 단독으로 쓰일 수는 없고, React.suspense 컴포넌트의 하위에서 렌더링을 해야 함

★★★ React.Suspense ★★★

- Router로 분기가 나누어진 컴포넌트들을 위 코드처럼 lazy를 통해 import하면 해당 path로 이동할때 컴포넌트를 불러오게 되는데, 이 과정에서 로딩하는 시간이 생기게 됨
- Suspense는 아직 렌더링이 준비되지 않은 컴포넌트가 있을 때 로딩 화면을 보여주고, 로딩이 완료되면 렌더링이 준비된 컴포넌트를 보여주는 기능임

/_ suspense 기능을 사용하기 위해서는 import 해와야 한다. _/
import { Suspense } from 'react';

const OtherComponent = React.lazy(() => import('./OtherComponent'));
const AnotherComponent = React.lazy(() => import('./AnotherComponent'));

function MyComponent() {
return (

<div>
{/_ 이런 식으로 React.lazy로 감싼 컴포넌트를 Suspense 컴포넌트의 하위에 렌더링 _/}
<Suspense fallback={<div>Loading...</div>}>
{/_ Suspense 컴포넌트 하위에 여러 개의 lazy 컴포넌트를 렌더링시킬 수 있다. _/}
<OtherComponent />
<AnotherComponent />
</Suspense>
</div>
);
}

- Supense 컴포넌트의 fallback prop은 컴포넌트가 로드될 때까지 기다리는 동안 로딩 화면으로 보여줄 React 엘리먼트를 받아들임
- Suspense 컴포넌트 하나로 여러 개의 lazy 컴포넌트를 보여줄 수도 있음

★★★ React.lazy와 Suspense의 적용 ★★★

import { Suspense, lazy } from 'react';
import { BrowserRouter as Router, Routes, Route } from 'react-router-dom';

const Home = lazy(() => import('./routes/Home'));
const About = lazy(() => import('./routes/About'));

const App = () => (
<Router>
<Suspense fallback={<div>Loading...</div>}>
<Routes>
<Route path="/" element={<Home />} />
<Route path="/about" element={<About />} />
</Routes>
</Suspense>
</Router>
);

2. ☆☆ Loadable Components를 통한 코드 스플리팅

- 지연로딩 지원
- JS 코드 번들을 잘게 쪼개서 필요할 때마다 로드할 수 있도록 사용하는 기술! 미리 로드해야 하는 코드의 양을 줄여서 초기 로딩 시간을 개선할 수 있음

  yarn add @loadable/component

★★★ Loadable Components 적용 ★★★
import loadable from "@loadable/component";
(생략)

const Main = loadable(() => {
return import("pages/Main");
});
const Setting = loadable(() => {
return import("pages/Setting");
});
...

(생략)
<Route path="/" element={<Main />} />
<Route path="/setting" element={<Setting />} />
...
(생략)

---

(참고)
/board -> 게시글 목록
/board/view/:id -> 게시글 상태

/member/login
/member/join
