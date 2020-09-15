# 우아한테크러닝 3기 : React&TypeScript 2주차.

### 운좋게 참여하게 된 우아한테크러닝3기 강의 마구마구 기억나는데로 정리.
### 3일차 교육내용.
* React 만들기.     
리액트에서 가상돔이 만들어지고 실제 DOM으로 렌더링되는 과정을 간단하게 구현.

**가상돔의 구조 예시**
```json
const vdom = {
  type: 'ul',
  props: {},
  children: [
    { type: 'li', props: { className: "item" }, children: "Hello" },
    { type: 'li', props: { className: "item" }, children: "World" },
    { type: 'li', props: { className: "item" }, children: "React" },
    // ...
  ],
}
```
**index.js**
```javascript
/* @jsx createElement */
import { createElement, render } from "./tiny-react";

function Hello(props) {
  return <li className="item">{props.label}</li>;
}

function App() {
  return (
    <div>
      <h1>hello world</h1>
      <ul className="board" onClick={() => null}>
        <Hello label="Hello" />
        <Hello label="World" />
        <Hello label="React" />
      </ul>
    </div>
  );
}

console.log(<App />);
render(<App />, document.getElementById("root"));

```

'/* @jsx createElement */'부분은 '/*@jsx ...*/'구문으로 babel 컴파일시 실행되는 함수를 명시해줄수 있다.
여기서는 React.default.createElement가 아닌 간단히 구현한 createElement를 명시함.

**tiny-react.js**
```javascript
function renderElement(node) {
  if (typeof node === "string") {
    //마지막 노드인 경우.
    return document.createTextNode(node); 
  }

  if (node === undefined) return;

  const $el = document.createElement(node.type);

  //vdom은 tree 구조이기 때문에 renderElement함수를 재귀 호출하여 순환하며
  // dom 엘리먼트를 생성한다.
  node.children.map(renderElement).forEach((node) => {
    $el.appendChild(node);
  });

  return $el;
}


export function render(vdom, container) {
  // 최종적으로 생성된 엘리먼트가 container 파라미터로 전달받은 실제 dom에 렌더링됨.
  container.appendChild(renderElement(vdom));
}

/*
babel에 의해 컴파일 될때 호출되며
type이 함수일때는 apply()를 이용해 해당 함수를 호출하는데 apply() 를 사용하는 이유는
children이 리스트이기 때문에.
아닌경우는 객체 return.
*/
export function createElement(type, props, ...children) {
  if (typeof type === "function") {
    return type.apply(null, [props, ...children]);
  }
  return { type, props, children };
}

```
### 4일차 교육은 참여를 못함. 하하


