<Day17 - 0411>
<React 리액트 프로젝트>

# 리액트 프로젝트 만드는 방법

D:\이소은 포트폴리오>yarn create react-app react_project

---

# - .prettierrc 설정

```json
{
  "singleQuote": true,
  "semi": true,
  "useTabs": false,
  "tabWidth": 2,
  "trailingComma": "all"
}
```

---

# 필요 의존성 설치

> 필요 라이브러리

- react-router-dom : 리액트 라우터 (페이지 나누는 기능)
- sass, styled-components, classnames : 스타일링 목적
- immer : 불변성 관리
- ract-icons : 리액트에서 제공하는 아이콘 라이브러리
- @loadable / component : 지연로딩
- react-helmet-async : head 태그 내의 내용을 변경 시
- 의존성 설치

```
yarn add react-router-dom sass styled-components classnames immer react-icons @loadable/component
yarn add react-helmet-async
```

---

# react-helmet-async 설정

- src/index.js

```jsx
...

import { HelmetProvider } from 'react-helmet-async';

... // 코드 생략

root.render(
  <React.StrictMode>
    <HelmetProvider>
      <App />
    </HelmetProvider>
  </React.StrictMode>,
);

```

- 사용법

```javascript
import { Helmet } from "react-helmet-async";

const App = () => {
  return (
    <>
      <Helmet>
        <title>사이트 제목 변경 테스트!</title>
      </Helmet>
    </>
  );
};

export default App;
```

---

# 다국어 설정

i18next, react-i18next

i18n :국제화

i nternationalz... n

{}, {}, {} -> {}

- 의존성 : i18next, react-i18next
- 의존성 설치

```
yarn add i18next react-i18next
```

- 언어파일 생성

  - src/langs/ko, src/langs/en 폴더 생성
  - 각 폴더별로 공통 문구 - commons.js, 검증 문구 - validations.js, 에러 문구 - errors.js

- 언어파일 통합

  - (예) src/langs/ko/index.js

- 적용하기
  - useTranslation 훅 / react-i18next
  - t : 메세지 조회 함수
  - i18n : 편의 기능 객체, changeLanguage(..) : 언어 변경

---

# 레이아웃 구성

DDD(Domain Driven Design)
Domain - 전문가 영역

    member

    order
        containers
        components

- src/layouts/Mainlayout.js
- src/outlines/Header.js
- src/outlines/Footer.js

---

# 설정

- src.index.js : BrowerRouter 컴포넌트로 감싸기

```Jsx
...

import { BrowserRouter } from 'react-router-dom';

```

---

# 회원

- /member/join : 회원가입
- /member/login : 로그인

---

# 없는 페이지

- ＊ : 없는 페이지 - commons/pages/NotFound.js

---

# 에러페이지

> class형 컴포넌트 - componentDidCatch 사용

- commons/pages/Error.js
- commons/components/ErrorDisplay.js

---

# 공통 스타일 : src/index.css

- 공통 폰트
- 스타일 초기화
- 기준 폰트 사이즈 : styles/fontSize.js / small, normal, medium, big, extrabig
- 기준 컬러 : Primary, Secondary, Success, Danger, Warning, Info, Light, Dark
