# 7. Destructuring 과 Set 을 활용한 로또 번호 생성기 (예제)



```js
const SETTING = {
    name : "lucky lotto",
    count : 6,
    maxNumber : 45
};

const {count, maxNumber} = SETTING;

var lotto = new Set;

function getRandomNumber(maxNumber) {

    let tmp = Math.floor(Math.random()*maxNumber) + 1;
    lotto.add(tmp);

};

for(let i=0; i < count; i++){

    getRandomNumber(maxNumber);
    if(lotto.size !== i+1){ 
        i--
    }

}

lotto.forEach( v => console.log(v));
```



# 8. Template

# 9. function

# 10. 객체

# 11. module

# 12. Proxy

# 13. 미니 프로젝트



<article class="markdown-body">



</article>

ES6 7. Destructuring 과 Set 을 활용한 로또 번호 생성기 (예제)
