<Day07 - 0327>
<CSS 테두리 관련 속성, 여백 조절 속성, 문단 조절 속성>

# 테두리 관련 속성 
    
    - 1. border-style (테두리 스타일 지정하기)
            : solid 직선
            : dashed ----- 짧은 직선으로 된 점선
            : dotted ..... 점선
            : double ===== 이중선
            : none 없음

    - 2. border-width (테두리 두께 지정하기)
            : 경계선 두께

            border-top-width: <크기> | thin | medium | thick
            border-right-width: <크기> | thin | medium | thick
            border-botom-width: <크기> | thin | medium | thick
            border-left-width: <크기> | thin | medium | thick
            border-width: <크기> | thin | medium | thick

    - 3. border-color (테두리 색상 지정하기)
            : 경계선 색상

            border-top-color: <색상>
            border-right-color: <색상>
            border-bottom-color: <색상>
            border-left-color: <색상>
            border-color: <색상>

     -4. border (테두리 스타일 묶어 지정하기)
            : 단축 표기법
            : border: 두께 스타일 색상;

            border-top: <두께> <색상> <스타일>
            border-right: <두께> <색상> <스타일>
            border-bottom: <두께> <색상> <스타일>
            border-left: <두께> <색상> <스타일>
            border: <두께> <색상> <스타일>

     -5. border-radius (박스 모서리 둥글게 만들기)
            : 경계선 모서리를 둥글게
            : 네 모서리를 각각 다르게도 조절 가능

            <크기> = 둥글게 처리할 반지름 크기를 px이나 em같은 단위와 함께 수치로 표시
            <백분율> = 현재 요소의 크기를 기준으로 둥글게 처리할 반지름 크기를 %로 지정

     -6. 타원 형태로 둥글게 만들기
            : 원 - 50%

            border-radius: <가로 반지름> <세로 반지름>


     -7. box-shadow (선택한 요소에 그림자 효과 내기)
            : 그림자 효과
            : 입체감

            box-shadow: <가로이동> <세로이동> <번짐정도> <색상>


# 여백 조절 속성

       1. CSS 포지셔닝
              - 브라우저 화면 안에 각 콘텐츠 영역을 어떻게 배치할지를 결정하는 것

       2. box-sizing (박스 너비 기준 정하기)
              width, height 기준

              * content-box : 기본값, 내용물 기준, 내부 여백, 경계선
              width 속성 값을 콘텐츠 영역 너비 값으로 사용
              -> 전체 크기 증가

              * border-box : 경계선 기준, 내부여백, 경계선 -> 크기X 
              width 속성 값을 콘텐츠 영역에 테두리까지 포함한 박스 모델 전체 너비 값으로 사용
              -> 내용물의 크기가 감소

       3. float (왼쪽이나 오른쪽으로 배치하기)
              * left : 요소를 문서의 왼쪽으로 배치
              * right : 요소를 문서의 오른쪽으로 배치
              * none : 좌우 어느쪽으로도 배치하지 않음

       4. clear (float 속성 해제하기)
              * clear: none | left | right | both

              - float 적용 속성을 제거
              - left: float => left 적용 제거
              - right: float => right 적용 제거
              - both: float => left, right 모두 적용 제거
              - ★★ 공간이 있는 요소에서만 적용 가능 
                (block, inline-block) 에서만 적용 가능

              - 가상 클래스 선택자 ::after 로 가능
                  ul::after{
                     display: block;
                     content: '';
                     clear: left;}

       5. position (배치 방법 지정하기)
              - static = 요소를 문서의 흐름에 맞추어 배치 (기본값)

              상대적인 배치
              - relative = 이전 요소에 자연스럽게 연결해 배치하되 위치를 지정할 수 있음. 처음 적용의 요소가 기준
              - absolute = 원하는 위치를 지정해 배치. 따로 정의된 것이 없으면 문서의 가장 왼쪽 상단이 기준. 상위 요소가 있으면 상위 요소에 상대 배치
              - fixed = 지정한 위치에 고정해 배치. 화면에서 요소가 잘릴 수도 있음. 뷰포트가 배치의 기준
                     (뷰포트: 화면에서 보이는 영역)

              - left: 왼쪽 -> 오른쪽 배치
              - right: 오른쪽 -> 왼쪽 배치
              - top: 위 -> 아래 배치
              - bottom: 아래 -> 위로 배치

       6. visibility (요소를 보이게 하거나 보이지 않게 하기)
              - visible: 기본값 (보임)
              - hidden: 감추기 (영역을 유지) 화면에서 요소를 감추지만 크기는 그대로 유지하기 때문에 배치에 영향을 미침

       7. z-index (요소 쌓는 순서 정하기)
              - 상대 배치에서 적용 가능 (position - relative, absolute, fixed)
              - 층위 (요소 위에 요소를 쌓을 때 쌓는 순서를 지정하는 것이 z-index 속성)
              - -index 값을 명시하지 않을 경우 웹 문서에 맨 처음 삽입하는 요소가 z-index: 1값을 가지며 그 후 삽입하는 요소들은 z-index값이 점점 커짐
              - 숫자가 높을수록 앞쪽에 배치, 숫자가 낮을수록 뒤에 배치


# 문단 조절 속성 

       1. column-width (단의 너비 고정하고 다단 구성하기)
              - 한 화면을 여러 단으로 구성할 때 단의 너비를 고정해 놓고 화면을 분할할 수도 있고 단의 개수를 고정해 좋고 화면을 분할할 수도 있음
              - 다단으로 편집할 때 단의 너비를 고정해 놓으려면 column-width 속성을 이용

       2. column-count (단의 개수 고정하고 다단 구성하기)
              - 단의 개수를 고정해 놓을 수도 있음
              - 브라우저 청의 너비와 상관없이 단의 개수를 항상 일정하게 유지해야 하기 때문에 창의 너비가 커지면 단의 너비도 커짐

       3. column-gap (단과 단 사이 여백 지정하기)
       
       4. column-rule 속성 (구분선의 색상, 스타일, 너비 지정하기)




