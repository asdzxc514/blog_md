# 5. Destructuring (파괴)



## Destructuring Array
배열 및 객체에서 원하는 정보만을 뽑아내는 새로운 방법이다.  
이 방법을 쓰면 index 번호를 굳이 지정하지 않아도 된다.

```js
const data = [1, 2, 3, 4];
const [d1, d2, d3] = data; // 할당 연산자 왼쪽에 배열 형태의 변수 리스트가 필요하다.  
console.log(d1, d2, d3); // 1 2 3
```

- `[선언할변수명, …]` 처럼 배열 인덱스 대신 배열 인덱스에 해당하는 위치에 변수명을 넣어서 사용
- 왼쪽의 **변수 리스트**와 오른쪽의 **배열**은 **배열의 인덱스를 기준**으로 할당된다.

```js
const today = new Date();
const formattedDate = today.toISOString().substring(0, 10);
const [year, month, day] = formattedDate.split('-');
console.log([year, month, day]); // [ '2019', '02', '25' ]
```
배열에서 필요한 요소만 추출하여 변수에 할당하고 싶은 경우에 유용하다


## Destructuring Object

```js
let obj = {
    name: 'hyejin',
    address: 'Korea',
    age: 10
}

let {name, age} = obj;
console.log(name, age); // 결과 hyejin, 10

// 변수명 다르게 줄때
let {name: myName, age: myAge} = obj;
console.log(myName, myAge); // 결과 hyejin, 10
```
`let {프로퍼티명, …} = 객체` : 각각의 프로퍼티가 변수로 추출된다.

`{프로퍼티명:지정할변수명, …}` : 변수명 다르게 줄때

```js
const todos = [
  { id: 1, content: 'HTML', completed: true },
  { id: 2, content: 'CSS', completed: false },
  { id: 3, content: 'JS', completed: false }
];

// todos 배열의 요소인 객체로부터 completed 프로퍼티만을 추출한다.
const completedTodos = todos.filter(({ completed }) => completed);


console.log(completedTodos); 
// 결과 [ { id: 1, content: 'HTML', completed: true } ]
```

## Destructuring 활용 JSON파싱

```js
let jsonData = [
  {
    title: "첫 번째 입니다",
    author: "1. Hyejin",
    category: { aaa : "1. Javascript"}, // 중첩 객체
    publishDate: "2019-02-25"
  }
  ,{
    title: "두 번째 입니다.",
    author: "2. Hyejin",
    category: { aaa : "2. Javascript"}, // 중첩 객체
    publishDate: "2019-02-26"
  }
]

let [{title: aTitle, author: aAuthor}] = jsonData
console.log(aTitle, aAuthor); // 첫 번째 입니다 , 1. Hyejin

let [, {title: bTitle, author: bAuthor}] = jsonData
console.log(bTitle, bAuthor); // 두 번째 입니다 , 2. Hyejin


// 중첩 객체의 경우 : 2개 모두 불러올 경우
const [p1, p2] = jsonData;
console.log(p1.category.aaa+ ', ' + p2.category.aaa); 
//1. Javascript, 2. Javascript
```


## Destructuring 활용 _Event객체전달

```html
<div>JavaScript</div>
```
```js
document.querySelector("div").addEventListener("click", function({type, target}){
  console.log(type+ ', '+target.tagName);
}); // 결과 click, DIV
```