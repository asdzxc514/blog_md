# 9. class

## Class란?

ES6에서 클래스는 특별한 `함수`이다.  
함수를 함수 표현식과 함수 선언으로 정의할 수 있듯이  
class 문법도 **class 표현식**과 **class 선언** 두 가지 방법을 제공한다.  
**호이스팅이 일어나지않아 클래스를 먼저 선언**해야한다.

```js
class Polygon {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
}
```

## Class 표현식
```js
// unnamed 
var Polygon = class {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
};

// named
var Polygon = class Polygon {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
};
```
- 클래스 선언과 클래스 표현식의 본문(body)은 `strict mode` 에서 실행된다. [참고사이트](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Strict_mode)
- `constructor` : class 로 생성된 객체를 생성하고 초기화하기 위한 특수한 메소드이며, 클래스안에 1개만 존재한다.
- 정적 클래스 측 속성 및 프로토 타입 데이터 속성은 ClassBody 선언 **외부**에서 정의해야 한다.


## extends를 통한 클래스 상속(sub classing)
`extends`  
: 클래스 선언이나 클래스 표현식에서 다른 클래스의 자식 클래스를 생성하기 위해 사용된다. (키워드)   
subclass에 constructor가 있다면, "this"를 사용하기 전에 가장 먼저 super()를 호출해야 한다.  

`super`  
: 객체의 부모가 가지고 있는 함수들을 호출하기 위해 사용된다. (키워드)

`Object.setPrototypeOf()`  
: 기존의 생성자가 없는 객체를 확장하고 싶을때 사용한다. (메소드) 


### super를 통한 상위 클래스 호출
```js
class Cat { 
  constructor(name) {
    this.name = name;
  }
  
  speak() {
    console.log(this.name + ' makes a noise.');
  }
}

class Lion extends Cat {
  speak() {
    super.speak();
    console.log(this.name + ' roars.');
  }
}
```

***



## class 를 통한 객체생성

```js
function Health(name){
  this.name = name;
}

Health.prototype.showHealth = function(){
  console.log(this.name + "님 안녕하세요");
}

const h = new Health("HYEJIN");
h.showHealth();



// ES6 Class
class Health2 {  // 반드시 대문자로 시작해야함
  constructor(name, lastTime){
    this.name = name;
    this.lastTime = lastTime;
  }
  showHealth(){
    console.log(this.name + "님 안녕하세요");
  }
}

const myHealth2 = new Health2("HYEJIN");
myHealth2.showHealth();


console.log(myHealth2);
console.log(toString.call(Health2)); // function인것을 확인
```

모습만 클래스지 실제로는 function prototype으로 연결된 구조이다.

### Class 의 장점
1. 모듈화로 인해 가독성이 좋다
2. 여러사람들이 협업을 할 때 유용하다



## Object assign으로 JS객체만들기


## Object assign으로 Immutable 객체만들기


## Object setPrototypeOf로 객체만들기


## Object setPrototypeOf 로 객체간 prototype chain생성하기






# 10. 객체

# 11. module

# 12. Proxy

# 13. 미니 프로젝트




<article class="markdown-body">


</article>




ES6 8. function - Arrow 활용, this context, default paramaters, rest paramaters 알아보기


h("HYEJIN");