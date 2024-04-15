<Day06 - 0326>
<CSS 박스모델>

# 블록 레벨 요소와 인라인 레벨 요소
        1. 블록 레벨(block-level) 요소
                - 태그를 사용해 요소를 삽입했을 때 혼자 한 줄을 차지하는 요소
                - 한 줄을 차지한다는 것은 해당 요소의 너비가 100%라는 의미로 그 요소의 왼쪽이나 오른쪽에 다른 요소가 올 수 없음
                - 공간O , 너비(width), 높이(height) 지정
                - 줄개행
                - 너비나 마진, 패딩 등을 이용해 크기나 위치를 지정하려면 블록 레벨 요소여야 함
                - <div> 태그나 <p> 태그 등이 블록 레벨 요소를 만드는 대표적인 태그
                - <p>,<h1>~<h6>, <ul>, <ol>, <div>, <blockquote>,<form>, <hr>, <table>, <fieldset>, <address>
                - 외부여백(margin) : 상하좌우 적용 가능

        2. 인라인 레벨(inline-level) 요소
                - 줄을 차지 하지 않는 요소
                - 화면에 표시되는 콘텐츠만큼 영역을 차지하고 나머지 공간에는 다른 요소가 올 수 있음
                - 한 줄에 여러 개의 인라인 레벨 요소를 표시할 수 있음
                - <img> 태그나 <string> 태그 등이 인라인 레벨 요소를 만드는 태그
                - 공간X, 너비(width), 높이(height) 지정 X
                - 줄개행 X
                - <img>, <object>, <br>, <sub>, <sup>, <span>, <input>, <textarea>, <label>, <button>
                - 외부여백(margin) : 좌우 여백만 적용 가능


# 박스 모델(box model) - 박스 형태의 콘텐츠
        - 웹 문서의 블록 레벨 요소들은 모두 박스 형태
        - 스타일 시트에서는 이렇게 박스 형태인 요소를 박스 모델(box model) 요소라고 부름
        - 박스 모델은 실제 콘텐츠 영역, 박스와 콘텐츠 영역 사이의 여백인 패딩(padding), 박스의 테두리(border), 그리고 여러 박스 모델 사이의 여백인 마진(margin) 등의 요소로 구성됨


# display 속성 - 화면 배치 방법 결정하기
        - display 속성을 사용하면 블록레벨 요소를 인라인 레벨 요소로 바꾸거나 인라인 레벨 요소를 블록 레벨 요소로 바꿀 수 있음
        - 세로로 표시되는 목록을 가로 내비게이션으로 바꿀 때, 한 줄로 표시되는 이미지에 여백과 테두리를 추가해 갤러리로 표시할 때 이 방법을 사용

        * display: none | contents | block | inline | inline-block | table | table-cell 등

        * block : inline -> block
        * inline : block -> inline
        * inline-block : inline(줄 개행X) + block(너비, 높이, 상하 외부여백),  블록 레벨 요소와 인라인 레벨 요소 두 가지 특성 모두 가짐 ★★★ inline-block은 상하여백이 중첩되지 않음
        * none : 해당 요소를 화면에 아예 표시하지 않음

                 (참고)
                 visibility: hidden; 도 비슷한 역할을 하는데 visibility 속성은 화면에서 감추기만 할 뿐 원래 요소가 있는 공간은 그대로 차지하지만, display: none;은 아예 공간조차 차지하지 않음

                        * visibility
                        - visible : 보임, 기본값
                        - hidden : 영역 공간을 유지한 채 감추기


# 여백을 조절하는 속성들
        - margin 속성 - 요소 주변 여백 설정하기
        - 마진(margin) : 현재 요소 주변의 여백
        - 마진을 이용하면 한 요소와 다른 요소 사이의 간격을 조절할 수 있음

        - padding 속성 - 콘텐츠 영역과 테두리 사이 여백 설정하기
        - 패딩(padding) : 콘텐츠 영역과 테두리 사이의 여백, 다시 말해 테두리 안쪽의 여백이라고 생각하면 됨
        - padding 속성은 margin 속성과 사용법이 비슷함

                1. margin - 외부 여백
                        margin: 50px (상단, 하단, 우측, 좌측 모두 50px)
                        margin: 50px 20px (상하단 50px, 좌우 20px)
                        margin: 50px 30px 20px (상단 50px, 좌우30px, 하단 20px )
                        margin: 50px 40px 30px 20px (상단 50px, 우 40px, 하단 30px, 좌20px)

                        * margin-top: <크기> | <백분율> | auto
                        * margin-right: <크기> | <백분율> | auto
                        * margin-bottom: <크기> | <백분율> | auto
                        * margin-left: <크기> | <백분율> | auto
                        * margin: <크기> | <백분율> | auto

                * 마진 중첩(margin overlap) 현상
                        - 요소를 세로로 배치할 경우, 마진과 마진이 만날 때 마진 값이 큰 쪽으로 겹치는 것
                        - 이런 현상을 마진 중첩(margin overlap) 또는 마진 상쇄(margin collapse)라고 함
                        - 마진 중첩은 아래 마진과 위 마진이 서로 만날 때 큰 마진 값으로 합쳐지는 것이고, 오른쪽 마진과 왼쪽 마진이 만날 경우에는 중첩되지 않음. (inline-block 속성은 예외)

                2. paddng - 내부 여백
                        * padding-top: <크기> | <백분율> | auto
                        * padding-right: <크기> | <백분율> | auto
                        * padding-bottom: <크기> | <백분율> | auto
                        * padding: <크기> | <백분율> | auto


                * auto : 균등하게 배분
                         요소의 너비 값을 뺸 나머지 공간의 좌우 마진을 똑같이 맞춤
                         웹 요소를 중앙에 배치하려고 할 때 자주 사용
