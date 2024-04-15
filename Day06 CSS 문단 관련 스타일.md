<Day06 - 0326>
<CSS 문단 관련 스타일>

# direction 속성 - 글자 쓰기 방향 지정하기
        * direction: ltr | rtl (배치 기준)
        * ltr = 왼쪽에서 오른쪽으로(left-to-right) 텍스트를 표시 (기본 값) 왼 -> 오
        * rtl = 오른쪽에서 왼쪽으로(right-to-left) 텍스트를 표시
            오 -> 왼

# text-align 속성 - 텍스트 정렬하기
        * text-align: start(기본값) | end | left | right | center | justify | match-parent

        * start = 현재 텍스트 줄의 시작 위치에 맞추어 문단을 정렬. left-to-right 언어라면 왼쪽으로 right-to-left 언어라면 오른쪽에 맞추어 정렬
        * end = 현재 텍스트 줄의 끝 위치에 맞추어 문단을 정렬. left-to-right 언어라면 오른쪽으로, right-to-left 언어라면 왼쪽으로 맞추어 정렬
        * left = 왼쪽에 맞추어 문단을 정렬
        * right	= 오른쪽에 맞추어 문단을 정렬
        * center =  가운데 맞추어 문단을 정렬
        * justify = 양쪽에 맞추어 문단을 정렬
        * match-parent = 부모 요소를 따라 문단을 정렬. 다만 부모 요소의 속성 값이 start나 end일 경우, 부모 요소가 left-to-right인지, right-to-left인지에 따라 left나 right 값으로 계산해 적용

         <style>
            .align-left {text-align:left;}  /* 왼쪽 정렬 */
            .align-right {text-align:right;}  /* 오른쪽 정렬 */
            .align-center {text-align:center;}  
            /* 가운데 정렬 */
            .align-justify {text-align:justify; }  
            /* 양쪽 정렬 */
        </style>

# text-indent 속성 - 텍스트 들여 쓰기
        * text-indent: <크기> | <백분율>

        * <크기> = 단위와 함께 들여 쓸 크기를 지정. 음수 값도 사용할 수 있음
        * <백분율> = 부모 요소의 너비를 기준으로 상대적 크기를 지정

        <style>
            .indent1 {text-indent:15px;}  /* 15px만큼 들여쓰기 */
            .indent2 {text-indent:5%;}  /* 5%만큼 들여쓰기 */
        </style>

# line-height 속성 - 줄 간격 조절하기
        * line-height : normal | <숫자> | <크기> | <백분율> | inherit

        <style>
            .big-line {
            line-height:2; } 
            /* 글자 크기 2배만큼의 줄간격 */
            
            .small-line {
            line-height: 0.7; } 
            /* 글자 크기 0.7배만큼의 줄간격 */
        </style>

# text-overflow 속성 - 넘치는 텍스트 표기하기
        - 넘치는 텍스트를 어떻게 처리할지 지정하는 속성
        - text-overflow 속성은 해당 요소에서 overflow 속성 값이 hidden이거나 scroll, auto이면서 white-space: nowrap 속성을 함께 사용했을 경우에만 적용됨

        * text-overflow: clip | ellipsis

        * clip = 넘치는 텍스트를 자름. 기본값. 넘치는 부분 보임X
        * ellipsis = 말 줄임표(...)로 잘린 텍스트가 있다고 표시


# list-style-type 속성 - 목록의 블릿과 번호 스타일 지정하기
        - 순서 없는 목록의 경우, 목록 앞에 다양한 블릿(bullet)을 넣을 수 있고, 순서 목록에서는 번호 스타일을 지정할 수 있음

        * list-style-type: none | \<순서 없는 목록 블릿\> | \<순서 목록의 번호\>

        * disc(●) = 채운 원
        * circle(○) = 빈 원
        * square(■) = 채운 사각형
        * none = 블릿 없애기