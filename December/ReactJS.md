## 왜 ReactJS를 사용하는가?
1. There's many big websites behind ReactJS.
  - 단순히 '큰 회사들이 사용하기 때문'이 아닌, 그들이 리액트를 택한 후 보이는 행보들이(e.g. 적극투자) 더욱 리액트의 입지를 견고히 하고 있음.
2. 굉장히 큰 커뮤니티
  - ReactJS is mostly JavaScript: 자바스크립트를 사용하다보니 자바스크립트의 커뮤니티를 그대로 끌고 왔다고 봐도 과언이 아니다.
    - e.g. 라이브러리, 프레임워크, 가이드라인, 튜터, 채용 등
  - 즉, 리액트를 기반으로 한 생태계가 존재
  - Learn once, write anywhere: 여전히 그 한계치를 넓혀가는 중

### VanillaJS vs ReactJS
- 리액트는 UI Interactivity를 가능하게 함
- **즉 JS로 element 생성(업데이트)하고, React가 HTML로 변역**

<br/>

## ReactJS Rules
1. element 생성을 위해 HTML body에 직접 작성하지 않는다
  - 자바스크립트와 리액트를 이용하여 element생성
  - React가 interactivity를 만드는 엔진과 같다면, React.dom은 모든 리액트 element를 HTML body에 둘 수 있도록 해준다.
```
<script>
  const root = document.getElementById("root");
  const span = React.createElement("span");
  ReactDOM.render(span, root);        //span을 root안에 render하라는 뜻
</script>
```

<br/> 

## `.createElement()`
- 첫번째 인자: 만들 태그
- 두번째 인자: properties(props)
- 세번째 인자: 넣을 내용
- e.g. `const span = React.createElement("span", { id: "sexy-span", style: {color:"red"} }, "hello!");`

<br/>

## create-react-app 없는 바닐라 리액트 코드 예시:
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

<br/>

## Replacing `.addEventLister()`
```
const btn = React.createElement(
      "button",
      {
        onCick: () => console.log("clicked!"),
      },
      "click me!"
    );
```
- 두번째 parameter로 들어간 props 안에 `id`, `style`등은 html tag안에 넣어주고,
- Event listener는 따로 안 넣어줘도 대신 실행

<br/>

## Replacing `.createElement()`: JSX
- 그 전에, 브라우저가 JSX 이해할 수 있게끔 code transformer `Babel standalone` 설치 필요
- **JSX에서 자바스크립트 쓸 땐 `{}` 필수**
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

<br/>

## Component
- 나의 컴포넌트는 **대문자**로 시작해야한다
  - e.g. 만약 소문자로 시작하면 React와 JSX는 HTML button태그라고 착각

<br/>

## Rendering
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
- 리액트의 좋은점은 UI에서 '바뀐 부분만' 업데이트 해준다는것.
  - 다시 render할때마다 Container가 통째로 바뀌는거 같지만 그렇지 않다.
- 위처럼 reRender를 굳이 하지 않아도 되는 방법: below

### How to automatically trigger re-rendering
- `useState`'s modifier(e.g. `setCounter`) would change the value, **AND** re-render automatically
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
- modifier function : whole component will be recreated again(rerendered), but only changing the changed value on HTML.
  - when you change the state, that will trigger re-render.
  - **state가 바뀌면 리액트가 컴포넌트를 re-rendering 해준다.**

### state 바꾸는 법
- 위처럼 setState 사용하되, if need to calculate the state based on current value: `setCounter(current => current+1)` this way is much more safe.

<br/>

## props
- parents component => child component

### Btn(props)
```
   const Btn = (props) => {
      console.log(props);
      return (
        <button
          style={{
            backgroundColor: "tomato",
            color: "white",
            padding: "10px 20px ",
            borderRadius: "10px",
            border: "none",
          }}
        >
          {props.banana}
        </button>
      );
    };

    const App = () => {
      return (
        <div>
          <Btn banana="Save Changes" />
        </div>
      );
    };

```

### Or Btn({banana})\_shortcut
- props가 object고, 그 안에 banana가 있다는 사실을 아니까. 
```
   const Btn = (props) => {
      console.log({banana});
      return (
        <button
          style={{
            backgroundColor: "tomato",
            color: "white",
            padding: "10px 20px ",
            borderRadius: "10px",
            border: "none",
          }}
        >
          {banana}
        </button>
      );
    };

    const App = () => {
      return (
        <div>
          <Btn banana="Save Changes" />
          <Btn banana="Continue" />
        </div>
      );
    };

```

<br/>

## `React.memo()`
```
const Btn = ({ text, changeValue }) => { 
      return (
        <button
          onClick={changeValue}
          style={{
            backgroundColor: "tomato",
            color: "white",
            padding: "10px 20px ",
            borderRadius: "10px",
            border: "none",
          }}
        >
          {text}
        </button>
      );
    };
const App = () => {
  const [value, setValue] = React.useState("Save Changes");
  const changeValue = () => setValue("Revert Changes");
  return (
    <div>
      <Btn text={value} changeValue={changeValue} />
      <Btn text="Continue" />
    </div>
  );
};
```
- "props가 변하지 않는 컴포넌트는 re-render되지 않았으면 좋겠다" e.g. `<Btn text="Continue" />`
- e.g. `const MemorizedBtn = React.memo(Btn);`
- 기존의 Btn 대신 MemorizedBtn로 변경 -> props가 변경되는 버튼만 리렌더링 됨.
- 후에 앱 구동 속도에 영향을 줌
- 내가 렌더링을 컨트롤 할 수 있다는 것

<br/>

## prop types
- prop의 type이 어떤건지(e.g. string, number) 규정지음으로써 실수 최소화
- 임포트 후 아래와 같이 사용 가능
```
Btn.propTypes = {
      text: PropTypes.string.isRequired,
      fontSize: PropTypes.number,
    };
```
