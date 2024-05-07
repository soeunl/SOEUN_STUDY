<Day06 - 0326>
<Javascript 함수, 유효범위체인, this, Argument>

# 4가지 모두 동일한 기능

1.  function outer() {
    var inner = function() {

        };

    }

2.  function outer () {
    function inner () {

        }

    }

3.  var outer = function () {
    var inner = function() {

        };

    }

4.  var outer = function () {
    function inner () {

        }

    }

---

var num1 = 10;
function outer() {
var num2 = 20;

    function inner () {
        var num3 = 30;

        return num1 + num2 + num3;
    }

    var result = inner ();

    console.log(result);

}

---

# 유효범위 체인 (Scope)

함수 객체(실행 X) => 평가(번역) => 실행 가능 객체 (EC - Execution Content)

global EC {
변수 레코드 - window

    window.num1 = 10

    외부 변수 레코드 참조 : null

}

outer EC {
변수 레코드 {
num2 : 20
}

    외부 변수 레코드 참조: Global EC 변수 레코드 주소 - window 객체의 주소 값

}

inner EC {
변수 레코드 {
num3 : 30
}

    외부 변수 레코드 참조: outer EC 변수 레코드 주소

}

=> 유효범위 체인 (Scope)
올라가면서 상대적으로 접근한다. 본인이 가지고 있으면 지역변수. 상단에서 가지고 있으면 전역변수

---

# 함수 선언문의 끌어올림

    - 자바스크립트 엔진은 변수 선언문과 마찬가지로 함수 선언문을 프로그램의 첫머리로 끌어올림
    - 함수 선언문은 프로그램 어떤 위치에서도 작성할 수 있음

console.log(window);
var result = add(10, 20);
console.log(result);

function add(num1, num2) {
return num1 + num2;
}

--> 번역되는 과정에서 모두 위로 올라가므로 함수가 어디에 나오든 상관없음

---

# let과 const

let, const - 지역 범위 {...}

let : 변수 선언자
const : 상수 선언자 - 값을 변경 X

- 변수 선언 const -> 변경이 필요한 경우 let 변경

---

# this

this : 호출한 함수의 객체 주소
this 바인딩 - this 지역변수 값 결정

const person = {
name : "이이름",
age : 40,
showInfo : function () {
console.log(this);
}
};

person.showInfo();
-> {name : "이이름", age : 40, showInfo : ƒ}

const person2 = {
name : "김이름",
age : 30,
};

person2.showInfo = person.showInfo;

console.log(this);

person2;
{name : "김이름", age : 30, showInfo : ƒ}

person2.showInfo();
{name : "김이름", age : 30, showInfo : ƒ}

const showInfo = person.showInfo;

showInfo(); // windows.showInfo();

---

# 가변길이의 인수 목록 (Argument 객체)

- 가변적인 매개변수를 정의할 때 사용

argument - 인수(매개변수) : 함수에 정의된 내용
arguments.length : 인수 개수
parameter - 인자 : 매개변수로 사용된 값, 매개변수에 대입된 값
arguments는 모든 매개변수와 인수의 값을 담고 있음

    function add(num1, num2) {
        console.log(arguments)
    }

(참고)
parameter : 인자 - 매개변수 (ex) num1, num2
argument : 인수 - 매개변수로 사용된 값 (ex) 10, 20

---

# 전개 연산자, 나머지 연산자 : ... ★★★

function sum (... params) {
console.log(params);
}

sum (10, 20, 30, 40, 50);
-> (5)
[10, 20, 30, 40, 50]

---

# ...은 가변적인 변수

function sum (...params) {
let total = 0;

    for (let i = 0; i < params.length; i++) {
        total += params[i];
    }
    return total;

}

sum (10, 20)
-> 30
sum(10, 20, 30);
-> 60

---

function add(a, ...params) {
console.log('a', a, 'params', params);
}

add(10, 20, 30, 40, 50);

a 10 params -> (4) [20, 30, 40, 50]

---

function add(a, b) {
b = b || 10;

    console.log('a', a, 'b', b)

}

add(5)

a 5 b 10

= 같다

function add(a, b = 10) {
console.log('a', a, 'b', b)
}

---

# 즉시 실행 함수

- 함수 정의와 동시에 호출

(function(){
// 즉시 실행코드 console.log("즉시 실행");
})(); - 정의하자마자 실행이 됨

---

    const result = (function(num1, num2) {
        return num1 + num2;
    })(10, 20);

---

    (function(매개변수 정의 ,...) {
        // 실행코드
    }) (인자)

---

    (function() {
        console.log("실행");
    })();

---

    (function(num1, num2) {
        const result = num1 + num2;
        return result;
    })(10, 20);

---
