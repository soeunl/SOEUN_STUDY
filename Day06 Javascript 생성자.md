<Day06 - 0326>
<Javascript 생성자>

# 생성자

 - 함수객체 -> 다른 객체 생산
 - 생성자를 사용하면 이름이 같은 메서드와 프로퍼티를 가진 객체를 여러개를 효율적으로 생성할 수 있음
 - 자바스크립트에서는 생성자라고 하는 함수로 객체를 생성할 수 있음
 - new 연산자로 객체를 생성할 것이라 기대하고 만든 함수를 생성자라고 함
 - 생성자는 일반 함수와 구분할 수 있도록 관용적으로 첫 글자를 대문자로 씀
 - 생성자 안에서 this.프로퍼티 이름에 값을 대입하면 그 이름을 가진 프로퍼티에 값이 할당된 객체가 생성됨
 - 생성자와 new 연산자로 생성한 객체를 생성자의 인스턴스라고 부름

    new 연산자 : 메모리에 공간을 생성하는 연산자

# 생성자의 역할

- 생성자는 객체를 생성하고 초기화 하는 역할
- 생성자 이름은 같지만 프로퍼티 값이 다른 객체(인스턴스)를 생성할 수 있음

# 생성자로 객체 생성하기

    - 생성자 함수명 : 첫 시작 문자 대문자 ★★★

    function Person() {
        this.name = "이이름";
        this.age = 40;
    }

    const p1 = new Person();

    p1 -> Person {name: "이이름", age: 40}

    const p2 = new Person();

    p1 === p2;

    -> false

# 객체가 생성되는 과정

    1. 함수 객체에 정의된 prototype 객체의 상속
    2. this 값을 상속을 받은 객체로 변경함으로써 초기화

    (참고)
        객체간의 상속
        프로토타입 체인 연결관계를 가지고 상속함
        [[Prototype]]
        .__proto__

        모든 함수
            Function.prototype 상속관계

     function Person() {
        this.name = "이이름";
        this.age = 40;
    }

        const p1 = {};

        p1;
        -> {}

        p1.__proto__ = Person.prototype; (상속하는 과정)
        -> {}

        Person.call(p1);
        -> 초기화 (값을 넣어주는 과정. this의 값을 바꾸어줌)

        p1;
        -> Person{name: "이이름", age = 40}

        (참고)
        Function.prototype.apply()
        apply() 메서드는 주어진 this 값과 배열 (또는 유사 배열 객체) 로 제공되는 arguments 로 함수를 호출
        apply(thisArg, ...)
        Function.prototype.call()
        call()은 이미 할당되어있는 다른 객체의 함수/메소드를 호출하는 해당 객체에 재할당할때 사용
        call(thisArg, ...)

person(); // window.Person();

 function Person() {
        this.name = "이이름";
        this.age = 40;
    }

        const p1 = new Person();

        p1;
        -> Person {name: "이이름", age : 40}

        p1 === p2;
        -> false

        p1.name = '(수정)이이름';

-------------------------------------------------
function Person(name, age) {
        this.name = name;
        this.age = age;
    }

    const p1 = new Person("이이름", 40);
    
    p1;
     -> Person ("김이름", 30)

    p2;
    
function Person (name, age) {
    this.name = name;
    this.age = age;
    this.showInfo = function() {
        console.log(this.name. this.age);
    };
}
const p1  = new Person ("이이름", 40)

p1;
-> Person {name: "이이름", age: 40, showInfo:ƒ}

p1.showInfo();
-> 이이름 40


# 객체를 만드는 과정

     1. function Person() {
            this.name = "이이름",
            this.age = 40;
        }

     2.  const p1 = {};

     3.   p1.__proto__= Person.prototype;
        -> {}

     4.   p1;
        -> Person {}

     5.  Person.call(p1);

     6.   p1;
        -> Person {name: '이이름', age: 40}