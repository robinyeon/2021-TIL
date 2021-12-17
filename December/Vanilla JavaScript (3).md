***WIP***

```
const HIDDEN_CLASSNAME = "hidden";

function onLoginSubmit(event) {
    event.preventDefault();
    loginForm.classList.add(HIDDEN_CLASSNAME);
    const username = loginInput.value;
    localStorage.setItem("username", username);
    greeting.innerText = `Hello ${username}!`;
    greeting.classList.remove(HIDDEN_CLASSNAME);
}
```

## localStorage
- like a tiny DB
### localStorage.setItem("key", "value")
### localStorage.getItem("key")
### localStorage.removeItem("key")

## innerText


## string convention
- 일반적으로 string만 포함된 변수는 full대문자로 표기
- if we make mistakes writing string, JS won't let us know. on the other hand, if we make mistakes writing variables, JS let us know by error.
- repeated string is better to be saved in variables.

## making function
- 반복되는 행위는 함수로 만들어주기

## argument vs parameter
"...the procedure defines a parameter, and the calling code passes an argument to that parameter. You can think of the parameter as a parking space and the argument as an automobile."
`f(x) = x*x`와 같은 함수 정의 부분에서 변수 ‘x’가 매개변수(parameter)가 되며, f(2)와 같은 함수 호출 부분에서 값 ‘2’ 가 함수의 전달인자(argument)가 된다.


## setTimeout vs setInterval
interval: e.g. 매 2초 마다 일어나기 sth over and over and over again
setInterval(the function you want to run, every x millisecond e.g. 5000 = 5s)
setInterval(sayHello, 5000);

timeout: only once
setTimeout(the function you want to run, after x millisecond e.g. 5000 = 5s)
setTimeout(sayHello, 5000);

## Date()
const date = new Date();
date.getHours();
date.getMinutes();
date.getSeconds();

## problem solving
- all the developers have same problems. you can be almost sure there will be function.

## padStart padEnd
- 'string'이어야만 해. 그러니 숫자인 시간은 string으로 바꾸고 붙여줘야겠지.
//string이 2글자 되지 않는다면 앞에 0 붙이기 by padStart
// "1".padStart(2, "0");
// "1"이라는 string이 2글자(this string should be 2 characters long)가 되지 않는다면 앞(start of the string)에 "0"을 붙여주세요라는 의미

//string이 2글자 되지 않는다면 뒤에 0 붙이기 by padEnd
// "1".padEnd(2, "0");
// "1"이라는 string이 2글자(this string should be 2 characters long)가 되지 않는다면 뒤(end of the string)에 "0"을 붙여주세요라는 의미

"1".padStart(2, "0");
'01'
"12".padStart(2, "0");
'12'
"1".padEnd(2, "0");
'10'
"hello".padStart(20, "x");
'xxxxxxxxxxxxxxxhello'

### clock
```
function getClock() {
    const date = new Date();
    const hours = String(date.getHours()).padStart(2, "0");
    const minutes = String(date.getMinutes()).padStart(2, "0");
    const seconds = String(date.getSeconds()).padStart(2, "0");
    clock.innerText = `${hours}:${minutes}:${seconds}`;
}
```

## Math
Math.random() 0~1 사이의 랜덤한 숫자 반환
Math.random() * 10 0~10 사이의 랜덤한 숫자 반환
Math.random() * 20 0~20 사이의 랜덤한 숫자 반환

Math.round() 반올림
Math.ceil() 올림
Math.floor() 내림

`Math.floor(Math.random()*10)`

## create HTML from JS

//JS => HTML 하는 방법 createElement: create HTML by JS
const bgImage = document.createElement("img");
bgImage.src = `img/${chosenImage}`;

### appendChild
- add the html to the body
document.body.appendChild(bgImage);


## 복사
```
function handleToDoSubmit(event) {
    event.preventDefault();
    const newTodo = toDoInput.value;
    // newTodo에 복사해서 넣었을뿐
    // toDoInput에 들어오는 current value를 newTodo라는 변수에 넣었을뿐
    console.log(newTodo);
    toDoInput.value = "";
    // toDoInput.value만 영향받지 newTodo는 영향받지 않아
    console.log(newTodo, toDoInput.value);
}
```

## JSON.stringify()
object든 array든 string의 형태로 저장
## JSON.parse()
string => array

## Date.now()
useful way to get random number 

## .id
JS로 HTML태그에 id 만들기

## .filter()
old array에 수정하는것이 아닌 new array를 반환

## navigator.geolocation.getCurrentPosition()
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

## inspect tool > network
- 우리가 뭔갈 했을 때 인터넷에서 무슨일이 일어났는지 보여주는 탭









