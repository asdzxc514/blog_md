# 6. Set & WeakSet



## Set으로 유니크한 배열 만들기

- `set` : 중복 없이 유일한 값을 저장하려고 할때 사용한다.
- 이미 존재하는지 체크할 때 유용하다.

```js
let mySet = new Set();
// console.log(toString.call(mySet));

mySet.add("중복");
mySet.add("hyejin");
mySet.add("중복");
mySet.add("abcd");
mySet.add("중복");

console.log(mySet.has('중복')); // true

mySet.forEach(function(v){
  console.log(v) // 중복,  hyejin, abcd
});

mySet.delete('중복');

mySet.forEach(function(v){
  console.log(v) // hyejin, abcd
});
```

## WeakSet 으로 효과적으로 객체타입저장하기

- `WeakSet` : 참조를 가지고 있는 객체만 저장이 가능하다.  
- 객체형태를 중복없이 저장하려고 할때 유용하다.
```js
let arr = [1,2,3,4];
let arr2 = [5,6,7,8];
let obj = {arr, arr2};

let ws = new WeakSet();

/* 
ws.add(arr); // 변수
ws.add(function(){}); // 함수

아래 3개는 오류 : Invalid value used in weak set
ws.add(111);  // 숫자
ws.add("111"); // 문자
ws.add(null);
*/

ws.add(arr);
ws.add(arr2);
ws.add(obj);

arr = null; // 이것때문에 아래 false가 나옴

console.log(ws);
console.log(ws.has(arr)+ ', '+ws.has(arr2));  // false, true
```