<Day11 - 0402>
<Javascript 속성관리, 노드관리>

# Document 객체

    1. 아이디로 선택
        document.getElementById("아이디명"); - 단일 선택

    2. 클래스명으로 선택
        document.getElementsByClassName("클래스명"); - 복수개 선택

    3. 태그명으로 선택
        document.getElementsByTagName("태그명"); - 복수개 선택

    4. 네임속성으로 선택
        document.getElementsByName("name 속성명"); - 복수개 선택

    5. CSS 선택자 선택
        document.querySelector("CSS 선택자") - 단일 선택
        document.querySelectorAll("CSS 선택자") - 복수개 선택

    6. children : 자식 요소들

    7. parentElement : 부모요소 (부모는 단수개 선택)

    8. firstElementChild : 첫번째 자식 요소

    9. lastElementChild : 마지막 자식 요소

    10. previousElementSibling : 앞쪽 형제 요소

    11. nextElementSibling : 뒤쪽 형제 요소

    12. document 객체
            html : document
            head : document.head
            body : document.body

    13. form의 name 속성

---     

# 속성(Attribute)을 관리하는 메서드

    - 1. ☆ 요소의 속성 값 ☆
        : 대부분의 HTML 요소에는 속성을 설정해서 추가적인 정보를 더할 수 있음
        이를 활용해서 요소에 다른 요소와 구별되는 특별한 스타일을 입히거나 특별한 기능을 부여하기도 함

     - 2. ☆ 속성 값 가져오기 ☆  

        ① getAttrbute (조회) (거의 대부분이 문자열로 가져옴)
        : 요소 객체의 getAttrbute 메서드는 요소의 속성을 가져옴
        해당하는 속성이 없을 때는 null 또는 빈 문자열을 반환    
        요소 객체.getAttribute(속성의 이름)

        ② setAttribute (추가)
        : 요소 객체의 setAttribute 메서드는 요소의 속성을 설정함
        해당하는 속성이 없을 때는 그 속성을 새롭게 추가한 후에 설정
        요소 객체.setAttribute(속성 이름, 속성 값)

        ③ removeAttribute (삭제)
        : 요소 객체.removeAttribute(속성 이름)

        ④ hasAtrribute(속성 확인)
        : 요소 객체.hasAtrribute(속성 이름)

    - 3. ☆ 전체 속성의 목록 가져오기 ☆
        : 요소 객체에는 attributes 프로퍼티가 정의되어 있음
        이 프로퍼티는 NamedNodeMap 객체로 그 요소에 설정된 모든 속성의 속성 노드 객체가 담겨 있음
        NamedNodeMap 객체는 유사 배열 객체이며 읽기 전용
        NamedNodeMap 객체의 요소인 속성 노드 객체의 name 프로퍼티에는 속성 이름이 담겨 있으며, value 프로퍼티에는 속성 값이 담겨 있음
        NamedNodeMap 객체의 요소는 배열의 인덱스는 물론 속성 값으로도 가져올 수 있음

---

# class만을 위한 속성

    className : class 속성

        클래스만을 위한 속성 - classList 객체 (class 추가, 제거, 삭제)
            classList
                add() : 클래스 추가
                remove() : 클래스 제거
                replace() : 클래스 변경
                toggle() : 클래스가 있으면 제거, 없으면 추가
                contains() : 클래스의 존재 유무

        * 정보성 속성은 data-속성명으로 입력
          data-속성명 : document 객체에 하위 속성 dataset 객체를 통해 접근 가능

---

# HTML 요소의 내용을 읽고 쓰기

    - 1. ☆ innerHTML 프로퍼티 ☆
        : innerHTML 프로퍼티는 요소 안의 HTML 코드를 가리킴
        innerHTML 프로퍼티를 사용해서 요소 안의 코드를 읽거나 쓸 수 있음

    - 2. ☆ textContent와 innerText 프로퍼티 ☆
        : textContent 프로퍼티는 요소의 내용을 웹 페이지에 표시했을 때의 텍스트 정보를 표시함
        textContent 프로퍼티 값은 지정한 요소의 자식 노드인 모든 텍스트 노드를 연결한 값
        extContent 프로퍼티에 텍스트를 대입하면 요소의 내용을 텍스트로 변환할 수 있음

---

# 노드 생성/삽입/삭제하기

    - 1. ☆ 노드 생성하기 ☆ 

        동적 요소 생성, 변경
        document.createElement("태그명");
        document.createTextNode("텍스트명");

        : 새로운 요소 노드 객체를 생성할 때는 createElement 메서드를 사용
        var element = document.createElement(요소의 이름);
        DOM 트리 계층 구조를 뜻하는 프로퍼티(parentNode, childNode 등) 값은 모두 null
        reateElement로 생성한 객체는 메모리에 생성되어 있을 뿐 문서의 DOM 트리와는 아무런 관계가 없음

        새로운 텍스트 노드 객체를 생성할 때는 createTextNode 메서드를 사용
        ar textnode = document.createTextNode(텍스트);

    - 2. ☆ 노드 삽입하기 ☆
    
        ① 요소의 마지막에 삽입하기 : appendChild 메서드 
         - 요소 노드.appendChild(삽입할 노드)
         - appendChild 메서드로 노드 객체를 삽입하면 그 객체가 DOM 트리에 추가되고, DOM트리의 각 노드에 계층 구조를 정의하는 프로퍼티(parentNode, childNode 등)가 바뀜

         ② 지정한 자식 노드의 바로 앞에 삽입하기 : insertBefore 메서드
         - 요소 노드.insertBefore(삽입할 노드, 자식 노드)

         ③ 노드 옮기기
          - 이미 있는 노드를 appendChild와 insertBefore 메서드로 문서에 삽입하면 해당 노드를 현재 위치에서 삭제하고 새로운 위치에 삽입
          - 결과적으로 그 노드는 이동하게 됨

         ④ 노드 삭제하기
          - 노드.removeChild(자식 노드)

         ⑤ 노드 치환하기
          -  노드.replaceChild(새로운 노드, 자식 노드)

 ---

    (참고)
        부모요소.apendChild("자식 요소") -> 가장 마지막 자식 요소로 추가
        자식요소.removeChild("자식 요소") -> 자식 요소 제거
        부모요소.replaceChild("기존 요소", "새로운 요소");
        부모요소.insertBefore("기준 요소", "추가 요소") // 기준 요소 앞에 추가 요소가 추가
