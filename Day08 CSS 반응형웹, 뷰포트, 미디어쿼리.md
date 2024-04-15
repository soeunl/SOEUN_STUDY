<Day08 - 0328>
<CSS 반응형 웹, 뷰포트, 미디어 쿼리>

# 모바일 기기와 반응형 웹 디자인
    - 여러 기기에 맞는 사이트를 별도로 제작하지 않고 앞의 사이트처럼 화면 크기에 반응해 화면 요소들을 자동으로 바꾸어 사이트를 구현하는 것
    - 반응형 웹은 모바일 기기에 반응하는 것이 아니라 모바일 기기에 있는 웹 브라우저 창의 너비 값에 반응함


# 반응형 웹의 장점
    - 모든 스마트 기기에서 접속 가능
    - 가로 모드에 맞추어 레이아웃 변경 가능
    - 사이트 유지,관리 용이


# 뷰포트
    - 1. 뷰포트 : 화면에서 실제 내용이 표시되는 영역
    - 2. 뷰포트 지정하기
        뷰포트는 <meta>태그를 이용해 <head> 태그와 </head> 태그 사이에 작성
        <meta name="viewport" content="<속성1=값>, <속성2=값2>, ...">

        (content 안에서 사용하는 뷰포트 속성)
        - width : device-width -> 뷰포트 너비
        - height : device-height -> 뷰포트 높이
        - user-scable : yes -> 확대/축소 가능 여부
        - initial-scale : 처음 로딩 시 화면 배율
        - maximum-scale : 최대 확대/축소 값
        - minimum-scale : 최소 확대/축소 값


# 미디어 쿼리 구문
    - @media 속성을 사용해 특정 미디어에서 어떤 CSS를 적용할 것인지 지정해줌
    - @media [only | not] 미디어 유형 [and 조건] * [and 조건]
    - 미디어 쿼리 구문은 <style>과 </style> 사이에 사용하며 대,소문자를 구별하지 않음
    - 기본적으로 미디어 유형이 지정되어야 하고 필요할 경우, and 연산자로 조건을 적용

# 미디어 쿼리의 조건
      - 뷰포트의 너비와 높이를 미디어 쿼리의 조건으로 사용할 수 있음
      - 이때 height(높이) 값은 미디어에 따라 달라지기 때문에 주의해야 함

        - width, height	웹 페이지의 가로 너비, 세로 높이
        - min-width, min-height	최소 너비, 최소 높이
        - max-width, max-height	최대 너비, 최대 높이


# 단말기의 가로 너비와 세로 높이
        - device-width, device-height : 단말기의 가로 너비, 세로 높이
        - min-device-width, min-device-height : 단말기의 최소 너비, 최소 높이
        - max-device-width, max-device-height : 단말기의 최대 너비, 최대 높이


# 화면 회전
        - orientation : 화면 방향
        - orientaion: portrait : 단말기 세로 방향
        - orientation: landscape : 단말기 가로 방향


# 미디어 쿼리 적용하기
        - 외부 CSS 파일 연결하기 
            :  <link> 태그 사용하기
               <link rel="stylesheet" media="미디어 쿼리 조건" href="css 파일 경로">
            :  @import 구문 사용하기 
               @import url(css 파일 경로) 미디어 쿼리 조건



(참고)
index.html = 대문 페이지 이름
    css
        style.css = 스타일 파일 이름
    js

  XEICON = 아이콘 사이트

  swiper.js = 배너 사이트

  calc = 계산 할때 사용 (css에서 사용)
    calc (100% / 3)

