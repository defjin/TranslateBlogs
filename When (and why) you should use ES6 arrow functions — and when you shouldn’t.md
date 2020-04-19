When (and why) you should use ES6 arrow functions — and when you shouldn’t

https://medium.com/free-code-camp/when-and-why-you-should-use-es6-arrow-functions-and-when-you-shouldnt-3d851d7f0b26

# 언제 arrow function(화살표함수)을 써야하고, 언제 쓰지 말아야하는가? 

Arrow functions(also called "fat arrow functions")는 의심의 여지 없이 ES6의 가장 유명한 기능 중 하나이다. 이것은 함수를 간결하게 사용하는 새로운 방법이다.


ES5 문법에 따른 함수가 있다.
``` javascript
function timesTwo(params) {
    return params * 2
}

timesTwo(4); // 8
```

arrow function 으로 표현된 정확히 같은 기능을 하는 함수가 있다.(ES6)

``` javascript
var timesTwo = params => params * 2

timesTwo(4); // 8
```

훨씬 짧아졌다. 암시적으로 값을 돌려주기 때문에 중괄호와 return 문을 생략할 수 있다. (블록이 없는 경우에만 가능하다 - 자세한 것은 아래에서...)

ES5의 함수와 비교해서 화살표 함수가 어떻게 다르게 동작하는지를 이해하는 것이 중요하다. 


## Variations
 
 화살표 함수에는 다양한 문법이 가능하다. 일반적인 것들부터 살펴보자. 

### 1. No parameters

인수가 없다면 => 앞에 빈 괄호를 넣을 수 있다. 

``` javascript
() => 42
```

사실은, 괄호조차도 쓸 필요가 없다. 
``` javascript
_ => 42
```

### 2. Single parameter

 인수가 하나인 경우에는 괄호는 선택할 수 있다. 

``` javascript
 x => 42 || (x) => 42
```

### 3. Multiple parameters

 괄호가 필수이다. 

``` javascript
(x,y) => 42
```

### 4. Statements(as opposed to expressions)

 가장 기본적인 형태로, function expression은 값을 생성한다. 반면 function statement 가 액션을 수행한다.

 화살표 함수에서, statements는 중괄호 {} 를 반드시 써야하는 것을 기억하는 것이 중요하다. 중괄호가 있다면, 무조건 `return` 을 써야한다. 


 if 문을 가지고 있는 화살표 함수의 예시를 보자.

 ``` javascript
 var feedTheCat = (cat) => {
     if (cat === 'hungry'){
         return 'Feed the cat';
     } else {
         return 'Do not feed the cat';
     }
 }
 ```

### 5. "Block body"

 함수가 블록 안에 있다면, 명시적으로 return 문을 사용해야 한다. 

 ``` javascript
 var addValues = (x,y) => {
     return x+y
 }
 ```

### 6. Object literals

만약 객체 리터럴을 리턴하려고 한다면, 괄호로 싸야한다. 괄호는 인터프리터에게 괄호 안에 있는 것을 평가하도록 강제하고 그래야 객체 리터럴이 리턴된다. 


## Syntactically anonymous

 화살표 함수는 익명함수라는 것은 중요하다. 

 이러한 익명성은 몇 가지 이슈를 야기한다. 

 1. 디버그하기 힘들다.

 error가 생긴다면, 정확한 함수의 이름과 정확히 몇 번째 줄에서 발생했는지를 알기 어렵다. 

 2. No self-referencing

 만약 함수가 자기 자신을 참조하는 것이 필요하다면, 작동하지 않을 것이다. (ex. 재귀, unbind가 필요한 이벤트 핸들러 등.)


## Main benefit : No binding of 'this'

전통적인 함수 표현식에서 `this` 키워드는 이것이 호출된 컨텍스트에 따라 다른 값으로 바인딩된다. 그러나 화살표 함수를 사용할 때는 `this`는 사전적(lexcically)으로 바인딩된다. 이 경우에는 화살표 함수를 포함하고 있는 코드에서 `this`를 사용한다. 


 예를 들어, 아래의 `setTimeout` 함수를 살펴보자.
 
 ``` javascript
 //ES5

 var obj = {
     id: 42,
     counter: function counter() {
         setTimeout(function() {
             console.log(this.id);
         }.bind(this), 1000);
     }
 }
 ```

 ES5 예제에서는 `this` 컨텍스트를 함수 안으로 전달하기 위해서는 `.bind(this)`가 필요했다. 기본적인 `this`는 undefined 이다. 

 ``` javascript 
 var obj = {
     id: 42, 
     counter: function counter() {
         setTimeout(()=> {
             console.log(this.id);
         }, 1000);
     }
 }
 ```

 ES6에서 화살표 함수는 `this` 키워드에 바인딩 될 수 없다. 그래서, 사전적으로 상위 스코프로 올라가서 그것이 정의되어 있는 스코프에서의 `this` 값을 사용한다.  


 ## When you should not use Arrow functions

 몇 가지 화살표 함수에 대해서 배우고나서, 필자는 여러분들이 화살표 함수가 일반 함수를 대체할 수 없다는 것을 이해하기를 바란다. 

  다음은 화살표 함수를 사용하지 말아야하는 예들이다. 

  1. Object methods 

  ``` javascript
  var cat = {
      lives : 9 
      jumps : () => {
          this.lives--;
      }
  }
  ```

 `cat.jumps`를 호출하면, `lives`의 값은 감소하지 않는다. `this`가 어디에도 바인딩 되어 있지 않고 이것의 상위 스코프에서 `this`의 값을 상속받기 때문이다. 

 2. Callback functions with dynamic context

  만약 여러분의 컨텍스트가 동적으로 동작하길 원한다면, 화살표 함수는 옳은 선택이 아니다. 아래의 이벤트 핸들러를 살펴보자. 

  ``` javascript
   var button = document.getElementById('press')
   button.addEventListener('click', ()=> {
       this.classList.toggle('on');
   });
  ```

 버튼을 클릭하면, TypeError를 얻게 될 것이다. `this`가 버튼에 바인드된 것이 아니라 부모 스코프에 바인드되어있기 때문이다. 

 3. When it makes your code less readable 

 우리가 앞에서 문법의 다양성을 다룬 것은 생각해 볼 가치가 있었다. 일반적인 함수라면, 사람들은 정확히 어떤 것을 기대할지 알 수 있다. 화살표 함수를 쓴다면, 정확히 어떤 것을 기대하는지 알아내는 것이 더 어려울 것이다. 


 ## When you should use them

  화살표 함수는 `this`가 함수 자신이 아니라 컨텍스트에 바인드 될 때 가장 빛난다. 

  익명함수임에도 불구하고, `map`이나 `reduce` 같은 메소드와 함께 사용하는 것을 좋아한다. 왜냐하면, 내 코드를 더 가독성이 높게 만들어주기 때문이다. 나에게는 득이 실보다 더 많다. 



  제 글을 읽어주셔서 감사하고, 만약 좋다면 clap 을 눌러주세요. 다른 글들도 살펴보고 가세요.
