***WIP***

create-react-app은 importing script 같은거 다 준비해준거.
- package.json은 우리가 importing한 script 찾아낼 수 있음

1. terminal에서 node.js 깔린거 확인 `node -v`
2. `npx create-react-app 프로젝트이름`
3. 설치 후 `code 프로젝트이름`하면 VSCode에서 열림
4. VSCode 터미널에서 `npm start` 하면 브라우저 자동 열림(development server열림)
5. create-react-app 폴더 정리

css modular
App.module.css 파일 만들어서 import `import styles from "./Button.module.css"`
- styles라는 object에 넣는것. 필요에 따라 골라 꺼내쓸 수 있도록.
```
import styles from "./Button.module.css"

function Button({ text }) {
    return <button className={styles.btn}>{text}</button>
}
```

## 언제 코드가 실행될지 결정하는 방법 useEffect (React의 관점에선 일종의 방어막 같은 것) 
특정 코드들은 첫 component render때에만 실행되게 하고 싶어 e.g. API call이 다른 state 변화 될때마다 call 된다면 무거워
1. **state 변할때 전체 component, 전체 code는 다시 실행됨**
2. API call 같은것 또한 다시 실행될 것임.
3. **가끔은 component 내부의 몇몇 코드는 처음 딱 한번만 실행되고 다시는 실행되지 않도록 하고싶을때 -> useEffect**

useEffect(1, 2)
1: only going to run one time
2: magical but later
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

특정 무언가가 업데이트 될때만 코드를 실행하기
```
 useEffect(() => {
    console.log("Search for", keyword);
  }, [keyword]);
```
{keyword}가 바뀔때만 코드를 실행하기
[] what react is watching


useEffect recap code below:
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


CleanUp function
component가 없어질때(destroy) 무언가를 실행하는 것.
useEffect의 callback내에 return 되는 **함수** === destroy 될때 실행될 것
함수로 안적으면 적용 안되더라
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
보통 위와 같이 적지 않고 아래와 같이 useEffect 안에 한번에 넣어서 적음
```
const Hello = () => {
  useEffect(() => {
    console.log("hi :)");
    return () => console.log("bye :(")
  }, [])
  return (<h1>Hello Laphoo!</h1>);
}
```
