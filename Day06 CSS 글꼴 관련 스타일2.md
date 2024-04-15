<Day06 - 0326>
<CSS 글꼴 관련 스타일2>

# font-variant 속성 - 작은 대문자로 표시하기 
     - 대문자를 소문자 크기에 맞추어 작게 표시
            * normal = 일반적인 형태로 표시
            * small-caps = 작은 대문자로 표시


# font-style 속성 - 글자 스타일 지정하기
     - normal	일반적인 형태로 표시
     - italic	이탤릭체로 표시
     - oblique	이탤릭체로 표시


# 텍스트 스타일
    - 1. color
            : 글자 색상을 바꿀때 사용
            : color 속성에 사용할 수 있는 색상 값은 16진수나 rgb(또는 rgba), hsl(또는 hsla) 또는 색상 이름
            : R(0~255) G(0~255) B(0~255)
            : rgb(0~255, 0~255, 0~255);
            : rgb(0, 255, 0)
            : 16진수(0~10, A,B,C,D,E,F) : 숫자의 자리수가 줄어듦
            : rgb(0, 255, 0) = #00FF00 (hex code) = #0F0도 가능(숫자가 반복되는 부분이 있으면 하나로 짧게 쓸수도 있음)

            * hsl ()
                h - 색상
                s - 채도
                l - 밝기

            * rgba
                : (a) 투명도

            * 색상 명칭으로 사용
                : red, blue, orange, pink ...   

    - 2. text-decoration
            : 텍스트에 줄 표시하기/없애기
            : 텍스트에 밑줄을 긋거나 취소 선을 표시할 수 있음

            * none = 밑줄을 표시하지 않음
            * underline = 밑줄을 표시
            * overline = 영역 위로 선
            * line-through = 영역을 가로지르는 선(취소 선)

            <style>
                p {line-height: 1.8;}
                a {text-decoration:none;}  /* 밑줄 없앰 */
                .edited {text-decoration:line-through;}  
                  /* 취소선 */
            </style>

    - 3. text-transform 속성 - 텍스트 대,소문자 변환하기
            : 텍스트를 대,소문자 또는 전각 문자로 변환
            : 한글에는 영향을 미치지 않고 영문자에만 적용

            * none = 변환하지 않음
            * capitalize = 시작하는 첫 번째 글자를 대문자로 변환
            * uppercase = 모든 글자를 대문자로 변환
            * lowercase = 모든 글자를 소문자로 변환
            * full-width = 가능한 모든 문자를 전각 문자로 변환

            * .trans1 {text-transform:uppercase;}  
                /* 대문자로 */
              .trans2 {text-transform:capitalize;}  
                /* 첫글자만 대문자로 */

    - 4. text-shadow 속성 - 텍스트에 그림자 효과 추가하기
            : 텍스트에 그림자 효과를 추가해 텍스트를 좀 더 입체적으로 보이게 함 
            : text-shadow : 가로거리 세로거리 번짐정도 색상

            * text-shadow: none | <가로 거리> <세로 거리> <번짐 정도> <색상>

            * <가로 거리> = 텍스트부터 그림자까지의 가로 거리를 입력. 양수 값은 글자 오른쪽, 음수 값은 글자 왼쪽에 그림자를 만듦. 필수 속성
            * <세로 거리> = 텍스트부터 그림자까지의 세로 거리를 입력. 양수 값은 글자 아래쪽, 음수 값은 글자 위쪽에 그림자를 만듦. 필수 속성
            * <번짐 정도> = 그림자가 번지는 정도. 양수 값을 사용하면 그림자가 모든 방향으로 퍼져 나가기 때문에 그림자가 크게 표시. 반대로 음수 값은 그림자가 모든 방향으로 축소되어 보임. 기본값은 0
            * <색상> = 그림자 색상을 지정. 한 가지만 지정할 수도 있고 공백으로 구분해서 여러 색상을 지정할 수도 있음. 기본 값은 현재 글자 색

    - 5. white-space 속성 - 공백 처리하기
    
            : 텍스트와 함께 연속해 입력된 여러 개의 공백을 어떻게 처리할지 지정
            : 줄개행

            * white-space: normal | nowrap | pre | pre-line | pre-wrap 

            * normal = 여러 개의 공백을 하나로 표시 (기본값)
            * nowrap = 여러 개의 공백을 하나로 표시하고 영역 너비를 넘어가는 내용은 줄을 바꾸지 않고 계속 한 줄로 표시
            * pre = 여러 개의 공백을 그대로 표시하고 영역 너비를 넘어가는 내용은 줄을 바꾸지 않고 계속 한 줄로 표시
            * pre-line = 여러 개의 공백을 하나로 표시하고 영역 너비를 넘어가는 내용은 자동으로 줄을 바꿔 표시
            * pre-wrap = 여러 개의 공백을 그대로 표시하고 영역 너비를 넘어가는 내용은 자동으로 줄을 바꿔 표시

            * td { white-space: nowrap; }  /* 줄 바꿈 없음 */

            (참고)
                overflow
                    : visible => 기본값 : 넘치더라도 보여주기
                    : hidden => 넘치는 영역은 감추기
                    : scroll => 스크롤바 생성
                    : auto => 넘치면 스크롤바 생성, 넘치지 않으면 스크롤바 생성X

                text-overflow
                    : elipsis => 말줄임표

    - 6. letter-spacing과 word-spacing 속성 - 텍스트 간격 조절하기
                : letter-spacing => 낱 글자 사이 간격을 조절
                  word-spacing => 단어와 단어 사이 간격을 조절