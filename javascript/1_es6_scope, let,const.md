# 1. scope 스코프
대부분의 프로그래밍 언어는 블록 레벨 스코프 지만,  
javascript에서는 함수 레벨 스코프(Function-level scope)를 따른다.   

`var` - 함수 스코프  / `let`, `const` - 블럭 스코프, 호이스팅 일어나지않음

## let
1. 재할당이 가능하다.
2. 동일한 이름을 갖는 변수를 중복해서 선언할 수 없다. 


```js
var name = "global var";

function home(){
    var homevar = "homevar";
    for(var i=0; i<100; i++){  // let

    }
    console.log(i);
}
home();  // var 일때 결과 : 100, let 일때 결과 error
```

## let 과 closure

```html
<ul>
    <li>Javascript</li>
    <li>Java</li>
    <li>Python</li>
    <li>django</li>
</ul>
```

```js
var list = document.querySelectorAll("li");
for(let i=0; i<list.length; i++){   // let
    list[i].addEventListener("click", function(){ // ☆
        console.log((i+1) + " 번째 리스트입니다!!")  // 0터 시작이라 +1 해줌
    });
}
```
 
여기서 `var` 를 사용할 경우 결과는 모두 "5번째 리스트입니다!!" 로 출력된다. (이때 i가 클로저 변수)
  
☆ 표시된 줄에 콜백함수 안에 i의 값이 전역인 for문안에 i 값을 참조한다.  
for문은 0, 1, 2, 3 을 뽑아내고, 4에서 끝이난다.

console.log 에 +1 을 해줌으로써  
1,2,3,4로 for문이 돌고, for문이 끝나는 5에서 멈추기 때문에
콜백함수는 마지막 값인 5로 출력이 되는것이다.

`let` 을 사용하여 깔꼼하게 끝!

## const
1. 반드시 선언과 동시에 할당이 이루어져야 한다.
2. 재할당이 불가능하다. 
3. 배열과 오브젝트의 값을 변경하는 것은 가능하다.



```js
const arg = [0, 1];
const obj = {foo: 'bar'};
 
const newArg = [...arg];  // 스프레드(spread) 문법
const newObj = Ojbect.assign({}, obj);
 
newArg[0] = 10;
newObj.foo = 'rab';  // obj의 foo의 값은 그대로임 
 
console.log(arg, obj);
// [0, 1], {foo: 'bar'}
 
console.log(newArg, newObj);
// [10, 1], {foo: 'rab'}
```

## 스프레드(spread) 문법 - [...arr]
```js
// 함수호출
myFunction(...iterableObj);

// 배열 리터럴, 문자열
[...iterableObj, '4', 'five', 6];

// 객체 리터럴( new in ECMAScript 2018)
let objClone = { ...obj };
```

- 배열 복사 및 합치기
```js
//ES5에서 배열 합치기
var arr1 = [2,3,4]
var arr2 = [5,6,7]
var merged = arr1.concat(arr2)

//ES6에서 배열 합치기
const newMerged = [...arr1, ...arr2]

//ES5에서 배열 복사하기
var copiedArr = arr1.slice()
//ES6에서 배열 복사하기
const copiedArr = [...arr1]


//ES5에서 오브젝트 합치기
var obj1 = {a: 3}
var obj2 = {b: 4}
var merged = Object.assign({}, obj1, obj2)

//ES5에서 오브젝트 복사하기
var copiedObj = Object.assign({}, obj1)

//ES5에서 오브젝트 복사하기
const copiedObj = {...obj1}
```


- 배열을 이어붙이는 더 나은 방법  (concat, unshift)
```js
var arr1 = [0, 1, 2];
var arr2 = [3, 4, 5];
// arr2 의 모든 항목을 arr1 에 붙임
arr1 = arr1.concat(arr2);
```
```js
var arr1 = [0, 1, 2];
var arr2 = [3, 4, 5];
// arr2 의 모든 항목을 arr1 의 앞에 붙임
Array.prototype.unshift.apply(arr1, arr2) // arr1 은 이제 [3, 4, 5, 0, 1, 2] 가 됨
```

## var, let, const 의 사용
ES6를 사용한다면 var는 사용하지 않는다. (혹은 자제한다)  
const를 기본으로 사용한다.  
변경이 될 수 있는 변수는 let을 사용한다. 