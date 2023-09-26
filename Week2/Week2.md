8장
*함수를 정의하는 방법
1. 함수 선언문으로 정의 //호출문이 앞에 있어도 호출 가능(외에는 변수 할당 후 호출가능)
    funtion square(x) {return x*x;}
2. 함수 리터럴로 정의
    var square = function(x) { return x*x; }
3. Function 생성자로 정의
    var square = new Function("x","return x*x");
4. 화살표 함수 표현식으로 정의
    var square = x => x*x;

*함수를 호출하는 법
객체의 프로퍼티에 저장된 값이 함수 타입일 때는 그 프로퍼티를 매서드라고 부른다.
obj.m = function() {....};
obj.m();으로 호출
*즉시 실행 함수
(function(){...})(); -> 익명함수를 정의하는 동시에 실행 가능

*함수 인수
함수 인수 생략 - 함수 정의식에 작성된 인자 개수보다 인수를 적게 전달해서 함수를 실행하면 인수에서 생략된 인자는 undefined 가 된다.
Arguments 객체 - Arguments 객체는 '유사 배열 객체'이다.
function f(x,y) { [0]=1, [1]=2로 들어옴
    arguments[1]=3; // y의 값도 같이 바뀜
    console.log("x = "+ x + ", y = " + y);
}
f(1,2) => x=1,y=3

*재귀함수
익명함수 사용 - arguments.callee를 사용하면 익명 함수도 재귀 호출을 할 수 있다. (arguments.callee가 지금 실행중인 함수를 가리키기 때문)
ex) return n*arguments.callee(n-1);
주의) 재귀 호출은 반드시 멈춰야 한다.(조건문을 사용해서 n값이 1이하일 때 재귀 호출을 멈추자)
재귀 호출로 문제를 간단하게 해결할 수 있을 때만 사용한다. (호출된 횟수만큼 메모리 소비량이 늘어나서 대부분 while문이나 for문이 이해가 더 쉽고 메모리 공간도 덜 차지한다.)

*자바스크립트는 싱글스레드
자바스크립트는 싱글스레드이기 때문에 호출 스택에 쌓인 실행 문맥(함수 또는 코드)을 위에서부터 아래로 차례차례 실행합니다. 실행 문맥 단위의 작업을 차례대로 실행하므로 실행 문맥 하나의 작업이 끝날 때까지 또 다른 실행 문맥의 작업을 살행하지 않는다.

*this값
var tom={
    name: "Tom",
    sayHello: function(){
        console.log("Hello! " + this.name);
    }
};
tom.sayHello(); -> Hello! Tom

var huck = {name : "Huck" };
huck.sayHello = tom.sayHello;
huck.sayHello(); -> Hello! Huck //this.name이기 때문

호출될 때의 상황에 따라 this가 가리키는 객체가 바뀐다. (실행 문맥의 디스 바인딩 컴포넌트가 가리키는 객체가 무엇인지에 따라 this가 가리키는 객체가 바뀜)
1. 최상위 레벨 코드의 this // this는 전역 객체를 가리킨다.
    console.log(this); -> Window 
2. 이벤트 처리기 안에 있는 this
    이벤트가 발생한 요소 객체를 가리킨다.
3. 생성자 함수 안에 있는 this
    사용자가 정의한 생성자 함수 안에 있는 this는 그 생성자로 생성한 객체를 가리킴
4. 생성자의 prototype 메서드 안에 있는 this
    그 생성자로 생성한 객체를 가리킨다.
5. 직접 호출한 함수 안에 있는 this

*클로저
주의) 반복문 안에서 클로저 만들기
반복문 안에서 클로저를 만들었을 때, 
예) e[i].onclick=function(){...} (0을 누르면 0, 1이면 1이 출력되어야 하는데 상관없이 3이 출력됨) Why? 바깥의 i를 참조하는 클로저가 되어서(onclick 이벤트 처리기 때문) -> let i를 이용하면 이런 오류를 막을 수 있음

*이름 공간
주의) 전역 유효범위 안에서 이름이 같은 변수나 함수를 선언하면 자바스크립트 엔진이 그 프로그램의 첫머리로 끌어올려서 변수 또는 함수를 단 하나만 생성한다.
이러한 오류를 피하기 위한 방법
객체를 이름 공간으로 활용하기 - var myApp = myApp || {};
으로 작성해두면 myApp이 이미 정의되어있을 때는 그것을 사용하고 그렇지 않으면 빈 객체를 myApp에 할당한다.
함수를 이름 공간으로 활용하기 - 전역변수와 함수 안의 지역변수가 있을 때, 함수 안에서는 지역변수만 사용하기 때문에 이런 방법을 통해 오류를 방지할 수 있다.

