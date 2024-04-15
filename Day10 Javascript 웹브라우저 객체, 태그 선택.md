<Day10 - 0401>
<Javascript 웹브라우저 객체, 태그 선택>

# 웹 브라우저에서 자바스크립트가 하는 일

    - 웹 페이지의 Document 객체 제어(HTML 요소와 CSS 스타일 작업)
    - DOM 이라는 API를 활용
    - 웹 페이지의 Window 객체 제어 및 브라우저 제어
    - 웹 브라우저에 내장된 다양한 객체를 활용하며, 대표적인 객체로 Location, Navigator 등이 있음
    - 웹 페이지에서 발생하는 이벤트 처리
    - Http를 이용한 통신 제어
    - XMLHttpRequest 객체를 활용

---

# 코어 객체

    - 내장 생성자 객체
        Array
        String
        Object

    - 내장 객체
        math
        JSON

---        

# 호스트 객체 - 웹브라우저 객체가 탑재

    - window (모두 브라우저와 관된 기능임)
        location : 브라우저 URL과 관련된 객체
        history : 방문 기록과 관련된 객체
        screen : 화면 정보
        navigator : 브라우저 환경정보

        document

        REPL 명령

---

# 웹 브라우저에서 자바스크립트 실행 순서

    - 서버가 html 문자열 응답 -> 브라우저 -> document 객체 변환 -> DOMContentLoaded 이벤트 발생 -> document 객체 변환 완료 -> 트리구조 재구성(이진트리 - 검색에 최적화, 검색을 빨리 하기 위해, 요소를 빨리 찾기 위해) -> DOMTree

    ① 웹 브라우저로 웹 페이지를 열면 가장 먼저 Window 객체가 생성. Window 객체는 웹 페이지의 전역 객체로 웹 페이지의 탭마다 생성됨

    ② Document 개체가 Window 객체의 프로퍼티로 생성되며 웹 페이지를 해석해서 DOM 트리의 구축을 시도. readyState 프로퍼티의 초깃값은 "loading"이라는 문자열

    ③ HTML 문서는 HTML 구문을 작성 순서에 따라 분석하며 Document 객체 요소와 텍스트 노드를 추가해 나감

    ④  HTML 문서 안에 script 요소가 있으면 script 요소 안의 코드 또는 외부 파일에 저장된 코드의 구문을 분석. 오류가 발생하지 않으면 그 시점에 코드를 실행. script 요소의 구문을 분석해서 실행할 때는 HTML 문서의 구문 분석이 일시적으로 막히고, 자바스크립트 코드의 실행을 완료한 후에는 일시적으로 막혔던 HTML 문서의 구문 분석을 재개함

    ⑤ HTML 문서의 모든 내용을 읽은 후에 DOM 트리 구축을 완료하면 document.readyState 프로퍼티 값이 "interactive"로 바뀜

    ⑥ 웹 브라우저는 Document 객체에 DOM 트리 구축 완료를 알리기 위해 DOMContentLoaded 이벤트를 발생

    ⑦ img 등의 요소가 이미지 파일 등의 외부 리소스를 읽어 들여야 한다면 이 시점에 읽어들임

    ⑧ 모든 리소스를 읽어 들인 후에는 document.readyState 프로퍼티 값이 "complete"로 변경. 마지막으로 웹 브라우저는 Window 객체를 상대로 load 이벤트를 발생

    ⑨ 이 시점부터 다양한 이벤트(사용자 정의 이벤트, 네트워크 이벤트)를 수신하며, 이벤트가 발생하면 이벤트 처리기가 비동기로 호출됨

    (주의)
    - HTML 문서를 다 읽어 들이지 못한 상태에서 자바스크립트로 HTML 요소를 조작하면, 조작할 요소 객체가 없으므로 자바스크립트 코드가 의도대로 동작하지 않음
    - 이미지 등의 외부 리소스를 읽어 들이는 시점이 DOM 트리 구축이 끝난 후라는 점에 유의. load 이벤트는 이미지 등의 외부 리소스를 모두 읽어 들인 후에 발생하기 때문에 외부 리소스를 읽어 들이는 시간이 걸리는 만큼 사용자가 기다려야 하는 시간도 길어짐
    - 이를 방지하려면 load 이벤트 대신 DOMContentLoaded 이벤트의 이벤트 처리기에 초기화 작업을 작성한 함수를 등록
    * document.addEventListener("DOMContentLoaded", function(e) {
	// 초기화 작업을 작성 
    }, false);

