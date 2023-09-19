1장
자바스크립트는 인터프리터 언어다(한 줄마다 번역해서 실행)
동적 타입 언어다. (프로그램 실행 도중 변수가 저장되는 타입이 동적으로 바뀔 수 있음)
함수가 일급 객체다. (함수에 함수를 인수로 넘길 수 있음)



3장
데이터 타입 중 원시 타입은 숫자, 문자열 등이 있고 객체 타입은 참조 타입이다.
자바스크립트에서는 숫자가 모두 64비트 부동소수점이다.
보간 표현법은 ${...}이다.



4장
객체 생성하기 - var card = { suit: "하트", rank: "A" };
{}부분이 객체 리터럴이다. suit(프로퍼티 이름), "하트"(프로퍼티 값)
프로퍼티 값을 읽거나 쓸때는 card.suit나 card["rank"] 을 사용한다. - 객체에 없는 프로퍼티를 읽을 때는 undefined를 반환
var obj = {}; 처럼 선언시 빈 객체가 생성됨
card.value = 14; 처럼 없는 프로퍼티 이름에 값을 대입하면 새로운 프로퍼티가 추가된다.
반대로 delete card.rank; 처럼 프로퍼티를 삭제할 수 있다.
console.log("suit" in card); -> true (in을 사용해 프로퍼티의 유무 확인 가능)

객체는 참조타입이다. var a = card; 라고 했을 때, a.suit = "스페이드" 를 한다면 card.suit도 스페이드로 바뀐다.

함수 선언 - function square(x) {return x * x}
함수 선언문도 끌어올림이 가능하기 때문에 함수 선언 전 함수를 실행해도 문제가 없다.

let x;와 같이 let을 이용해 선언하면 { }안에서만 유효범위를 갖는다.
const c = 2;(const는 반드시 초기화 해야한다.)로 선언시, c=5처럼 도중에 변경이 불가능하다.

var squre = function(x){return x*x;};처럼 함수 리터럴로 함수를 정의할 수 있는데, 이는 무명함수 혹은 익명함수라고 부르며, 선언문 끝에 반드시 세미콜론을 붙여야한다. /주의 - 무명함수는 함수 선언문을 끌어올리지 않는다.

생성자 - 자바스크립트에는 클래스가 없기 때문에 생성자라고 하는 함수로 객체를 생성할 수 있다.
function Card(suit, rank){
    this,suit = suit;
    this.rank = rank;
    }
var card = new Card("하트","A"); - Card {suit:"하트",rank:"A"}
var card={}; card.suit="하트"; card.rank="A"; 로 표현해도 같다.



6장



7장
조건문 - if, else if, else로 이루어짐
switch문 - switch(표현식){ /자바스크립트에서는 표현식이 꼭 상수가 아니어도됨
    case 표현식 1: ...
    ...
    defalt: ...
}
for/in 문 - for(변수 in 객체 표현식) {}
var obj = {a:1,b:2,c:3};
for(var p in obj){
    console.log("obj."+p+" = "+obj[p])
} -> a = 1이런식으로 나옴