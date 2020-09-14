# [ES6] Spread 연산자, Rest 파라미터, Array Like

## Spread 연산자.
- Spread 연산자(...)는 이터러블 오브젝트의 엘리먼트를 하나씩 분리하여 전개한다. 전개한 결과를 변수에 할당하거나 호출하는 함수의 파라미터 값으로 사용할 수 있다.
```javascript
//EX
    [...iterableObject]
    function(...iterableObject) 
``` 
```javascript
let one  = [11, 12];
let two = [21, 22];
let spreadObj = [51, ...one, 52, ...two];
console.log(spreadObj); //[51, 11, 12, 52, 21, 22]
console.log(spreadObj.length); //6

let spreadTxt = [..."string"];
console.log(spreadTxt); //["s", "t", "r", "i", "n", "g"]
```
### 함수 파라미터. (Spread  파라미터)
- 호출하는 함수의 파라미터 값을  spread 연산자로 작성하면, 함수를 호출하기 전에 파라미터값을 분리하여 전개한다.
```javascript
const values = [10, 20, 30];
function func(one, tow, three) {
    console.log(one + two + three);
}
func(...values);  //60
```

## rest 파라미터
- 호출받는 함수에 'function(...param)'형태로 spread 연산자를 이용하여 파라미터를 작성한 형태를 rest 파라미터라고 한다.
```javascript
let func = (one) => {
    console.log(one);
}
func(...[1,2,3]); // 1
```
'func(...[1,2,3])'이 'func(1,2,3)'과 같은 형태로 전개되므로 콘솔에 1만 출력된다. 호출 받는 쪽에서도 spread연산자를 사용하여 파라미터를 작성하면 2와 3을 받을 수 있다.
```javascript
let func = (...param) => {
    console.log(param, Array.isArray(param));
}
let func2 = (one, ...param) => {
    console.log(one, param);
}
func(...[1,2,3]); // [1, 2, 3] true
func2(...[1,2,3]); // 1, [2,3]
```

## Array-like
- Array는 아니지만 Array처럼 사용할 수 있는 Object를 Array-like라고 한다. ES6 스펙에 공식 용어라고 한다. 
  key-value 형태의 Object 특징을 유지하면서 배열의 특징을 가져온것이 Array-like이다.  
```javascript
    let values = {0: "zero", 1: "one", 2: "two", length: 3};
    for(let key in values) {
        console.log(key, ':', values[key]);
    }
    for(let i = 0; i<values.length; i++) {
        console.log(values[i]);
    }
    // 0 : zero 
    // 1 : one 
    // 2 : two 
    // length : 3
    // zero 
    // one 
    // two    
```
for-in 문과 다르게 for()문에서는 Array와 동일하게 사용이 가능하다. 혼동을 줄 수 있기 때문에 실제 사용은 안해야겟다.
Array-like의 프로퍼티 키 값은 0부터 1씩 증가하면서 순차적으로 작성되어야만 한다. 또한 length를 키로 하여 전체 프로퍼티 개수를 명시 해주어야만 한다.

** ECMAScript6 정리 **
