## localStorage
- `localStorage.setItem("key", "value")` localStorage에 저장하기
- `localStorage.getItem("key")` key에 해당하는 value값 가져오기
- `localStorage.removeItem("key")` key에 해당하는 value값 삭제


### `JSON.stringify()`
- JavaScript 값이나 객체를 JSON 문자열로 변환
- 즉 object든 array든 string의 형태로 저장할 수 있도록 도와줌
```
JSON.stringfy([1,2,3,4])    // "[1,2,3,4]"
```

### `JSON.parse()`
- JSON 문자열의 구문을 분석하고, 그 결과에서 JavaScript 값이나 객체를 생성
```
const json = '{"result":true, "count":42}';
const obj = JSON.parse(json);

console.log(obj.count);
// expected output: 42

console.log(obj.result);
// expected output: true
```

<br/>

## `.innerText`
- e.g. `greeting.innerText = `Hello ${username}!`;`
- text 삽입 시 사용

<br/>

## DRY (Don't Repeat Yourself)

### string convention
- string만 포함된 변수는 full UpperCase로 표기하는 관습
- If we make mistakes writing string: JS won't let us know.
- On the other hand, if we make mistakes writing variables, JS will let us know by showing error.
- Thus it's better to save repeated strings in variables.

### making function
- 반복되는 행위 역시 함수로 만들어주기

<br/>

## argument vs parameter
- `f(x) = 2x`와 같은 함수 정의 부분에서
    - 변수 `x`가 parameter(매개변수)가 되며
    - `f(2)`와 같은 함수 호출에서의 값 `2`가 함수의 argument(전달인자)가 된다.
> "...the procedure defines a parameter, and the calling code passes an argument to that parameter. **You can think of the parameter as a parking space and the argument as an automobile**."_ from [MSDN](https://docs.microsoft.com/en-us/dotnet/visual-basic/programming-guide/language-features/procedures/differences-between-parameters-and-arguments)

<br/>

## setTimeout vs setInterval
- Interval: sth over and over again e.g. 매 2초마다 발생시키기
    - setInterval(the function you want to run, every 'x' millisecond e.g. 5000 = 5s)       
- Timeout: 몇 초 후 발생시키기(단발성)     
    - setTimeout(the function you want to run, every 'x' millisecond e.g. 5000 = 5s)      
    - e.g. `setTimeout(sayHello, 5000);`

<br/>

## clock

### Date()
```
const date = new Date();
date.getHours();
date.getMinutes();
date.getSeconds();
```
- 보통은 `hours = date.getHours()`와 같이 변수에 넣어 사용
- `Date.now()`: useful way to get random number.
- 한자리 숫자가 두자리로 표현되진 않음 e.g. `13:01`이 아닌 `13:1`로 표기됨
    - *Remember, all developers experience same problems.*

### `.padStart()` and `.padEnd()`
- string에 적용 가능
    - 따라서 숫자인 시간은 string으로 변환 후 적용해줘야 

- string이 2글자가 되지 않는다면 앞에 "0" 붙이기 by using `.padStart()`
```
"1".padStart(2, "0"); // "01"
// "1"이라는 string이 2글자가 되지 않는다면 앞에 "0"을 붙여주세요라는 의미

"hello".padStart(20, "x"); // "xxxxxxxxxxxxxxxhello"
```

- string이 2글자가 되지 않는다면 뒤에 "0" 붙이기 by using `.padEnd()`
```
"1".padEnd(2, "0"); // "10"
// "1"이라는 string이 2글자가 되지 않는다면 뒤에 "0"을 붙여주세요라는 의미
```

### How to make clock
```
function getClock() {
    const date = new Date();
    const hours = String(date.getHours()).padStart(2, "0");
    const minutes = String(date.getMinutes()).padStart(2, "0");
    const seconds = String(date.getSeconds()).padStart(2, "0");
    clock.innerText = `${hours}:${minutes}:${seconds}`;
}
```

<br/>

## Math
### `Math.random()`
- 0~1 사이의 랜덤한 숫자 반환
- `Math.random() * 10` 0~10 사이의 랜덤한 숫자 반환
- `Math.random() * 18` 0~18 사이의 랜덤한 숫자 반환

### 올림, 내림, 반올림
- `Math.round()` 반올림
- `Math.ceil()` ceiling천장 -> 올림
- `Math.floor()` floor바닥 -> 내림

### Array내의 element 랜덤하게 보여주기
- e.g. `Math.floor(Math.random()*10)`를 index`[]`로 활용하기 

<br/>

## `.createElement("tag")`
- the way to create HTML by JS
- e.g. `const bgImage = document.createElement("img");`

### `.appendChild()` and `.prepend()`
- for attachment
    - `appendChild`: attach at the end.
    - `prepend`: attatch at the front.
- add html to the body e.g. `document.body.appendChild(bgImage);`

<br/>

## 변수 관련
```
function handleToDoSubmit(event) {
    event.preventDefault();
    const newTodo = toDoInput.value;    // newTodo에 toDoInput.value를 복사해서 넣었을뿐. toDoInput에 들어오는 current value를 newTodo라는 변수에 넣었을뿐.
    toDoInput.value = "";    // 그러니 toDoInput.value만 영향을 받고 newTodo는 영향받지 않는다.
}
```

<br/>

## `.id`
- JS로 HTML 태그에 id 부여하는 방법 e.g. `li.id = 

<br/>

## .filter()
- old array에 수정을 가하는것이 아닌 new array를 만들어내 반환하는 것

<br/>

## Weather_location
- `navigator.geolocation.getCurrentPosition(function for success, function for failure)`
```
function onGeoSuccess(position) {
    const lat = position.coords.latitude;
    const lng = position.coords.longitude;
    console.log("You live in", lat, lng);
}

function onGeoError() {
    alert("Can't find your location :( So NO WEATHER for you!")
}

navigator.geolocation.getCurrentPosition(onGeoSuccess, onGeoError)
```