*객체로서의 함수
bind 매서드 - var sayToTom = say.bind(tom); //항상 this가 객체 tom을 가리킴

*고차함수란 함수를 인수로 받거나 함수를 반환하는 함수를 고차함수라고 한다.

*화살표 함수
 var square = function(x) {return x*x;};
 var square = (x) => {...}; //둘이 같다, 인수가 하나인 경우 괄호 생략가능
 var f = (x,y,z) => {...};
 var f = () => {...}; //인수가 없는 경우 괄호 생략 불가능
 //몸통 안의 문장이 return 뿐이면 중괄호와 return 키워드를 생략할 수 있음
 var f = (a,b) => ({x:a,y:b}); //몸통 안에 return 문장만 있더라도 함수의 반환값이 객체리터럴이면 ()로 묶어야 함
 // 화살표 함수의 this값은 정의할 때 결정되므로, call이나 apply 메서드를 사용하여 this를 바꾸어 호출해도 this 값이 바뀌지 않는다.
 // 화살표 함수 안에는 arguments 변수를 사용할 수 없다
 // 화살표 함수는 생성자로 사용할 수 없다
 // 화살표 함수는 yield 키워드를 사용할 수 없다.(제너레이터로 사용할 수 없다)

 *이터레이터
 var a=[5,4,3]; // Symbol.iterator 메서드는 이터레이터를 반환하는 함수다
 var iter = a[Symbol.iterator](); 
 *for/of 문
 for(var v of "ABC") console.log(v); // "A","B","C"를 순서대로 표시함

9장
 객체의 생성방법
 1. 리터럴로 생성
    var card = {suit:"하트", rank:"A"};
 2. 생성자로 생성
    function Card(suit,rank){
        this.suit=suit;
        this.rank=rank;
    }
    var card = new Card("하트", "A");
 3. Object.create로 생성
    var card = Object.create(Object.prototype,{
        suit: {
            value: "하트",
            writable: true,
            enumerable: true,
            comfigurable: true
        },
        rank: {
            value: "A",
            writable: true.
            enumerable: true,
            comfigurable: true
        }
    });

프로토타입
*생성자 안에서 메서드를 정의하는 방식의 문제점 - 생성자 안에서 this 뒤에 메서드를 정의하면 그 생성자로 생성한 모든 인스턴스에 똑같은 메서드가 추가된다. 이는 메모리를 잡아먹게됨.
*프로토타입 객체
*내부 프로퍼티 [[Prototype]] or __proto__
모든 객체는 내부 프로퍼티를 가지고 있으며, 이것은 함수 객체의 prototype 프로퍼티와는 다른 객체이다.

*데이터의 캡슐화
객체 안에서 var _name="Tom"; -> 이 코드의 변수 _name은 즉시 실행 함수의 지역 변수이므로 함수 바깥에서 읽거나 쓸 수 없다.

*프로퍼티가 있는지 확인하기
-in 연산자
    console.log("name" in person); //->true 이 객체가 소유한 프로퍼티
    console.log("name" in person); //->false 프로퍼티가 없음  
    console.log("name" in person); //->true 상속받았을 때
-hasOwnProperty 메서드
    console.log(person.hasOwnProperty("name")); // -> true 이 객체가 소유한 프로퍼티 ->false: 상속받은 프로퍼티
-propertyIsEnumerable ->true: 이 객체가 소유한 열거 가능 프로퍼티
->false : 상속받은 프로퍼티 or 열거할 수 없는 프로퍼티

10장
배열의 매서드 p390~391

*다차원 배열의
- 2차원 배열의 생성
    var x = new Array(3); //우변을 리터럴 []로 표기할 수 있다
    for(var i=0;i<3;i++){
        for(var j=0;j<3;j++){
            x[i][j]=count++; //우변을 리터럴 []로 표기할 수 있다
        }
    }
    배열 리터럴을 이용해 표현할 수도 있다.
    var x =[
        [1,2,3],
        [4,5,6],
        [7,8,9]
    ];