---

# async와 defer 속성

    - async와 defer 속성은 script 요소의 논리 속성으로 HTML5부터 추가된 속성
    - 둘 다 src 속성을 가진 script 요소에는 적용할 수 있지만 인라인 스크립트에는 사용할 수 없음
    - 이들 속성을 사용하면 자바스크립트 코드를 실행할 때 HTML 구문 분석을 막지 않음

<script async src="../scripts/sample.js"></script>
<script defer src="../scripts/sample.js"></script>

    - async 
        : script 요소에 async 속성을 설정하면 script 요소와 코드가 비동기적으로 실행.
        여러 개의 script 요소에 async 속성을 설정하면 다 읽어 들인 코드부터 비동기적으로 실행하므로 실행 순서가 보장되지 않음. 
        읽어 들이는 순서에 의존하는 script 요소에는 async 속성을 설정하지 말아야 함!

    - defer 
        : defer 속성을 설정한 script 요소는 DOM 트리 구축이 끝난 후에 실행.
        DOM 구축이 끝난 시점에 실행되기 때문에 자바스크립트 코드로 요소 객체에 이벤트 처리기를 등록하는 등의 초기화 작업을 할 수 있음.

        외부 링크 연결하는 방식 <script defer src="..."></script>
        -> 스크립트 실행은 DOMContentLoaded 이벤트 발생 이후에 진행
        -> defer 속성은 DOMContentLoaded 이벤트의 대안으로 활용할 수 있음★★★

---        

# window 객체 ★★★

    - 클라이언트 측 자바스크립트에서 가장 중요한 객체는 Window 객체
    - Window 객체는 전역 객체이며, 전역 변수는 Window 객체의 프로퍼티
    - 웹 브라우저에서 사용할 수 있는 다양한 객체가 모두 Window 객체의 프로퍼티

    1. ☆ window 객체의 주요 프로퍼티 ☆
        pageXOffset : 가로 방향 스크롤 정도
        pageYOffset : 세로 방향 스크롤 정도

        - 스크롤바를 제외한 현재 창의 보이는 영역
        * innerWidth
        * innerHeight

        - 스크롤바를 포함한 현재 창의 보이는 영역
        * outerwidth
        * outerHeight 

    2. ☆ window 객체의 주요 메서드 ☆
        console
            .log("값")
            .dir(..) : 객체의 이름과 값 형태로 구성 출력
            .error(값) : 글자 색이 빨간색
            .trace() : console.trace()에 도달하기까지 위치를 쌓아가듯이(stack) 보여주는 기능

        open(주소, 창의 이름, 옵션) -> 팝업
                - 옵션
                    width : 너비
                    height : 높이
                    scrolling
                    location
        
        opener : open을 호출해서 열어준 창

        alert("메세지") - 알림 메세지
        prompt("메세지") - 입력 창, 반환값이 입력한 값
        confrim("메세지") - 확인, 취소, 확인 -> true, 취소 -> false, 진행 여부 통제시 많이 사용

---        

# Location 객체
    
    - 주소창과 관련된 객체
    - Location 객체는 창에 표시되는 URL을 관리
    - Location 객체는 window.Location 또는 location으로 참조할 수 있음

    1. ☆ Location 객체의 주요 프로퍼티 ☆
        - 주소의 정보
        Location 객체의 속성은 살아있다
    (추가하면 추가되고, 제거하면 제거된다)

    2. ☆ Location 객체의 주요 메서드 ☆
        - 주소에 대한 통제 기능
            assign(주소) : 주소 이동
                - 방문 기록이 남는 주소 이동
                - location.href="주소";

            replace(주소) : 주소이동
                - 방문 기록이 남지 않는 주소 이동

            reload() : 새로고침

            시크릿모드 -> 방문기록 X
            CTRL + SHIFT + N

