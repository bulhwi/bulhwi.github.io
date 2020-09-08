# 우아한테크러닝 3기 : React&TypeScript 1주차.

## 운좋게 참여하게 된 우아한테크러닝3기 강의 내용 무차별 정리.
### 1일차 교육내용/목표 설명.
* React&TypeScript 기반 웹 앱개발 교육
* 웹앱을 개발하는데 중요한 컴포넌트와 상태관리에 대한 이해
* 아키텍처 설계
##### TypeScript
###### 데이터 타입명시 
 데이터타입에 느슨한 'JavaScript'보다 엄격하게 타입을 선언하여 에러를 방지할 수 있다.
 ```typescript
let num: Number;
num = 'string'; //error
```
```TypeScript
// Type Alias로 타입을 공통으로 관리할 수도 있다.
type Num: Number;
type Str: String;

let height: Num = 180;
let weight: Num = 75;
let name: Str = 'name';
```
**참고** : [TypeScript Basic Types](https://www.typescriptlang.org/docs/handbook/basic-types.html)

###### Type Alias와 Interface
```Typescript
type Foo = {
    num: Number;
    text: String;
}

interface Bar {
    num: Number;
    text: String;
}

const foo: Foo = {
    num: 100,
    text: 'foo string'
}

const bar: Boo = {
    num: 100,
    text: 'bar string'
}
``` 
TypeScript를 처음 접하다보니 헷갈리는 부분이다. type alias와 interface의 동작은 같은데 어떠한 용도로 어떻게 구분하여 사용하는지 모르겠음.
interface는 extends, implements등 확장가능한 구문들이 사용될 수있는 반면에 type alias는 아닌것 같다.
추후에 강의를 진행하며 스터디를 해야함. 

###### Babel을 사용하면 컴파일 과정에서 코드가 어떻게 변할까?
```javascript
import React from 'react';

function App () {
  return (
    <h1 id="header">Hello</h1>
    )
}
```
해당 코드를 Babel을 사용하여 컴파일하면. 
```javascript
"use strict";

var _react = _interopRequireDefault(require("react"));

function _interopRequireDefault(obj) { return obj && obj.__esModule ? obj : { default: obj }; }

function App() {
  return /*#__PURE__*/_react.default.createElement("h1", {
    id: "header"
  }, "Hello");
}
```
위와 같은 형태로 코드가 바뀌고, 'createElement()'에서 DOM 엘리먼트 생성을 위한 동작을 한다. 
```javascript
React.createElement(
  type,
  [props],
  [...children]
)
```
인자로 주어지는 타입에 타라 태그가 생성된다. JSX를 사용할 경우 React.createElement()를 직접 호줄하는 일은 거의 없다고 한다.
##### React
###### CRA를 이용한 React&TypeScript 프로젝트 구성.
```bash
$ npm create react-app demo-project --template typescript //npm
$ yarn create react-app demo-project --template typescript //yarn
```
CRA(create react app)은 vue-cli를 통해 프로젝트를 구성하는 것 처럼 내부에 복잡한 webpack 관련 설정들이 디폴트 형식으로 구성 되어있다.
그렇기 때문에 초기 프로젝트 세팅을 간편하게 할 수 있는 반면에 CRA가 지원하지 않는 구성을 추가하거나 변경하는것이 굉장히 까다롭다.
reject라는 키워드를 통해 환경구성을 커스텀할 수 있기는 하지만 굉장히 복잡하여 추천하지 않는다고 했다.
프로덕션용 앱이라면 CRA는 사용하지 않는 것이 좋음.  

##### 상태관리 : Redux, MobX
vuex와 같은 포지션의 생태관리 모듈인 것 같다. 강의를 진행하면서 자세히 알게 될 것 같다.
상태를 관리하고 업데이트하기 위한 모듈임.

**강의에서 언급된 참고 URL**: 
* [타입스크립트 플레이그라운드](https://www.typescriptlang.org/play) 
* [code sandbox](https://codesandbox.io/index2) 
* [ReactJS](https://reactjs.org/)
* [Redux](https://redux.js.org/)
* [MobX](https://mobx.js.org/README.html)
* [redux-sage](https://redux-saga.js.org/)
* [blueprint - 타입스크립트 기반으로 개발된 UI 프레임웍](https://blueprintjs.com/)
* [testing-library](https://testing-library.com/)
 
### 2일차 교육내용
* javaScript 스펙 정리.
* Redux 간단 구현.

#### JavaScript 함수 선언 유형.
```javascript
function foo() {} //일반적인 선언

const bar = function(){} // 함수도 객체로 취급이 되기때문에 변수에 할당이 가능하다

// 즉시 호출되는 펑션에 선언방식.
// 브라우저에 의해 js가 로딩되면 최초 1번 호출되는 콜백 펑션임.
(function(){
    console.log('IIFE')
})();
 
// ES6부터 지원하는 화살표 함수.
const bar = (x) => x * 2;
const bar = (x) => {return 0;};
```

#### JavaScript 비동기적 프로그래밍(Promise, Async, await)
콜백지옥의 단점(중첩된 중괄호, 예외처리의 어려움등등등)을 해결하려는 시도속에서 만들어진 Promise는 비교적으로 안전하고 관리하기 쉬운 코드 구조를 가지지만 번거롭다는 
평가도 있었다고 한다. 
```javascript
const p = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve('응답');
    }, 1000);
});

p.then((res) => {
    console.log(res) //응답
}).catch((err) => {
    console.log(err);
});

async function promiseFunc() {
    let result = await p.then((res) => {
        return res;
    }).catch((err) => {
        return err;
    });

    console.log(result);
}
promiseFunc();
``` 

#### 클로저(Closure)
```javascript
function foo(x) {
    return function bar() {
        return x;
    };
}
const f = foo(10); // function bar를 리턴. 
console.log(f()); // 10
```
'console.log(foo(10))'시점에서 x의 사이클은 끝나지만 foo의 내부 함수인 bar함수에서는 x의 참조를 유지한다. 
이러한 상황에서 갇혀있다. 닫혀있다는 표현으로 클로저라고 부름. 

**내부함수에서 외부의 스코프를 기억하고 있는 상태 또는 외부에서 선언된 변수,데이터등의 참조를 끊지 않고 가지고 있는 상태.**

등등등 JavaScript 기본 정리.

#### redux 간단 구현.

```javascript
//index.js
import { createStore, actionCreator } from "./tiny-redux";

function reducer(state = {}, { type, payload }) {
  switch (type) {
    case "init":
      return {
        ...state,
        count: payload.count
      };
    case "inc":
      return {
        ...state,
        count: state.count + 1
      };
    case "reset":
      return {
        ...state,
        count: 0
      };
    default:
      return { ...state };
  }
}

const store = createStore(reducer);

store.subscribe(() => {
  console.log(store.getState());
});

store.dispatch({
  type: "init",
  payload: {
    count: 1
  }
});

store.dispatch({
  type: "inc"
});

store.dispatch(actionCreator("reset"));

const Increment = () => store.dispatch(actionCreator("inc"));

Increment();
Increment();
Increment();
```
```javascript
//redux.js
export function createStore(reducer) {
  let state;
  const listeners = [];
  const publish = () => {
    listeners.forEach(({ subscriber, context }) => {
      subscriber.call(context);
    });
  };
  const dispatch = (action) => {
    state = reducer(state, action);
    publish();
  };
  const subscribe = (subscriber, context = null) => {
    listeners.push({
      subscriber,
      context
    });
  };
  const getState = () => ({ ...state });

  return {
    dispatch,
    getState,
    subscribe
  };
}

export const actionCreator = (type, payload = {}) => ({
  type,
  payload: { ...payload }
});
```

