# 6. Map & WeakMap 알아보기



## Map & WeakMap 추가정보를 담은 객체저장하기

Array를 개선한 자료구조 : Set, WeakSet  
Object를 개선한 자료구조 : Map, WeakMap

`Map` : key, value 구조이다.

```js
let wm = new WeakMap();
let myfun = function(){};
// 이 함수가 얼마나 실행됐지? 를 알려고 할때.

wm.set(myfun, 0);

console.log(wm);  // WeakMap {ƒ => 0}

let count = 0;
for(let i=0; i<10; i++){
  count = wm.get(myfun); // get value
  count++;
  wm.set(myfun, count);
}

console.log(wm);  // WeakMap {ƒ => 10}

myfun = null;
console.log(wm.get(myfun)); // undefined
console.log(wm.has(myfun));  // false
```



## WeakMap 클래스 인스턴스 변수 보호하기
- WeakMap의 키는 오직 Object형 뿐이다.  
- 키로 원시 데이터형은 허용되지 않는다. (가령 Symbol은 WeakMap 키가 될 수 없음)
- 다른 강한 키 참조가 없는 경우 모든 항목은 가비지 컬렉터에(하단 내용 참고) 의해 WeakMap에서 제거된다.
  
  
- `WeakMap` : new, .has(), .get(), .set(), .delete() 만 지원
- `WeakSet` : new, .has(), .add(), .delete() 만 지원
- WeakSet에 저장되는 **value**, WeakMap에 저장되는 **key**는 반드시 **객체**여야 한다.

```js
const wm = new WeakMap();  // 프라이빗한 변수 만들기1


function Area(width, height){
  wm.set(this, {width, height});  // 프라이빗한 변수 만들기2
}

Area.prototype.getArea = function(){
  const {width, height} = wm.get(this);
  return width * height;
}

let myarea = new Area(20,10);
console.log(myarea.getArea()); // 200
console.log(myarea.height); // undefined , 외부에서 접근 불가
myarea = null;

console.log(wm.has(myarea));  // false
```

***

### 1. 메모리의 생명주기
> [ 메모리 할당 ]  
> 프로그램이 사용할 수 있도록 운영체제가 메모리를 할당하는 단계  
> 저수준의 언어는 이를 개발자가 명시적으로 처리해줍니다.  
> 고수준의 언어는 개발자가 이를 신경쓰지 않아도 됩니다.

> [ 메모리 사용 ]   
> 할당된 메모리를 실제로 프로그램이 사용하는 단계  
> 개발자가 필요에 따라 읽기와 쓰기 작업을 진행합니다.  

> [ 메모리 해제 ]   
> 프로그램에서 필요하지 않은 메모리를 전체를 되돌려 주어 다시 사용하게 만드는 단계  
> 메모리 할당 작업과 마찬 가지로 저수준은 이를 명시합니다.

```js
var n = 374; // 숫자에 대한 메모리 할당
var s = 'sessionstack'; // 문자에 대한 메모리 할당
var o = { a: 1, b: null }; // 객체 및 그 값에 대한 메모리 할당
var a = [1, null, 'str']; // (객체와 같음) 배열과 그 값에 대한 메모리 할당
function f(a) { return a + 3; } // 함수에 대한 할당 - 함수는 호출할 수 있는 객체
someElement.addEventListener('click', function() { // 함수 표현식 또한 객체를 할당
  someElement.style.backgroundColor = 'blue';
}, false);
```
변수와 함수를 선언하고 함수의 표현식을 이용하는 것이 전부 메모리를 할당하는 과정이다.

### 2. 가비지 컬렉션
사용이 완료된 메모리를 정리하는 것

### 3. 가비지 컬렉터 (Garbage Collector)  
프로그래머가 동적으로 할당한 메모리 중 더 이상 사용하지 않는 영역을 자동으로 찾아내어 해제해주는 것
- 프로그래밍을 하기가 훨씬 쉬워짐
- 메모리에 관련된 버그가 발생할 확률도 낮아짐

가비지 콜렉션 알고리즘의 핵심 개념은 `참조` 이다.


```js
// 기본
function Area(height, width){
  this.height = height;
  this.width = width;
}

Area.prototype.getArea = function(){
  return this.height * this.width;
}

let myarea = new Area(10,20);
console.log(myarea.getArea());  // 200
console.log(myarea.height);  // 10
```

```js
// WeakMap 활용   
const wm2 = new WeakMap();  // 프라이빗한 변수 만들기1


function Area2(height, width){
  wm2.set(this, {width, height});  // 프라이빗한 변수 만들기2
}

Area2.prototype.getArea = function(){
  const {width, height} = wm2.get(this);
  return width * height;
}

let myarea2 = new Area2(10,20);
console.log(myarea2.getArea()); // 200
console.log(myarea2.height); // undefined , 외부에서 접근 불가
```