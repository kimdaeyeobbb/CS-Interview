# 화살표 함수 (arrow function)

## 화살표 함수 개념

- 전통적인 함수표현의 간편한 대안

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



<br><br>

# 예시로 알아보는 화살표 함수 VS 일반 함수

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
