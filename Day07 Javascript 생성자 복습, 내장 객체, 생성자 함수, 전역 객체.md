<Day07 - 0327>
<Javascript 생성자 복습, 내장객체, 생성자 함수, 전역 객체>

# 생성자 복습
    - prototype
        new를 통해 만듬

        (1) 함수 객체의 prototype 객체의 상속 (상속)
        (2) this가 prototype 객체를 상속받은 객체로 주소 변경 (초기화)

            Function.prototype
                apply (thisArg, ...)  => 초기화 과정
                call (thisArg, ...)

                this로 정의된 값이 초기화 될때마다 새로운 함수객체가 만들어짐. 매번!!

    -  prototype

    객체가 정해지면 상속을 통해 기능을 공유(상속받은 곳의 자원을 씀)
    매서드가 매번 만들어지는게 아니라 상속을 하면 됨
    자원을 공유 또는 상속받은 자원을 공유하기 위해 만듬
    
    ★ 객체를 만드는 과정은 함수 생성자 객체에 있는  prototype 자원을 공유하기 위한 것임 ★

    ★ 공유할 기능을 정의하기 위해 prototype 자원을 상속받음 ★

    상속을 하려면 prototype이 꼭 필요!!
    배열을 만들면 Array.prototype 기능으로 생성


생성자 함수 객체
    - 객체에서 객체를 생산하는 객체
    - prototype 객체 : 생성자 함수로 역할을 할 수 있음 prototype이 없으면 생성자 역할을 할 수 없음

    new 생성자함수();
        (1) prototype 객체의 상속
            상속을 왜 할까?
                - 생성자 함수.prototype에 정의된 자원을 공유하기 위해
                    * 자원의 종류 : 속성, 함수, 메서드 => 여기에 정의된 기능들을 공유하기 위해
                    * 객체가 생성이되면 공유를 위한 자원 연결
                    
        (2) this 값 -> 현재 생성될 객체의 주소로 바뀜 -> 생성자 함수 호출 -> 초기화


* 연산자 instanceof => 체인 확인. prototype 연결관계 체크, 출처를 체크

* 모든 객체의 시작점은 object.prototype

---

# 내장 객체

    자바스크립트 객체
        * 코어 객체
            - 내장 생성자 함수 객체

            - 내장 객체
                : Math - 수학과 관련된 편의 메서드가 있는 객체
                : JSON

        * 호스트 객체 : 실행 환경에 따라서 추가된 객체
            - 웹브라우저 객체 
                : 현재 브라우저에만 탑재가 되어 있는 객체
                : 웹브라우저의 기능과 관련된 객체
                : 가장 상위 객체는 window 객체

                window
                    location 객체 - 브라우저의 주소와 관련된 기능, 정보
                    history 객체 - 브라우저의 방문 기록과 기능
                    screen 객체 - 화면
                    navigator 객체 - 정보성 객체

                    documents 객체 - 웹 문서를 다루는 객체


