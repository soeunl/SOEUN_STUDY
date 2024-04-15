<Day06 - 0326>
<CSS 색상과 배경을 위한 스타일>

# 웹에서 색상 표현하기
        1. 16진수 표기법 
                - #ffff00 처럼 # 기호 다음에 6자리 16진수로 표시하는 것으로 가징 기본적인 방법
                - 6자리는 앞에서부터 두 자리씩 묶어 #RRGGBB 형식으로 표시
                - #ffff00 처럼 두 자리씩 중복될 경우 #ff0으로 줄여서 표기할 수 있음
        2. rgb와 rgba 표기법
                - 빨간색, 초록색, 파란색의 양을 십진수로 표현
                - 하나도 섞이지 않았을 때는 0으로 표시하고 가득 섞였을 때는 255로 표시하며 그 사이 값으로 각 색상의 양을 조절
                - rgba에서 맨 끝의 a, 즉 a(alpha)는 불투명도 값을 나타내는 것으로 0부터 1까지의 값 중에서 사용할 수 있음
                - 1은 완전 불투명, 0.9나 0.8처럼 숫자가 작아질수록 조금씩 투명해지다가 0이 되면 완전히 투명해짐
                - 투명도를 표기할 때는 0.5 대신 소수점 앞의 0을 빼고 .5라고 표기도 가능
        3. hsl과 hsla 표기법
                - hsl은 차례대로 hue(색상), saturation(채도), lightness(밝기)

                hsl(<hue 값>, <saturation 값>, <lightness 값>);
                hsla(<hue 값>, <saturation 값>, <lightness 값>, <alpha 값>);

                - 밝기(lightness)도 %로 표시하는데 0%가 가장 어둡고 100%가 가장 밝음
        4. 색상 이름 표기법
                - red, yellow, black 처럼 잘 알려진 색상 이름으로 표시
                - 모든 브라우저에서 표현할 수 있는 색상을 웹 안정 색상(web-safe color)라고 하는데 기본 16가지 색상을 포함한 216가지임


[배경 색과 배경 이미지]

# background-color 속성 - 배경 색 지정하기
        * background-color: <색상>
          16진수나 rgb 값 또는 색상 이름을 사용해 지정

        * background-color: #00ff00; 
        /* 16진수 : 세밀히 색상 조절 */
        * background-color: rgb(0, 255, 0); 
        /* rgba: 필요하면 * 투명도도 함께 조절 가능 */
        background-color: green;   
        /* 색상 이름 : 원색 사용 */

# background-image 속성 - 웹 요소에 배경 이미지 넣기
        - 배경 이미지에는 웹에서 사용 가능한 파일인 jpg나 gif, png 파일을 사용하며 이것을 url(파일경로) 형식으로 사용
        - 파일 경로는 현재 웹 문서를 기준으로 상대 경로를 지정할 수도 있고 'http://'로 시작하는 절대 경로를 사용할 수도 있음
        - 파일 경로에는 작은 따옴표(또는 큰따옴표)를 붙여도 되고 안 붙여도 됨

        * background-image: url(파일 경로)

# background-repeat 속성 : 배경 이미지 반복 방법 지정하기
        * background-repeat: repeat | repeat-x | repeat-y | no-repeat

        * repeat = 브라우저 화면에 가득 찰 때까지 배경 이미지를 가로와 세로로 반복
        * repeat-x = 브라우저 창 너비와 같아질 때까지 배경 이미지를 가로로 반복
        * repeat-y = 브라우저 창 높이와 같아질 때까지 배경 이미지를 세로로 반복
        * no-repeat = 배경 이미지를 한 번만 표시하고 반복하지 않음. 반복 없음

# background-size 속성 - 배경 이미지 크기 조절하기
        * background-size: auto | contain | cover | <크기 값> | <백분율>
        - 너비와 높이를 함께 지정하면 이미지가 왜곡될 수 있음
        - 너비와 높이 중 한가지만 설정하면 나머지는 비율에 맞추어 자동 설정

        * auto	원래 배경 이미지 크기만큼 표시
        * contain = 요소 안에 배경 이미지가 다 들어오도록 이미지를 확대/축소
        * cover	배경 이미지로 요소를 모두 덮도록 이미지를 확대/축소
        * <크기 값> = 너비 값과 높이 값을 지정. 너비 값만 지정할 경우, 원래 배경 이미지 크기를 기준으로 축소/확대 비율을 자동으로 계산해 높이 값을 지정
        * <백분율> = 배경 이미지가 들어갈 요소의 크기를 기준으로 백분율 값을 지정하고 그 크기에 맞도록 배경 이미지를 확대하거나 축소

# background-position 속성 - 배경 이미지 위치 조절하기
        - 배경 이미지 배치
        - background-position: 좌 -> 우, 위 -> 아래
        - left, right, center, top, center, bottom

        * background-position: <수평 위치> <수직 위치>;
          수평 위치 : left | center | right | <백분율> | <길이 값>
          수직 위치 : top | center | bottom | <백분율> | <길이 값>

# background-origin 속성 - 배경 이미지 배치할 기준 조절하기
        - background-position 속성을 이용해 배경 이미지를 배치할 때 기준이 필요한데 이 기준은 background-origin 속성으로 지정할 수 있음

        * background-origin: border-box | padding-box | content-box 

        * border-box = 박스 모델의 가장 외곽인 테두리(border)가 기준. 경계선부터 배치 (기본값)
        * padding-box = 박스 모델에서 테두리를 뺀 패딩(padding)이 기준. 내부 여백부터 배치
        * content-box = 박스 모델에서 내용 부분이 기준. 내용 영역부터 배치

        (1) background-origin: padding-box; - 배경 이미지가 패딩 영역부터 시작
        (2) background-origin: border-box; - 배경 이미지가 테두리부터 시작
        (3) background-origin: content-box; - 배경 이미지가 콘텐츠 영역부터 시작

# background-attachment 속성 - 배경 이미지 고정하기
        -  background-attachment 속성을 이용하면 배경 이미지를 고정할 수 있음
        - background-attachment: fixed; 로 설정하면 웹 문서 화면을 아래로 스크롤하더라도 배경 이미지는 고정되고 내용이 이미지 위에 떠 있는 것처럼 보임

        * background-attachment: scroll | fixed

        * scroll = 화면 스크롤과 함께 배경 이미지도 스크롤됨
        * fixed	= 화면이 스크롤되더라도 배경 이미지는 고정됨. 기본 값

# background 속성 - 속성 하나로 배경 이미지 제어하기
        - 지금까지 설명한 배경 이미지 관련 속성을 background라는 하나의 속성으로 줄여 사용할 수 있음
        - background : 색상 이미지(url(..)) 반복(repeat) attachment 배치(position);
        - 색상, 이미지 둘중 한개는 필수

        * background:url('images/bg3.jpg') no-repeat fixed right bottom;


        (여백)
        margin : 영역 외부 여백
        padding : 영역 내부 여백