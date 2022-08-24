# 화살표 함수

## 화살표 함수의 장점

1. 간결한 문법
2. 명시적인 반환을 하므로 코드를 한줄로 작성할 수 있음
3. 다른 함수 내부에서 화살표 함수를 사용할 때 this를 재차 bind하지 않음

<br>

# 예시로 알아보는 화살표 함수 VS 일반 함수

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
- [화살표 함수](http://wesbos.com/arrow-functions/)
- [템플릿 리터럴](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Template_literals)
- [함수](https://ko.javascript.info/function-basics)
- [브라우저 이벤트](https://ko.javascript.info/introduction-browser-events)
- [비동기처리와 콜백함수](https://joshua1988.github.io/web-development/javascript/javascript-asynchronous-operation/)
