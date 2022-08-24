# 화살표 함수 (arrow function)

## 화살표 함수 개념

- ```function 키워드``` 대신 ```화살표(=>)```를 사용하여 전통적인 함수 표현보다 간단한 방법으로 함수를 선언할 수 있음

<br>

## 화살표 함수 기본 문법

```js
/* 매개변수 지정 방법*/
() => { ... }  // 매개변수가 없는 케이스
a => { ... }   // 매개변수가 한 개인 경우, 소괄호 생략 가능
(a,b) => { ... }   // 매개변수가 여러 개인 경우, 소괄호 생략 불가


/* 함수 몸체 지정 방법 */
a => { return a*a }    // single line block (한 라인으로 구성된 문단)
a => a*a   // 함수 몸체가 한줄의 구문이라면 중괄호를 생략할 수 있으며 암묵적으로 return됨 (위 표현과 동일)

() => {return {i: 10};}
() => ({i: 10})   // 위 표현과 동일. 객체 반환시 소괄호 사용함

() => {   // multi line block (여러줄로 구성된 문단)
    const k = 50;
    return k*k;
};
```

## 화살표 함수 호출

- 화살표 함수는 익명함수(함수명이 없는 함수)로만 사용할 수 있음 
```js
/* ES5 */
var mulTwoTimes = function(k) {return k*k };
console.log(mulTwoTimes(50));   // 2500


/* ES6 */
const mulTwoTimes2 = a => a*a;
console.log(mulTwoTimes(30));   // 900
```


<br>

## 화살표 함수의 장점

1. 기존 함수 표현식에 비해 문법이 간결함
2. 명시적인 반환을 하므로 코드를 한줄로 작성할 수 있음
3. 다른 함수 내부에서 화살표 함수를 사용할 때 this를 재차 bind하지 않음

<br>

## 화살표 함수의 단점

1. this, super에 대한 바인딩이 없고, methods로 사용될 수 없음
2. new.target 키워드가 없음
3. (scope 지정시 사용하는) call, apply, bind methods를 이용할 수 없음
4. 생성자로 사용할 수 없음
5. yield를 화살표 함수 내부에서 사용할 수 없음

<br>

## 화살표 함수의 특징

### 기본 꼴
```js
/* 매개변수가 여러개인 경우 */
(parameter1, parameter2, ... , parameterN) => {statements}

/* 매개변수가 1개 */
(parameter) => {statements}

/* 매개변수가 없는 경우 */
() => {statements}   // 매개변수가 없는 경우 소괄호만 써줘도 됨
```


<br>

## 화살표 함수 예시
```js
const stacks = [
    "Javascript",
    "React",
    "Node",
    "sql"
];

console.log(stacks.map(stack => stack.length));  // [ 10, 5, 4, 3 ]
```

<br>

## 콜백함수로 사용하는 일반함수   VS   화살표 함수

### 콜백함수로 사용하는 일반 함수
```js
/* ES5 */
var arr1 = [1,2,3,4,5];
var mulTwice = arr1.map(function(a){
// map: 배열 내 모든 요소에 대해 주어진 함수를 호출한 결과를 모아 새로운 배열 리턴
    return a*a;
});

console.log(mulTwice);  //  [ 1, 4, 9, 16, 25 ]
```

<br>

### 콜백함수로 사용하는 화살표함수
```js
/* ES6 */
const arr1 = [1,2,3,4,5];
const mulTwice = arr1.map(a => a*a);

console.log(mulTwice);  // [ 1, 4, 9, 16, 25 ]
```

<br>


## 일반 함수의 this   VS   화살표 함수의 this

### 일반 함수의 this





<br><br>

# 일반 함수 

- 자바스크립트 상 모든 함수는 실행될 때마다 함수 내부에 this라는 객체가 추가됨


- cf) 일반 함수에서 this가 바인딩 되는 상황
1. 함수 실행시 전역(window)객체를 가리킴
2. 메서드 실행시 메서드를 소유하고 있는 객체를 가리킴
3. 생성자 실행시 새롭게 만들어진 객체를 가리킴

- <b>일반 함수</b>는 함수를 선언할 때 this에 바인딩할 객체가 정적으로 결정되는 것이 아니고, 함수를 호출할 때 <b>함수가 어떻게 호출되었는지에 따라 this에 바인딩할 객체가 동적으로 결정</b>됨

