## create-react-app
- 바닐라 리액트에서 일일이 임포팅 했던 script 등을 미리 준비해줌
- package.json에서 우리가 script 확인 가능

### install
1. terminal에서 node.js 깔린거 확인 `node -v`
2. `npx create-react-app 프로젝트이름`
3. 설치 후 `code 프로젝트이름`하면 VSCode에서 열림
4. VSCode 터미널에서 `npm start` 하면 브라우저 자동 열림(development server열림)
5. create-react-app 폴더 정리

<br/>

## CSS modular
- App.module.css 파일 만들어서 import
- e.g. `import styles from "./Button.module.css"`
- 필요에 따라 골라 꺼내쓸 수 있도록 styles라는 object에 넣는것.
```
import styles from "./Button.module.css"

function Button({ text }) {
    return <button className={styles.btn}>{text}</button>
}
```

<br/>

## useEffect
- 언제 코드가 실행될지 결정하는 방법
1. **state 변할때 전체 component, 즉 전체 code는 실행된다**
2. API call 같은 것 또한 다시 실행됨
3. **가끔 component 내부의 몇몇 코드는 처음 딱 한번만 실행되고 다시는 실행되지 않도록 하고싶을때 useEffect 사용**
- 특정 코드들은 첫 component render때에'만' 실행되게 하고 싶음 e.g. API call이 다른 state 변화 될때마다 call 된다면 무거워 

### useEffect(1, 2)
1: function which is going to run only once
2: which one to watch
```
function App() {
  const [counter, setCounter] = useState(0);
  const onClick = () => setCounter((prev) => prev + 1);
  console.log("I run ALL the time");
  const iRunOnlyOnce = () => {
    console.log("I run ONLY ONCE");
  };
  useEffect(iRunOnlyOnce, []);
  return (
    <div className="App">
      <h1 className={styles.title}>{counter}</h1>
      <button onClick={onClick} text={"Continue"}>CLICK ME</button>
    </div>
  );
}
```

### watching: 특정 무언가가 업데이트 될때만 코드 실행하기
- {keyword}가 바뀔때만 코드를 실행하기
```
 useEffect(() => {
    console.log("Search for", keyword);
  }, [keyword]);
```
- `[]` what react is watching

### useEffect recap code below:
```
console.log("I run ALL the time.");

  useEffect(() => {
    console.log("I run only ONCE.")
  }, []);

  useEffect(() => {
    if (keyword !== "" && keyword.length > 5) {
      console.log("I run only when 'keyword' changes.");
    }
  }, [keyword]);

  useEffect(() => {
    if (counter !== 0) {
      console.log("I run only when 'counter' changes")
    }
  }, [counter]);
```

<br/>

## CleanUp function
- component가 없어질때(destroy) 무언가를 실행하는 것
- useEffect의 callback내에 return 되는 **함수** === destroy 될때 실행될 것 (함수로 안적으면 적용 안되더라)
```
const byeFn = () => {
    console.log("destroyed :(");
  }
  const hiFn = () => {
    console.log("created :)")
    return byeFn;
  }
  useEffect(hiFn, [])
  return (<h1>Hello Laphoo!</h1>);
}
```

### 보통 위와 같이 적지 않고 아래와 같이 useEffect 안에 한번에 넣어서 적음
```
const Hello = () => {
  useEffect(() => {
    console.log("hi :)");
    return () => console.log("bye :(")
  }, [])
  return (<h1>Hello Laphoo!</h1>);
}
```
