<Day04 - 0322>
<HTML 폼 태그, input 태그의 다양한 속성>

# button 태그
    - 폼 안에 버튼 형태를 만듬
    - type : submit => 제출 버튼 (기본값)
             reset => 다시 입력 버튼
             button => 일반 버튼


# method 속성
    - 방법에 관한 것
    - 제출 방식에 대한 부분
    - get(기본값) 과 post로 나누어져 있는데, 목적이 다르기 때문에 두가지로 나누어져 있음
    - get : 서버의 자원 조회, 서버 자원 요청
          : 데이터를 잘 조회하기 위해 질의하는 것
          : 자원을 찾아달라고 서버에게 힌트
    - post : 작성 
           : 데이터의 추가, 변경
           : 회원가입에 적합

    * 쿼리스트링(query string) 질의문
        - get 방식으로 양식을 제출하거나 할때 
        - ?가 붙어있고 키와 값 형태로 되어있음
        - 서버가 자원을 조회하기 위해 참고하는 데이터


# <fieldset>, <legend> 태그 - 폼 요소 그룹으로 묶기
    - 하나의 폼 안에서 여러 구역을 나누어 표시하려고 할 때 <fieldset>, <legend> 태그를 사용
    - <fieldset> 태그는 <fieldset>과 </fieldset> 태그 사이의 폼들을 하나의 영역으로 묶고 외곽선을 그려줌
    - <legend> 태그는 <fieldset> 태그로 묶은 그룹에 제목을 붙여 줌

    <fieldset>
			<legend>개인 정보</legend>
			<ul>
				<li>
					<label for="name">이름</label>
					<input type="text" id="name">
				</li>
				<li>
					<label for="mail">메일 주소</label>
					<input type="text" id="mail">
				</li>
			</ul>
	</fieldset>	


[<input> 태그의 다양한 속성]

# input 입력 (type submit, reset)
    - submit = 양식 제출 버튼 (사용자가 폼에 입력한 정보를 서버로 전송)
    - reset = 다시 입력 버튼 (<input> 요소에 입력된 모든 정보를 재설정해 사용자가 입력한 내용을 모두 지울 수 있음)
    * value = 입력값
        (submit, reset -> 버튼명 수정)
        (value 값으로 버튼명 수정 가능)    	

# input 태그의 매우 중요한 속성 중 하나인 name ★★★
    - 매우 중요하고 강조가 많이 되는 속성
    - 꼭 있어야 하는 속성
    - 입력항목의 역할. 항목명
    - name으로 입력항목이 있어야지 데이터가 전송
    - name이 있어야만 어떤 항목으로 데이터를 넘겼는지, 데이터를 작성했는지 알 수 있음

# checkbox와 radio 항목에서의 value값 ★★★
    - checkbox와 radio 항목에서는 value값을 꼭 입력해야함
    - 사용자가 입력을 하는 것이 아닌 선택을 하는 항목이기 때문
    - value로 값을 명시해야만 그 값이 전송됨
    * name 값은 항목 모두 같게 입력
    * value 값은 그 항목에 따라 각각 다르게 입력    

# action : 양식 제출 경로 ★★★
    - 작성한 데이터가 명시된 주소로 넘어감
    - 서버로 넘어감
    - <form action = "파일명(제출처)">

# type="text" - 텍스트 필드 만들기
    - 한 줄짜리 일반 텍스트를 입력하는 필드

# type="search", type="url", type="email", type="tel" - 분화된 텍스트 필드
    - type="search" : 검색 상자 만들기
    - type="url" : URL 입력란 만들기
   - type="email" : 메일 주소 입력란 만들기
    - type="tel" : 전화번호 입력란 만들기

# type="number" - 숫자 입력하기
    - 사용자가 입력한 내용을 숫자로 인식
    - 브라우저에 따라 스핀 박스가 표시되기도 함
    - 스핀 박스란 입력창 오른쪽에 작은 화살표를 표시해 화살표를 클릭하면 숫자를 증감시킬 수 있게 한 것

