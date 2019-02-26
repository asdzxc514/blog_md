# 8. function


## Arrow function Rule
ES6의 arrow function에는 몇 가지 규칙이 존재하며 대부분의 lamda에서도 비슷한 규칙을 가지고 있어서 lamda를 사용해본 경험이 있다면 어색하지 않을 것이다.  
1. Parameter와 화살표 사이에서 개행할 수 없다.
2. Parameter가 하나일 때는 괄호를 생략할 수 있다.
3. Parameter가 없으면 소괄호( ( ) )만 작성한다.
4. Block scope({ })를 지정하지 않고 한 줄로 arrow function을 사용할 때는 return이 생략될 수 있다.
5. 그 반대로 block scope를 사용한다면 return을 명시해줘야 한다.



## Arrow function의 활용

```js
// 기본
let newArr = [1,2,3,4,5].map(function(value, index, object){ 
    return value * 2; 
});
console.log(newArr);  // 1번, [2, 4, 6, 8, 10]

// arrow 사용
let newArr2 = [1,2,3,4,5].map( (v)=> { 
    return v * 2; 
});
console.log("arrow newArr2", newArr2);   // 2번, [2, 4, 6, 8, 10]

// arrow 사용에서 return 생략가능
let newArr3 = [1,2,3,4,5].map( (v)=> v * 2 );
console.log("arrow newArr3", newArr2);   // 3번, [2, 4, 6, 8, 10]
```

- 바뀐내용
1. function(value, index, object){ return value * 2; }
2. (v)=> { return v * 2; }
3. (v)=> v * 2  
(v)=> ( v*2 ) 이렇게 써도 같음

***
## Arrow function 의 this context
```js
const myObj = {
  runTimeout(){
    setTimeout(function(){
      this.printData(); // 여기서의 this 는 window를 가르키기때문에 아래 bind 로
    }.bind(this), 200); // 에러(this.printData is not a function)를 없앰
  },  
  printData(){
    console.log("hi HYEJIN~!");
  }
}
myObj.runTimeout();  // hi HYEJIN~~


// arrow function
const myObj2 = {
  runTimeout(){
    setTimeout( ()=> {
      this.printData(); // 여기서의 this 는 myObj2 를 가르키기 때문에 에러가 나지않음
    }, 200); 
  },
  
  printData(){
    console.log("hi HYEJIN !!");
  }
}

myObj2.runTimeout();  //hi HYEJIN !!
```
**Arrow Function은 `this`를 bind하지 않는다!**

***
## function default paramaters
```js
function sum(value, size){
  size = size || 1;  // 3만 넣었을경우 NaN이 나오는것을 방지, 기본 1
  return value * size;
}
console.log(sum(3,10)); // 10
console.log(sum(3)); // 3 


// default prameters
function sum2(value, size=1){
  return value * size;
}
console.log(sum2(3,10)); // 10
console.log(sum2(3)); // 3 


// default prameters, object 형식
function sum3(value, size={value:1}){
  return value * size.value;
}
console.log(sum3(3,{value:3}));  // 9
console.log(sum3(3));  // 3 
```

## rest paramaters

- 기본 구문
```js
function f(a, b, ...theArgs) {
  // ...
}
```

함수의 마지막 파라미터의 앞에 **...** 를 붙여 (사용자가 제공한) **모든 나머지 인수를 "표준" 자바스크립트 배열로 대체**한다.  
마지막 파라미터만 "Rest Paramaters" 가 될 수 있다.


- 옛날 방식
```js
function checkNum(){
  const argArray = Array.prototype.slice.call(arguments);
  console.log(toString.call(argArray));  // [object Array]
  const result = argArray.every( (v) => typeof v === "number" );
  console.log(result);  // false
}

const result = checkNum(10,2,3,4,5,"문자");
```

- rest paramaters
```js
function checkNum(...argArray){ // 매개변수에 ...이 들어갔다 = 배열로 받는다
  console.log(toString.call(argArray));  // [object Array]
  const result = argArray.every( (v) => typeof v === "number" );
  console.log(result); // false
}

const result = checkNum(10,2,3,4,5,"문자");
```
위 아래 모두 같은 결과를 나타낸다.  
몇 개의 인자가 들어갈지 모를 때 `...argArray`로 (배열로) 받아서 사용 할 수 있다.



`toString.call()` : 자주 사용하는 타입체크 