배열이란 Array 타입의 객체를 말하는데, 다음과 같은 성질을 갖는다.
1. 0 이상의 정수 값을 프로퍼티 이름으로 갖는다.
2. length 프로퍼티가 있으며, 요소를 추가하거나 삭제하면 length 프로퍼티 값이 바뀐다. 또한 length 프로퍼티 값을 줄이면 그에 따라 배열 크기가 줄어든다.
3. 프로토타입이 Array.prototype이므로 Array.prototype의 메서드를 상속받아서 사용할 수 있다. 또한 instanceof 연산자로 평가하면 Array 생성자 함수로 생성된 객체로 표시된다.

11장
*버그에 대처하기
-Strict 모드 사용
    function f(x){
        "use strict";
        y=x;
    }
    f(2);
-Strict 모드로 설정하면 바뀌는 점
    1. 변수는 모드 선언해야만 한다.
    2. 함수를 직접 호출할 때, 함수 안의 this 값이 undefined가 된다. 비 Strict 모드에서는 함수 안의 this값이 전역 객체의 참조가 된다.
    3. with 문은 사용할 수 없다.
    4. 함수 정의문에 같은 이름의 인수가 있으면 문법 오류가 발생한다.
    5. 객체에 같은 이름의 프로퍼티가 있으면 문법 오류가 발생한다.
    6. NaN, Infinity, undefined를 표기하면 TypeError가 발생한다.
    7. arguments[i]는 호출되었을 때의 인수 값을 유지한다. 비 Strict 모드에서는 arguments[i]가 인자의 별명이다. 따라서 한쪽을 수정하면 다른쪽도 바뀐다.
    8. arguments.callee를 읽을 수 없다. 읽기를 시도하면 TypeError가 발생한다.
    9. eval로 실행한 코드는 호출자의 유효 범위 안에 새로운 변수나 함수를 선언할 수 없다.

-console 디버깅, p438
-웹 브라우저의 개발자 도구를 사용한 디버깅, p439

*try/catch/finally 문
 try/catch/finally 문은 예외가 던져졌을 때 그것을 잡아서 처리한다.
 try블록 안에 예외(오류)가 발생할 가능성이 있는 코드를 작성하고, catch블록의 처리가 끝나면 그 변수는 사용할 수 없게 된다. 그리고 finally블록은 반드시 실행되는 코드이다.

12장
*정규표현식
    var reg = new RegExp("abc"); // RegExp 생성자로 생성
    var reg = /abc/; // 정규 표현식 리터럴로 생성
*문자 클래스
 문자 클래스인 대괄호 안에서 하이픈을 사용하면 문자의 범위를 지정할 수 있다.
 [a-z] //전체 소문자 중 한개 [abcx-z] // a,b,c,x,y,z,중 한개
 [a-zA-Z0-9] // 모든 알파벳과 숫자 중 문자 한개
*부정 문자 클래스
 [^...]
 console.log(/[^0-9]/.test("137")); // false
 대괄호 안의 패턴이 ^로 시작하지 않으면 ^을 문자로 인식한다.

*문자열 검색하기
 search 메서드 
    var s = "1 little,2 little indian";
    console.log(s.search(/little/)); // 2 - 일치한 최초 문자열 첫문자위치
    console.log(s.search(/\d)); // 0 - 일치한 최초 문자열 첫째 문자위치
    console.log(s.search(/\bindian/)); // 18 -일치한 i의 위치
    console.log(s.search(/3\s/)); // -1 -일치하지 않음
 replace 메서드
    console.log(s.replace(/indian/,"boy")) // 1 little,2 little boy
 치환패턴, 문자열 추출, split 메서드 p 473~476

13장
자바스크립트를 사용하지 않는 웹 페이지는 정적(static) 웹 페이지이다. 자바스크립트를 사용하면 웹 페이지를 동적(Dynamic)으로 만들 수 있다.
*자바스크립트가 하는 일
1. 웹 페이지의 Document 객체 제어(HTML 요소와 CSS 스타일 작업)
2. 웹 페이지의 Window 객체 제어 및 브라우저 제어
3. 웹 페이지에서 발생하는 이벤트 처리
4. HTTP를 이용한 통신 제어

* HTML에 자바스크립트를 삽입하는 방법 p486
* 웹 브라우저에서 자바스크립트 실행 순서 p487
* Window 객체 p493~
* 창 제어하기 p505~