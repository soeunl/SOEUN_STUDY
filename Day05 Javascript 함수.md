<Day05 - 0325>
<Javascript 함수>

# 함수★
  - 함수의 이름은 변수(지역변수) 함수는 객체
  - 일련의 처리를 하나로 모아 언제든 호출할 수 있도록 만들어 놓은 것
  - 함수의 입력 값을 인수, 함수의 출력 값을 반환값이라고 함
  - 기능을 담당함
  - 함수 안에도 함수를 정의할 수 있음
  - 자바스크립트 함수는 객체임★★★
  - 자바스크립트는 함수도 객체여서, 함수를 변수로 사용할수도 있음 (지역변수로)

        function 함수명 (인수) {   
          처리 로직 
          return 출력 반환값
        }

  1. 함수 선언문으로 함수 정의하기
      - function 함수명 (매개변수, ...) {
        // 실행 코드 ...

        return 반환값;
      }

      - function calc(x) {
            var y = x * 2 + 1;
            return y; (반환값. 내보내 주는 값. return이 없으면 undefined가 나옴)
        }
        calc(3); x = 3;
        x => 매개변수 (투입되는 변수)

  2. 함수 호출
      - 함수를 호출하려면 함수 이름 뒤에 소괄호 인수를 묶어서 입력 

  3. 함수의 실행흐름
    - 호출된 코드에 있는 인수가 함수 정의문에 대입
    - 함수 정의문의 중괄호 안에 작성된 내용이 순차적으로 실행
    - return 문이 실행되면 호출된 코드로 돌아감. return 문의 값은 함수의 반환값
    - return 문이 실행되지 않은 상태로 마지막 문장이 실행되면, 
      호출한 코드로 돌아간 후에 undefined가 함수의 반환값이 됨

    - function add(num1, num2) {
          var result = num1 + num2;
          return result;
      }
      
      add : 변수 => 함수 객체의 주소값

      (참고) console.dir... => 객체의 속성과 값 형태 출력

  4. 함수 선언문의 끌어올림

    - 함수 객체(실행 X) -> 번역(평가) -> 실행 가능 객체(EC - Exrcution Context) -> 실행

    - global EC {
      변수 레코드 - window의 하위 속성으로 변수가 정의
        windows.num0 = 5;
        외부 변수 레코드 참조 = null
    }

    * 유효범위 체인 (Scope) ☆☆☆

    outer EC {
      변수 레코드 객체 {
        num1: 10
      }

      외부 변수 레코드 참조: global EC 변수 레코드 주소 : window
    }

    inner EC {
      변수 레코드 객체 {
        num2 : 20,
        result : 35
      }

      외부 변수 레코드 참조: outer EC 변수 레코드 주소

      this 바인딩 : 호출한 객체의 주소값

    }

  5. 값으로서의 함수
    - 함수(X), 함수 객체(O) - 값이 있음. 변수에 대입 가능

    * 일등 함수 : 함수 = 값. 변수와 함수를 동등하게 취급함. 함수 == 값. 함수를 값으로 취급
      자바스크립트 함수는 일등 함수 
      - 매개변수로 함수 객체를 사용할 수 있음
      - 반환값으로 함수 객체를 사용할 수 있음 (클로저) 

      -> 함수형 프로그래밍이 가능

  6. 참조에 의한 호출과 값에 의한 호출


# 변수의 유효범위
      전역 유효범위와 지역 유효범위
        -> 함수 지역
        -> 유효범위 체인 (Scope)

      var : 함수 지역이 유효범위

      let, const -> {...}

      let : 변수 - 값 변경이 가능

      const : 상수 - 값 변경이 불가

      -> 변수는 기본적으로 const로 정의, 변경이 필요한 경우만 let으로 사용    

# 함수 안에서 변수 선언 생략
  - 변수를 선언하지 않은 상태에서 값을 대입하면 전역변수로 선언됨
  - 지역변수로써만 정의하는 경우는 반드시 변수 선언을 해야 함

# ★★★객체간의 상속 (__proto__)
  - 상속
      : 상속받은 객체가 상속을 해준 객체의 자원을 공유할 수 있게 됨

      [[prototype]] : 프로토타입 체인 - 상속 관계 링크
                                       상속 관계를 의미함
                                       연결하면 상속이 발생
                                      __proto__ 속성을 통해서 접근


# forEach
  var fruits = ["Apple", "Oranage","mango"];
  fruits.forEach(function(fruit) {
      console.log(fruit);
  });

* function outer() {
  function inner () { // 지역 변수 inner에 함수 객체의 주소 대입

  }
}


# v8엔진, 렌더링 엔진
  - 자바스크립트 엔진


# 함수 리터럴로 함수 정의하기
  - const 변수명 = 함수 객체
  - 함수를 변수에 할당하기 위해 값으로 생성하는 방법
  - 함수 리터럴은 이름이 없느 함수 이므로 익명함수 또는 무명함수라고 함
  * 익명 함수 - 이름 없는 함수
  - 함수 선언문에서는 끝에 세미콜론(;)을 붙일 필요가 없으나 함수 리터럴을 사용할땐 끝에 세미콜론(;)을 붙여야 함
  ★★★ 함수 리터럴로 정의한 함수는 끌어올리지 않는다



# ★★★ 
function outer(callback) {
    console.log(callback === inner);
    callback();
}

function inner() { // var inner = function () { ... }
    console.log("inner 호출");
}

outer(inner);

true
inner 호출

outer(function() { // callback = function() {...}
    console.log("inner 호출");
});

false

inner 호출
