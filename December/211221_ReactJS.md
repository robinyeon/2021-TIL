***WIP***

왜 React JS?
1. (many big websites behind React JS) 단순히 큰 회사들이 사용한다고 해서가 아닌, 그들이 굳이 다른 라이브러리, 프레임워크를 쓸 이유가 없는거지. 이미 안정적인 리액트를 위해 다양한 투자중.
2. 굉장히 큰 커뮤니티: ReactJS is mostly JS 사용하다보니 JS 커뮤니티를 그대로 끌고 왔다고 해도 과언이 아님 e.g. 라이브러리, 프레임워크, 가이드, 튜터, 채용문도 그래서 넓음
  - 즉, 리액트를 기반으로 한 생태계(ecosystem)이 존재한다는 의미
  - learn once, write anywhere. still expading their limitation.
 
why is it created for? 해결하려는 문제를 알지도 못하고 암기만 했으니 어려웠던거
compare Vanilla JS vs React JS 
**make UI interactive**
created shorcuts: buch of good ideas that every interatctivity developers need.

rule
1. element 생성을 위해 HTML(body)에 직접 작성하지 않는다: JS와 React JS를 이용하여 element 생성
  - react가 interactivity를 만들어준다면(엔진과 같은것)
  - react.dom은 library(혹은 package)인데, 모든 React element들을 HTML body에 둘 수 있도록 해줌.
  - `render` means 'show it to users.'
  ```
  <script>
    const root = document.getElementById("root");
    const span = React.createElement("span");
    ReactDOM.render(span, root); //span을 root안에 render 해달라
  </script>
  ```
**Learning hard way(which i never gonna use again) first so that i can reach the origin of reactJS**
`.createElement()`
first arguement에는 만들 태그
second argument에는 properties(props)
third argument에는 넣을 내용 
e.g. `const span = React.createElement("span", { id: "sexy-span", style: {color:"red"} }, "hello!");`

```
<!DOCTYPE html>
<html>
  <body>
    <div id="root"></div>
  </body>

  <!-- importing react and react-dom -->
  <script
    src="https://unpkg.com/react@17.0.2/umd/react.production.min.js"
    crossorigin
  ></script>
  <script
    src="https://unpkg.com/react-dom@17.0.2/umd/react-dom.production.min.js"
    crossorigin
  ></script>

  <!-- Hard way(for looking at the origin of ReactJS w/o any makeup) of creating ReactJS element -->
  <script>
    const root = document.getElementById("root");
    const span = React.createElement(
      "span",
      { id: "sexy-span", style: { color: "red" } },
      "hello!"
    );
    ReactDOM.render(span, root);
  </script>
</html>
```

**이것이 리액트의 파워**
**js로 element 생성(업데이트)하고,react가 html로 변역함**

replacing addEventLister:
```
const btn = React.createElement(
      "button",
      {
        onCick: () => console.log("clicked!"),
      },
      "click me!"
    );
```

리액트는 똑똑해
두번째 parameter로 들어간 props 안에,
id, style 등은 는 html tag안에 넣어주고(console에서 확인 가능), event listener는 따로 안넣어줘 대신 실행시켜주긴 하는거지

how to replace `.createElement()`: JSX
- but first, 브라우저가 JSX 이해할 수 있게끔 무언갈 설치해야함. code transformer `Babel standalone`

```
const Button = (
      <button
        style={{ backgroundColor: "tomato" }}
        onClick={() => {
          console.log("clicked!");
        }}
      >
        CLICK ME!
      </button>
    );
```
===
```
const btn = React.createElement(
  "button",
  {
    style: { backgroundColor: "tomato" },
    onClick: () => console.log("clicked!"),
  },
  "click me!"
);
```


나의 컴포넌트는 **대문자**로 시작해야한다: 만약 소문자면 React와 JSX는 이게 HTML button태그라고 생각할거야

2.6까지의 코드
```
<!DOCTYPE html>
<html>
  <body>
    <div id="root"></div>
  </body>

  <!-- importing react and react-dom -->
  <script
    src="https://unpkg.com/react@17.0.2/umd/react.production.min.js"
    crossorigin
  ></script>
  <script
    src="https://unpkg.com/react-dom@17.0.2/umd/react-dom.production.min.js"
    crossorigin
  ></script>
  <!-- importing Babel standalone -->
  <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
  <script type="text/babel">
    const root = document.getElementById("root");

    // 첫번째. Title과 Button을 함수로 만들어주기
    const Title = () => (
      <h3 id="title" onMouseEnter={() => console.log("mouse entered!")}>
        HELLO I'M A TITLE
      </h3>
    );

    const Button = () => (
      <button
        style={{ backgroundColor: "tomato" }}
        onClick={() => {
          console.log("clicked!");
        }}
      >
        CLICK ME!
      </button>
    );

    // 두번째. 일반 태그(e.g. <img/>) 담듯이 적어준다.
    const Container = () => (
      <div>
        <Title />
        <Button />
      </div>
    );
    ReactDOM.render(<Container />, root);
  </script>
</html>

```

<br/>


```
  <script type="text/babel">
    const root = document.getElementById("root");
    let counter = 0;
    function countUp() {
      counter += 1;
      render();
    }
    function render() {
      ReactDOM.render(<Container />, root);
    }
    const Container = () => (
      <div>
        <h3>Total clicks: {counter}</h3>
        <button onClick={countUp}>CLICK ME!</button>
      </div>
    );
    render();
  </script>

```
- Container 다시 render 할때마다 Container 통째로 바뀌는거 같지만, 리액트의 좋은점은 UI에서 '바뀐 부분만' 업데이트 해준다는것!
- 위처럼 reRender를 굳이 하지 않아도 되는 방법이 있음 -> below

how to: automatically triggering rerendering
- useState's modifier(e.g. setCounter) would change the value, AND rerender automatically
```
<script type="text/babel">
    const root = document.getElementById("root");
    const App = () => {
      const [counter, setCounter] = React.useState(0);
      const onClick = () => {
        setCounter(counter + 1);
      };
      return (
        <div>
          <h3>Total clicks: {counter}</h3>
          <button onClick={onClick}>CLICK ME!</button>
        </div>
      );
    };
    ReactDOM.render(<App />, root);
  </script>
```
- modifier function : whole component will be recreated again(rerendered), but only changing the changed value(on HTML).
  - when you change the state, that will trigger rerender.
  - **state가 바뀌면 React가 컴포넌트를 rerendering해준다.** 

#3.4 state 바꾸는 법
1. 위처럼 setState 사용
2. if need to calculate the state based on current value,
`setCounter(current => current+1)` this way is much more safe.

```
<input
  value={minutes} // input 값을 외부에서도 수정해주기 위해서 Input의 value를 연결
  id="minutes"
  placeholder="Minutes"
  type="number"
  onChange={onChange}
/>         
```
























