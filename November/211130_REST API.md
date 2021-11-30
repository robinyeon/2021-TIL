## form 데이터를 서버로 전송
### 1. form 태그 세팅
e.g. `<form action="/add" method="POST">`
- 폼 전송 버튼을 누를 시 `/add`라는 경로로 `POST`요청을 하는 폼
- `method` : GET과 POST 중 어떤 요청을 할 건지 정해주는 부분
- `action` : 어떤 경로로 요청할건지 정해주는 부분

### 2. input 태그 세팅
e.g. `<input type="text" class="form-control" name="title">`
- `name` 속성을 이용해 각각의 input에 이름 부여
- 폼 전송 시 input에 이름이 있으면 서버에서 어떤 데이터인지 확인 가능

```
<form action="/add" method="POST">
  <div class="form-group">
    <label>오늘의 할일</label>
    <input type="text" class="form-control" name="title">
  </div>
  <div class="form-group">
    <label>날짜</label>
    <input type="text" class="form-control" name="date">
  </div>
  <button type="submit" class="btn btn-outline-secondary">Submit</button>
</form> 
```

### 3. POST 요청 처리하는 코드짜기
```
app.post('/add', function(요청, 응답){
  console.log(요청.body);
  응답.send('전송완료')
});
```
- 누군가가 `/add`경로로 post 요청을 할때 콘솔창에서 `요청.body` 출력 가능
- `요청.body`는 object 형태 e.g. `{title: "send this to title", date: "send this to date"}`

### *body-parser
- 데이터 쉽게 처리 도와주는 라이브러리: 클라이언트 POST request data의 body로부터 파라미터를 편리하게 추출
- 2021년 이후 body-parser 라이브러리가 express에 기본 포함되어서 따로 npm으로 설치할 필요없이    
`app.use(express.urlencoded({extended: true}))`코드만 추가해 주면 됨

<br/>

## REST API
### API
- Application Programming Interface, 서로 다른 프로그램 간 소통할 수 있게 도와주는 통신 규약
- 웹에서 사용시, '서버와 고객간의 통신규약' === '서버에게 요청해서 데이터 가져오는 방법'      
e.g. "누군가 `/`로 접속시 index.html을 보내주세요" 즉 index.html을 보고 싶으면 /으로 접속하라는 API 정의

### REST API
- Representational State Transfer, API 디자인 방법론(이지만 요즘은 거의 정론)
- 웹 API 짤 때 REST 원칙을 지켜서 짜면 좋다고 권고 (특히 1번 중요)

#### 1. Uniform Interface: 인터페이스는 일관성이 있어야한다
- 하나의 URL로는 하나의 데이터를 가져오기: 하나를 가져오기 위한 두개의 URL을 만들지 말자
- 간결하고 예측가능하게 짜기: URL 하나를 알면 둘을 알게
- URL 이름짓기 관습 잘 따르기
  ```
  instagram.com/explore/tags/kpop
  instagram.com/explore/tags/food
  facebook.com/natgeo/photos
  facebook.com/bbc/photos
  ```
  - 단어들을 동사보다는 **명사** 위주로 구성
  - 응용해서 다른 정보들을 쉽게 가져올 수 있을 정도로 **일관성** 있음 
  - 대충 봐도 어떤 정보가 들어올지 **예측이 가능**함 

  그 외에도
  - 띄어쓰기는 언더바`_`대신 대시`-`기호 사용
  - 파일 확장자 쓰지 말기 (e.g. `.html`)
  - 하위 문서들을 뜻할 땐 `/` 기호 사용함 (하위폴더같은 느낌)

#### 2. Client-server 역할 구분
- 브라우저(고객)은 요청, 서버는 응답
- 고객에게 서버역할을 맡기거나 DB에 있는 자료를 직접 꺼내라는 식으로 코드 짜지 않기

#### 3. Stateless: 요청들은 각각 독립적으로 처리되어야 한다
- `요청1`을 성공해야 `요청2`를 보내주는 것처럼 요청간의 의존성이 존재하는 코드 짜지 않기
- 요청 하나 만으로 자료를 가져오기 충분하도록 요청에 필요한 모든 정보들을 실어 보내기

#### 4. Cacheable
- 요청을 통해 보내는 자료들은 캐싱이 가능해야 함
- 캐싱가능하다고 표시하거나 캐싱 기간 설정해주기     
#### *캐싱*
> 네이버를 방문하면 크롬 브라우저는 자동으로 자주 사용하는 이미지 파일, CSS 파일 등을 하드에 저장해놓습니다.    
> 별로 바뀔일 없는 네이버 로고나 아이콘 같은거요.   
> 하드에 저장해놓고 네이버 방문할 때 네이버서버에 네이버 로고주세요~라고 요청하지 않고 하드에서 불러옵니다.     
> 이 행위를 캐싱이라고 합니다.      

#### 5. Layered System
- 요청 처리하는 곳, DB에 저장하는곳 등 여러가지 단계를 거쳐 요청을 처리해도 됨
- 즉, 여러개의 레이어를 거쳐서 요청을 처리하게 만들어도 됨

#### 6. Code on Demand
- 서버는 고객에게 실제 실행가능한 코드를 전송해줄수도 있음

 



 

 