1. 내장 생성자
    - 자바스크립트에 처음부터 포함된 내장 생성자 (함수)

        1. Object
            const 변수명 = new Object();
                         = {...}
            object.prototype = 가장 상위 정점

            prototype
                .toLocaleString()
                    Locale : 지역화
                            - 그 지역의 표기법에 맞게 변경해서 출력

            Object.getOwnPropertyDescriptor()
            Object.getOwnPropertyDescriptors()

            * 데이터 프로퍼티 * 
                value - 값
                writable - false일때는 값을 변경할 수 없음
                enumerable - fasle일때는 열거 불가 (배제할 수 있음)
                configurable - fasle -> 설정 변경 불가, 삭제 불가
                                fasle로 되어 있어도 예외
                                - writable이 true -> 단 한번만 false로 변경 가능
                -> 변경
                    Object.defineProperty
                          .defineProperties

                (참고)
                    속성 : 통제 기능 포함

                Object.preventExtentions(): 객체의 새로운 속성 추가 불가

                * Object.seal(..): 객체 밀봉
                                    - 삭제 불가, 속성 추가 불가
                                    - 값 변경 가능

                * Object.freeze(..): 객체 동결
                                    - 삭제 불가, 속성 추가 불가
                                    - 값 변경도 불가

                 - 변수에 값을 직접 대입하는 것은 통제가 안됨

            * 접근자 프로퍼티 *
                - 함수 형태의 단축 표현법으로 정의
                - set 함수명 - 값을 변경하는 접근자 속성
                - get 함수명 - 값을 조회하는 접근자 속성
                - enumerable
                - configurable

                얕은 복사와 깊은 복사
                얕은 복사 -> 주소 복사
                깊은 복사 -> 완전히 다른 객체로 새로 만드는 복사

            * 전개 연산자 *
                : 깊은 복사 가능
                : ... 으로 표현

            (참고) 
                entries : 이름-값 쌍으로 조회
                Map.Entry : 이름 - 값의 쌍


    <wrapper 생성자 객체>

        2. String
            wrapper 생성자 객체

            indexOf(...) 문자열의 위치 번호 (0 부터 시작 좌 -> 우)
            lastIndexOf(...) : 문자열 위치 번호 (우 -> 좌)
                        - 문자열을 찾이 못하면 -1을 반환함
        3. Number
            wrapper 생성자 객체
            NaN : Not a Number - 숫자가 아니다
                  isNaN(...) 숫자가 아니면 true, 숫자이면 false
                  -> Number(값) -> NaN 반환 -> true
                  

                  Number -> 함수 그대로 사용 : 문자열 -> 숫자 변환

                  typeof num1 === 'number' : 숫자 판별 가능

                  parseInt(...) : 문자열, 실수 -> 정수로 변환 (정수로 바꾸어 주는 함수)
                  parseFloat(...) : 문자열, 정수 -> 실수로 변환

                  int -> 정수 - 소수점이 없는 수, 0, 1, 10, -1, -2
                  float -> 실수 - 소수점이 있는 수 1.123

                  parse -> 변환(변경)

                  toFixed(...) -> 소숫점자리 지정한 숫자대로 표기하고 문자열로 변경

        4. Boolean
            wrapper 생성자 객체
                - 함수처럼 사용했을 경우 : 값에 대한 평가 -> 실제 논리값으로 변경

        5. Array
            const 변수명 = new Array(...)
                         = [...] 
                         = Array.prototype

                         (참고)
                         자바스크립트의 배열은 배열이 아닌 배열객체임
                         배열 - 같은 자료형이 연속해서 나열된 형태
       
        6. Date - 날짜 조회 또는 변경
            날짜와 시간
            년도 : getFullYear() / setFullYear()
            월 : getMonth() 0~11 (0이 1월을 의미하고, 11이 12월을 의미함) / setMonth()
            일 : getDate() / setDate()
            요일 : getDat() 0~6 / 0-일, 6-토
            시간 : getHours() / setHours()
            분 : getMinutes() / setMinutes()
            초 : getSecond() / setSeconed()

            const date = new Date(); 
            date;   // 객체 생성 시점의 날짜와 시간


            const date = new Date();
            const strDate = `${date.getFullYear()}-${date.getMonth()+1}-${date.getDate()}`;
            strDate;


            const date = new Date();
            date.setDate(date.getDate() - 7); // 7일전
            date;


            getTime(): 1970.1.1 자정 -> 1000분 1초 단위로 카운트 수리 -> Epoch Time -> 초단위 -> Timestamp
                => (예) 유일한 값으로 ID를 만들 때 -> UID


            - Date.now() : 현재 시간이 Epoch Time

            - Date.parse(문자열 날짜) : 문자열 날짜 -> Date 객체로 변환

            달력
                (1) 이번달이 몇일로 끝나는지
                    - 다음달 1일에서 1일을 차감하면 현재 달의 마지막 날짜가 나옴

                (2) 이번달 1일이 몇 요일에 시작하는지
                    - getDay(): 0~6 => 5


                <달력 만들기>
                const date = new Date();
                const firstDate = new Date(date.getFullYear(), date.getMonth(), 1);

                const nextMonth = new Date(date.getFullYear(), date.getMonth(), 1);

                nextMonth.setMonth(nextMonth.getMonth() + 1);
                nextMonth.setDate(nextMonth.getDate() - 1);
                nextMonth;


                function add(num1, num2) {return num1 + num2;}
                const add10 = add.bind(this, 10);
                add10(20)
                30

        7. Function
            prototype
            apply
            call
            bind

        8. RegExp
            정규표현식
        9. Error
            try {

            } catch(e) {

            }


2. Function 생성자
    - Function은 함수를 생성하는 내장 생성자
    - Function 생성자로 생성한 함수는 전역 변수와 자신의 지역변수만 읽고 쓸 수 있다는 단점이 있어서 함수를 동적으로 생성해야 하는 특별한 상황 외에는 사용하지 않음

        Function 생성자 함수 객체 -> 생성
            Function.prototype
                apply
                call
                bind

            class는 생성자함수객체

---            

# ES6부터 추가된 주요 내장 생성자
    1. Symbol : 심벌을 생성 
    2. Promise : 처리 지연 및 비동기 처리를 관리하는 수단을 제공
    3. Map : key/value 맵을 생성
    4. Set : 중복을 허용하지 않는 데이터 집합을 생성

---

# 기타 내장 객체
    JSON
        (Javascript Object Nation) - 자바스크립트 객체 표기법
        모든 플랫폼에 통일된 형식으로 데이터를 보내기 위해
        자바스크립트 객체 표기법을 빌려서 사용
        (이름과 값 형태의 문자열)
        {
            "이름": "값",
            "이름": "값",
            ...
        }

     .parse(...) : JSON 문자열을 자바스크립트 객체로 변환
     .stringfy(...) : 자바스크립트 객체 -> JSON 문자열로 변환 / 직렬화

    Math
        - 수학 관련 편의 함수, 상수
        - PI : 원주율
        - round(...) : 반올림
        - floor(...) : 버림
        - ceil(...) : 올림
        - abs(...) : 절대값
        - sqrt (...) 

---

# 전역 객체

- 전역 객체의 프로퍼티는 프로그램의 어느 위치에서나 사용할 수 있음
- 자바스크립트 인터프리터가 시작될 때 혹은 웹 브라우저가 새로운 페이지를 읽어 들일 때마다 새로운 전역객체가 생성됨
- 클라이언트 측 자바스크립트에서는 Window 객체가 전역 객체임

1. 전역 프로퍼티
	- undefined, NaN, Infinity

2. 생성자 
	Object(), String(), Number() 등

3. 전역 함수
	parseInt(), parseFloat(), isNaN() 등 

4. 내장 객체
	Math, JSON, Reflect


