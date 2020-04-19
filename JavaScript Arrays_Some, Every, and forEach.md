JavaScript Arrays: Some(), Every(), and forEach()
https://levelup.gitconnected.com/javascript-array-some-vs-every-vs-foreach-knowledge-scoops-81dfe43369c6



# Some() 메소드

`some()` 메소드는 배열의 요소들을 순회하면서, 배열의 값이 조건을 만족하는지를 체크합니다. `some()` 메소드는 다음과 같은 형태의 불리언 표현식을 가집니다. 
``` javascript
(element) => boolean
```

`element`는 배열에서 값을 체크하는 현재 요소를 말합니다. 
`boolean`은 함수가 불리언 값을 리턴하는 것을 나타냅니다.



다음의 정수 배열을 생각해봅시다. 

``` javascript
let arr = [1,2,3,4,5,6,7,8];
```

`some()` 메소드를 이용하여 최소한 한 개의 요소가 배열에서 조건을 만족하는지를 확인할 수 있습니다. 

``` javascript
arr.some((value)=> {return (value %2 == 0 ); }); //true
```

배열은 2로 나누어떨어지는 요소(2,4,6,8)를 포함하고 있기 때문에 `some()` 메소드는 `true`를 리턴합니다. 



`some()` 메소드를 이용해서 배열이 음수를 포함하고 있는지를 살펴봅시다. 

``` javascript
arr.some((value)=> {return (value < 0 ); }); //false
```

결과로 `false`를 리턴합니다. 배열이 음수인 숫자를 가지고 있지 않기 때문입니다. 



`some()` 메소드는 불리언 표현식을 만족하는 요소를 찾는 즉시 순회를 멈춥니다. 

``` javascript
arr.some((value) => { 
    console.log(value); 
    return (value % 2 == 0); 
}); // 1 2
```
배열의 요소가 2인 경우에 값을 만족해서 `true`를 리턴하고 수행이 종료됩니다.




# Every() 메소드

`some()` 메소드와는 반대로 `every()` 메소드는 배열 안의 요소들이 전부 표현식을 만족하는지 여부를 체크합니다. 만약 하나라도 만족하지 못한다면 `false`를 리턴하고, 그렇지 않다면 `true`를 리턴합니다. 

``` javascript
let arr = [1, 2, 3, 4, 5, 6, 7, 8];
arr.every((value)=> { 
    return (value > 0); 
}); //true
```

배열 `arr`의 모든 값들이 양수기 때문에, 모든 값에 대해서 불리언 표현식을 만족합니다. 그래서 `true`를 결과로 받습니다.



만약 하나라도 불리언 표현식을 만족하지 않는다면 `false`를 받습니다. 
``` javascript
arr.every((value)=> { return (value == 5); }); //false
```

`every()` 메소드는 불리언 표현식을 만족하지 못하는 순간에 순회를 멈춥니다. 

``` javascript
arr.every((value) => { 
    console.log(value); 
    return (value != 4); 
}); // 1 2 3 4
```



# forEach() 메소드

`forEach()` 메소드는 이름에서 알 수 있듯이 배열의 모든 요소를 반복하고 원하는 작업을 수행하는데 사용됩니다.

```javascript
let arr = [1, 2, 3, 4, 5, 6, 7, 8];
arr.forEach((value) => { 
    console.log(value == 5); 
});
```
배열이 가진 8개의 모든 요소에 대해서 각각 `value==5` 표현식을 평가한 결과를 리턴합니다. 

```javascript
false false false false true false false false
```