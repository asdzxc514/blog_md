# 4. Object 객체


```js
function getObj(){
  
  const name = "crong";  
  const getName = function(){
    return name;
  }
  const setName = function(newname){
    name = newname;
  }  
  const printName = function(){
      console.log(name);
  }  
  return {
    getName: getName, setName: setName, name 
    // key 와 value 값이 일치하다면 getName, setName 으로 써줘도 무방함
    // value 받아 올 수 있음 (name)
  }  
}

var obj = getObj();
console.log(obj);

// 결과
// [object Object] {
//   getName: function(){
//     return name;
//   },
//   name: "crong",
//   setName: function(newname){
//     name = newname;
//   }
// }
```
오브젝트 리터럴의 편리함! value도 return 할 수 있다!

```js
const data = {
    name,
    getName(){
        // 함수도 없이 이렇게 만들 수 있음
    },
    age
}
```
간단하게 value 값으로만 만들 수 있다!