---            

# History 객체

    - History 객체는 창의 웹 페이지 열람 이력을 관리
    - 방문 기록과 관련된 객체
    - 창의 웹 페이지 열람 이력을 관리

    1. ☆ History 객체의 주요 프로퍼티 ☆
        length : 방문 기록 갯수
        scrollRestoration : auto - 페이지의 스크롤 위치 복구, manual - 스크롤 위치 복구 X, 문서 상단 위치

    2. ☆ History 객체의 메서드 ☆
        브라우저의 기능과 관련
        back() : 뒤로 1단계 이동
        forward() : 앞으로 1단계 이동
        go(숫자) : 숫자 -> 음수 : 뒤로 숫자만큼 이동
                           양수 : 앞으로 숫자만큼 이동
        pushState(state, title, url) : 창의 웹 페이지 열람 이력을 추가, 페이지는 이동하지 않음

---

# Naviator 객체

    - 스크립트가 실행 중인 웹 브라우저 등의 애플리케이션 정보를 관리
    - Navigator 객체는 브라우저 테스트에 활용

---

# Screen 객체

    - 화면(모니터) 크기와 색상 등의 정보를 관리
    - 사용할 수 있는 화면이란 화면에서 작업 표시줄 등을 제외한 나머지 부분
    - Screen 객체를 사용하면 웹 페이지가 어떤 크기의 단말기에 표시되고 있는지를 알 수 있음
    - 스마트 폰 등의 작은 화면에 표시할 때 크기가 작은 글꼴을 사용하거나 이미지를 작게 표시하는 등의 대응이 필요할 때 사용할 수 있음

---

# Document 객체

    - Document 객체는 창에 표시되고 있는 웹 페이지를 관리함
    - 이 객체로 웹 페이지의 내용물인 DOM 트리를 읽거나 쓸 수 있음
    - Document 객체는 클라이언트 측 자바스크립트에서 가장 중요한 객체임

    1. ☆ DOM 트리 ☆
        - 웹 페이지의 내용은 Document 객체가 관리함
        - 웹 브라우저가 웹 페이지를 읽어 들이면 렌더링 엔진은 웹 페이지의 HTML 문서 구문을 해석하고, Document 객체에서 문서 내용을 관리하는 DOM 트리라고 하는 객체의 트리 구조를 만들어냄
        - DOM 트리를 구성하는 객체 하나를 노드(Node)라고 함
        - Document 객체는 모든 노드의 조상 노드이며 DOM트리의 루트임

    2. ☆ Document 객체 주요 메서드 ☆
        선택!★★★
        노드 객체 가져오기. 선택을 위한 메서드

        - 아이디로 선택 : document.getElementById("아이디명");
            => 단수개 선택

        - 클래스명으로 선택 : document.getElementsByClassName("클래스명");
            => 복수개 선택

        - 태그명으로 선택 : document.getElementsByTagName("태그명"); => 복수개 선택

        - name 속성으로 선택 : document.getElementsByName("속성명"); => 복수개 선택

        - CSS 선택자 형식으로 선택 : document.querySelector("CSS 선택자 형식"); => 단수개 선택 (맨 처음 거)

        - CSS 선택자 형식으로 선택 : document.querySelectorAll("CSS 선택자 형식"); => 복수개 선택

        children : 자식 요소들
        parentElement : 부모요소
        firstElementChild : 첫번째 자식 요소
        lastElementChild : 마지막 자식 요소
        previousElementSibling : 앞쪽 형제
        nextElementSibling : 뒤쪽 형제

        html : document
        head : document.head
        body : document.body

        양식의 이름값
            양식이름. 입력항목 이름


 

        

