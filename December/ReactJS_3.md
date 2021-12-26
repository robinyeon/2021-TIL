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
