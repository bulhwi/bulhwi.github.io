# 우아한테크러닝 3기 : React&TypeScript 3주차.

### 운좋게 참여하게 된 우아한테크러닝3기 강의 마구마구 기억나는데로 정리.
## 5일차 교육내용.
### 커링(Currying)
- 커링은 N개의 인자를 받는 함수를 단일 인자를 받는 N개의 함수열로 만드는 것이다. 
  함수의 재사용성 측면에서 유용하게 사용이 된다.
```javascript
function funcA(a,b,c){
  return a + b + c;
}

function funcB(a) {
  return function func2(b) {
      return function func3(c) {
          return a + b + c;
      }       
  }
}

console.log(funcA(1,2,3)); // 6
console.log(funcB(1)(2)(3)); // 6
```
위와 같이 funcA와 funcB는 동일하게 동작한다. **funcB** 함수는 함수와 인자의 클로저를 사용하여 커링 함수를 만든다. 
ES6 화살표 함수로도 작성이 가능하다.
```javascript
    const funcC = (a) => (b) => (c) => {return a+b+c};
    console.log(funcC(1)(2)(3)); //6
```
커링함수의 큰 장점인 재사용성 측면에서 예를 들면,

```javascript
let addr = (a) => (b) => (c) => {
  console.log(`${a} ${b} ${c}`);
}

let addr2 = addr('경기도');
addr2('안양시')('동안구');
let addr3 = addr2('안양시');
addr3('만안구');

addr3 = addr2('수원시');
addr3('권선구');
addr3('팔달구'); 

// 출력
// 경기도 안양시 동안구 
// 경기도 안양시 만안구 
// 경기도 수원시 권선구 
// 경기도 수원시 팔달구 
```
위와 같은 형식으로 함수 인자의 연산 단계에서 호출자 또는 함수 사용자의 개입이 가능하다.