# type="range" - 슬라이드 막대로 숫자 지정하기
    - type="number" 필드와 type="range" 필드에서 사용할 수 있는 속성

          * min = 필드에 입력할 수 있는 최솟값을 지정 type="range"일 때 기본 최소값은 0
            max	= 필드에 입력할 수 있는 최댓값을 지정 type="ranage"일 때 기본 최대값은 100
            step = 짝수나 홀수 등 특정 숫자로 제한하려고 할 때 숫자 간격을 지정가능 기본 값은 1이며 생략할 수 있음
            value = 필드에 표시할 초기값

# type="date", type="month", type="week" - 날짜 표시하기
    -  date	날짜를 선택
          * month = 월(month)과 연도(year)를 선택
            week = 주(week)와 연도(year)를 선택

# type="time", type="datetime", type="datetime-local" - 시간 지정하기
    - 시간을 지정할 때는 type="time"을 사용
    - 날짜와 시간을 함께 지정하려면 type="datetime"이나 type="datetime-local"을 사용
          * min	= 날짜나 시간의 최솟값을 지정
            max	= 날짜나 시간의 최댓값을 지정
            step = 스핀 박스의 화살표를 누를 때마다 날짜나 시간을 얼마나 조절할지를 지정
            value =  화면에 표시할 초기값을 지정 
                * type="time"일 경우 시간은 00:00부터 23:59까지 입력하고 type="datetime"이나 
                  type="datetime-local" 유형일 경우, 날짜 다음에 키워드 T를 쓰고 24시간제로 시간을 지정

# type="file" - 파일 첨부하기
    - type="file" 필드를 넣으면 웹브라우저 화면에 [파일 선택]이나 [찾아보기] 등이 표시됨
    - 이 버튼을 클릭한 후 파일을 선택하면 파일이 첨부됨

# autofocus 속성 - 입력 커서 표시하기
    - autofocus 속성을 사용하면 페이지를 불러오자마자 폼의 요소 중에서 원하는 요소에 마우스 커서를 표시할 수 있음

 # placeholder 속성 - 힌트 표시하기
    - 사용자가 텍스트를 입력할 때 도움이 되도록 입력란에는 적당한 힌트 내용을 표시하고 있다가 그 필드를 클릭하면 내용이 사라지도록 만들 수 있음
    - 텍스트 필드 앞에 제목을 사용하지 않고도 해당 필드에 어떤 내용을 입력해야 할지 알려주는 것이 가능  


# <datalist> 태그, <option> 태그
    - 데이터 목록중에서 값을 선택하도록 만들 수 있음
    - 텍스트 필드에 직접 값을 입력하는 것이 아니라 데이터 목록에 제시한 값 중에서 선택하면 그 값이 자동으로 입력됨
    - 데이터 목록은 텍스트 필드와 함께 사용하기 때문에 <input> 태그를 함께 사용
    - 사용하는 방법은 <input> 태그의 list 속성 값과 데이터 목록의 id를 같게 만들어 사용

        <datalist id="datalist 아이디값">
            <option value="항목1" label="항목1명칭"></option>
            <option value="항목2" label="항목1명칭"></option>
            <option value="항목3" label="항목1명칭"></option>
        <datalist>
        <input type="text" list="datalist 아이디값">

       * value = 사용자가 테이블을 선택했을 때 서버로 넘겨질 값을 지정
       * label = 사용자를 위해 브라우저에 표시할 레이블. 따로 지정하지 않을 경우, value 값을 레이블로 사용


# <textarea> 태그 - 여러 줄 입력하는 텍스트 영역 만들기
    - 한 줄 이상의 문장을 입력할 때 사용하는 폼
    - 게시판에서 게시물을 입력하거나 회원가입 양식에서 사용자 약관을 표시할 때 자주 사용
    - 여러 줄 텍스트
    - name = 다른 폼 요소와 구분하기 위해 텍스트 영역의 이름을 지정
    - cols = 너비 (텍스트 영역의 가로 너비를 문자 단위로 지정)
    - rows = 몇행 (텍스트 영역의 세로 길이를 줄 단위로 지정, 지정한 숫자보다 줄 개수가 많아지면 스크롤 막대가 생김)


# 기타 다양한 폼 요소들
    - <button> 태그
        type : submit(기본값), reset, button

    - <output> 태그
        결과 값, 계산 결과

    - <progress> 태그
        진행 상태

    - <meter> 태그
        수치 정도, 값이 차지하는 크기 표시