- 화살표 함수
- 화살표 함수는 함수를 선언할 때 this에 바인딩할 객체가 정적으로 결정됨
- 화살표 함수의 this는 <b>언제나 상위 스코프의 this를 지칭함</b> (Lexical this)
- call, apply, bind 메서드를 사용하여 this를 변경할 수 없음


<br><br>

# 예시로 알아보는 화살표 함수 VS 일반 함수

- 기본꼴
```js
/* 일반 함수 */
function func1(){
    ...  
}

/* 화살표 함수 */
const arrFunc1 = () => {
    ...
};
```

<br>

- this 바인딩시 차이점
```js
function normalFunc() {
    this.name = "KIM";
    return {
        name: "PARK",
        speak: function () {
            console.log(this.name);
        },
    };
}

function arrFunc() {
    this.name = "KIM";
    return {
        name: "PARK",
        speak: () => {
            console.log(this.name);
        },
    };
}

const func1 = new normalFunc();
func1.speak(); // PARK - 일반 함수는 자신이 종속된 객체를 this로 가리킴

const func2 = new arrFunc();
func2.speak(); // KIM - 화살표 함수는 자신이 종속된 인스턴스를 가리킴
```

<br>


## 생성자 함수로 사용 가능 여부에 따른 차이점
- 일반 함수는 생성자 함수로 사용할 수 있음
- 화살표 함수는 생성자 함수로 사용할 수 없음 (prototype property를 가지고 있지 않기 때문)
```js
function normalFunc(){
    this.name = "KIM";
}

const arrowFunc = () => {
    this.name = "KIM";
}

const func1 = new normalFunc();
console.log(func1.name);   //  KIM

const func2 = new arrowFunc();   // Error
console.log(func2.name);   
```


<br>

## arguments 사용 가능 여부에 따른 차이점

- 일반 함수에서는 함수가 실행될 때 암묵적으로 arguments가 전달됨

```js
function func1(){
    console.log(arguments);
    //  [Arguments] { '0': 1, '1': 2, '2': 3, '3': 4, '4': 5 }
}

func1(1,2,3,4,5);
```

<br>

- 화살표 함수에서는 함수 실행시 arguments가 전달되지 않음
```js
const arrowFunc = () => {
    console.log(arguments);
}

arrowFunc(1,2,3,4,5);
```






<br><br>

## 일반함수

- 사용예시 (reduce)
```js
const arr1 = [1,2,3,4,5];

function basicFunc(accumulator, currentValue, currentIndex, array){
    console.log("acc: "+accumulator+", cur: "+currentValue
        +", currentIndex: "+currentIndex+", array: "+array);
    return accumulator + currentValue;
}

const initialValue = 0;
const sumOfNum = arr1.reduce(basicFunc, initialValue);

console.log(sumOfNum); // 0+1+2+3+4+5 = 15
```




## 화살표 함수

- 사용예시 (reduce)
```js
const arr1 = [1,2,3,4,5];

const initialValue = 0;
const sumOfNum = arr1.reduce(
    (previousValue, currentValue) =>
        previousValue+currentValue, initialValue
);

console.log(sumOfNum); // 0+1+2+3+4+5 = 15
```


<br><br>

###### :bookmark: Ref
- [화살표 함수 1](http://wesbos.com/arrow-functions/)
- [화살표 함수 2](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/Arrow_functions)
- [템플릿 리터럴](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Template_literals)
- [함수](https://ko.javascript.info/function-basics)
- [브라우저 이벤트](https://ko.javascript.info/introduction-browser-events)
- [비동기처리와 콜백함수](https://joshua1988.github.io/web-development/javascript/javascript-asynchronous-operation/)
- [함수 바인딩](https://ko.javascript.info/bind)
- [Method](https://developer.mozilla.org/ko/docs/Glossary/Method)
- [new.target](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/new.target)
- [생성자](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Classes/constructor)
- [yield](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/yield)
- [화살표 함수 다시 살펴보기](https://ko.javascript.info/arrow-functions)
- [Arrow function - 화살표 함수](https://poiemaweb.com/es6-arrow-function)
- [자바스크립트 비동기 처리와 콜백 함수](https://joshua1988.github.io/web-development/javascript/javascript-asynchronous-operation/)
