***WIP***

## JSX
- JSX(컴포넌트의 return부분)에 자바스크립트를 넣고 싶다면 `{}`잊지말기


## AJAX 모델(여러 기술을 사용하는 접근법, 웹 개발 기법)
: 빠르게 동작하는 동적인 웹 페이지를 만들기 위한 개발 기법의 하나
- XMLHttpRequest API (XHR) -> Fetch API

## 형식
- XML -> JSON

## [Fetch](https://wooooooak.github.io/javascript/2018/11/25/fetch&json()/)
- 자바스크립트에서 기본적으로 제공하는 fetch 함수
- Body 데이터의 form을 직접 변환해야함 (그래서 axios나 다른 라이브러리 쓰는거임+에러핸들링도 편함)
- Fetch 로는 데이터를 바로 사용할 수 없다.
  - 한줄로 쭉: 스트림일 뿐 데이터가 완전히 다 받아진 상태가 아님
  - 따라서 .then(res=>res.json()) 로 다 읽은 body의 텍스트를 promise 형태로 반환
  - .then((json) => console.log(json)) 서버에서 주는 json 데이터가 출력됨
- Fetch -> .then -> .then 보다 async await가 더 좋다(코드참조)
```
  useEffect(() => {
    fetch(`https://yts.mx/api/v2/list_movies.json?minimum_rating=8.8&sort_by=year`)
      .then((res) => res.json())
      .then((json) => {
        setMovies(json.data.movies)
        setLoading(false)
      })
  }, [])
```
===
```
  const getMovies = async () => {
    const response = await fetch(
      `https://yts.mx/api/v2/list_movies.json?minimum_rating=8.8&sort_by=year`
    );
    const json = await response.json();
    setMovies(json.data.movies);
    setLoading(false);
  }
  useEffect(() => {
    getMovies();
  }, []);
```
- async: "얘 비동기 할건데 어떤 비동기냐면, 이 안에선 await를 사용해서 순서대로 내려갈거야"


## map돌려서 리스트 만들때 key값 주는 것 잊지 말기
- key는 react.js에서만, map안에서 컴포넌트들을 render할때 사용
- map의 두번째인자인 index를 먹이거나
```
<ul>
    {movie.genres.map((genre, index) => <li key={index}>{genre}</li>)}
  </ul>
```
- 고유한 값이면 뭔들 상관 없으
```
<ul>
  {movie.genres.map((genre) => <li key={genre}>{genre}</li>)}
</ul>
```

## create-react-app이 날 힘들게 할때
1.	npm uninstall -g create-react-app
2.	npm add create-react-app
3.	다시 npx create-react-app myapp


## React-router-dom
- npm install react-router-dom
- screen = page = route
- route별로 생각해봐야함 
- url을 쳐다보고 있는 component
- react-router-dom 버전5 -> 버전6 달라진 점: Switch컴포넌트가 사라지고 -> Routes컴포넌트로 대체
- BrowserRouter: 보통의 웹사이트처럼 "/"
- HashRouter: "/#/"가 추가로 붙는다

### Router
### Switch
- React Router에서는 원하면 두개의 route를 한번에 렌더링 할 수 있음
- Switch를 쓰는 이유: 한번에 하나의route만 가져오고 싶기 때문
### Route
- path를 속성으로 갖고 진행

제목 클릭시 이동하게 만드는법
- `<a>`링크 사용해도 되지만 그렇게 되면 전체 새로고침 됨
- 이를 위한 react-router-dom내 `Link`: 브라우저 새로고침 없이도 유저를 다른 페이지로 이동시켜주는 컴포넌트

dynamic url
- dynamic하다는건 url에 변수를 넣을 수 있다는 의미 e.g. /movie -> `<Route path="/movie/:id">`
- `<h2><Link to={`/movie/${id}`}>{title}</Link></h2>`

useParams
- url내에 있는 변수(위의 `:id`와 같은것) 가져오는 법 useParams
- `<Route path="/movie/:id">` {id=34015} or 
- `<Route path="/movie/:id">`{tomato=34015}
```
const { id } = useParams();
console.log(id);
```


## Publishing
- `npm i gh-pages`
- package.json 내의 scripts에 'build' 있는것 확인. build run하게되면 production ready code를 생성하게 됨 : `npm run build` -> build 폴더가 생성됨
- package.json 가장 마지막에 `, "homepage": "https://robinyeon.github.io/Movie-App"`
  - `,`잊지말고
  - `"homepage": "https://사용자명.github.io/연결돼있는레포명"`
- package.json 내의 scripts에 `"deploy": "gh-pages -d build"` 추가
  - gh-pages에 디렉토리(-d) build에 있는걸 deploy하고 싶다는 의미
- build -> deploy의 순서를 항상 지켜야하는데, 귀찮으니까 `"predeploy": "npm run build",`
  - deploy 실행하게 되면(npm run deploy) 자동으로 predeploy가 먼저 실행됨
  - 그럼 자연스럽게 build 먼저 되면서 -> deploy 진행
- 이후 뭔가 수정하고 업데이트 하고 싶다면 `npm run deploy`만 하면 끝






