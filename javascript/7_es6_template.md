# 7. Template



## Template 처리
ES6에서 문자열 처리를 보다 간편하게 할 수 있는 템플릿을 제공한다.  
Template literal을 사용하여 거추장스러운 '**+**' 이나 '**\n**'을 더이상 사용하지 않아도 된다.  
`${ }` 안에는 **변수** 또는 연산식 등의 **표현식**이 들어갈 수 있다.



```js
let name = "HYEJIN";
// 1 왼쪽에 있는 `
let grettingTemplate = `
    Hi, ${name}!
    Have a nice day!
`; 
console.log(grettingTemplate);
// 결과
// Hi, HYEJIN!
// Have a nice day!
```



## Tagged Template literals
- 간단한 기본 예제
```js
let name = "HYEJIN";
let num = "010-1234-1234";
console.log(`hi, ${name}! Have a nice day! ${num} is your number`);
// 결과 : hi, HYEJIN! Have a nice day! 010-1234-1234 is your number
```
tagged template을 사용하여 text와 value로 분리할 수 있다.  
**text**는 공백 문자를 기준으로 배열의 형태로 파라미터가 들어오며,  
${ } 안의 표현식은 **value**라는 파라미터로 String type으로 들어온다.

- 배열관련 응용된 예제
```js
const data = [
  {
    name: 'COFFEE',
    order: true,
    items: ['americano', ' latte']
  },
  {
    name: 'CAFE',
    order: false,
  },
  {
    name: 'HYEJIN',
    order: true,
    items: ['americano', ' milk', ' green-tea']
  }
]

function fn(tags, name, items){
//   console.log(tags);
  if(typeof items === "undefined"){
    items = "<span style='color: red; margin-top: -20px;'>주문 가능한 상품이 없습니다.</span>";
  }
  return (tags[0] + name + tags[1] + items + tags[2]);
}

data.forEach((valueee) => {
 let template = fn`<h2 style='margin-top: 80px;'>Welcome Come  ${valueee.name} !</h2>
  <h3>주문가능항목 : <span style='font-size: 14px;'>${valueee.items}</span></h2>`;
  document.body.innerHTML += template;
});

// 결과
// Welcome Come COFFEE !
// 주문가능항목 : americano, latte
// Welcome Come CAFE !
// 주문가능항목 : 주문 가능한 상품이 없습니다.
// Welcome Come HYEJIN !
// 주문가능항목 : americano, milk, green-tea
```