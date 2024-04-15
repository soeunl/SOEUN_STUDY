<Day15 - 0408>
<React 컴포넌트 스타일링>

# 컴포넌트 스타일링

1. ☆ Sass 사용하기 ☆

① Sass란?

- Sass(Syntactically Awesome Style Sheets)
  (문법적으로 매우 멋진 스타일시트)
- CSS 전처리기로 복잡한 작업을 쉽게 할 수 있도록 해 주고, 스타일 코드의 재활용성을 높여 줄 뿐만 아니라 코드의 가독성을 높여서 유지 보수를 더욱 쉽게 함
- 두 가지 확장자 .scss와 .sass를 지원
- .sass 확장자는 중괄호({})와 세미콜론(;)을 사용하지 않음 ☆☆☆
- Sass를 사용하려면 sass라는 라이브러리를 설치해 주어야 합니다. 이 라이브러리는 Sass를 CSS로 변환해줌
- 적응이 잘 안 되면 .scss 확장자로 세미콜론과 중괄호 사용 가능
- .scss 확장자는 기존 CSS를 작성하는 방식과 비슷함

② 설치

- yarn add sass

③ utils 함수 분리하기

- 여러 파일에서 사용될 수 있는 Sass 변수 및 믹스인을 다른 파일로 분리하여 작성한 뒤 필요한 곳에서 쉽게 불러와 사용할 수 있음

@import("스타일 시트 경로")

2. ☆ scss 문법 ☆

- $red 등의 형식으로 변수 사용하기
- 재사용되는 스타일 블록을 함수처럼 사용할 수 있는 믹스인 만들기
  (ex) @mixin square($size) {
  $calculated: 32px x $size;
  width: $calculated;
  height: $calculated;
  }
- 들여쓰기로 표현
- &.red {}의 형태로 속성 정의
  (ex) &.red {
  // .red 클래스가 .box와 함께 사용되었을 때
  background: red;
  @include square(1);
  }

3. ☆ CSS Module ☆

- [파일이름]\_[클래스 이름]\_\_[해시값] 형태로 자동으로 만들어서 컴포넌트 스타일 클래스 이름이 중첩되는 현상을 방지해 주는 기술
- ☆ .module.css 확장자 ☆ 로 파일을 저장하기만 하면 CSS Module이 적용
- 클래스명이 중복이 되지 않도록 해줌

4. ☆ classnames ☆

- CSS 클래스를 조건부로 설정할 때 매우 유용한 라이브러리

  yarn add classnames

- classname bind (매개변수를 고정해서 새로운 함수를 만들어줌)
  : const cx = classNames.bind(styles);
  CSSModule 안에 있을 때 사용 가능

① Sass와 함께 사용하기

- Sass를 사용할 때도 파일 이름 뒤에 .module.scss 확장자를 사용해 주면 CSS Module로 사용할 수 있음

② CSS Module이 아닌 파일에서 CSS Module 사용하기

- CSS Module에서 글로벌 클래스를 정의할 때 :global을 사용했던 것처럼 CSS Module이 아닌 .css/.scss 파일에서도 :local을 사용하여 CSS Module을 사용할 수 있음

---

# styled-components

- 자바스크립트 파일 안에 스타일을 선언하는 방식
- CSS-in-JS 라고 부름
- yarn add styled-components (꼭 s를 붙이기)

---

# tagged 함수

- 함수명`문자열` 형태로 호출
- `` 안쪽은 매개변수
- ${} 안에다가 변수나 함수 등 입력 가능
