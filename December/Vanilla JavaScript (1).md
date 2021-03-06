## The Document Object
- JavaScript is already configured to manipulate(read and add) HTML which is done automatically.
- **`document` is magical object that is given to us by browser to interact with HTML.**
  - Grabbing the HTML by JavaScript then showing the object on its own way.
- `console.dir(document)` brings the HTML from the point of view of JavaScript: object.
  - e.g. `document.title`
  - `console.dir()` let us open up more details of the element in object form.

> JavaScript를 통해 브라우저와 커뮤니케이션이 가능하며, 이를 통해 HTML을 변경할 수 있다.      
> 서버와 클라이언트 사이의 주고받음은 HTML이 아닌 JavaScript를 통해 이루어진다.

<br/>

## Searching for Elements
- Grab one specific thing: `document.getElementById("id")`
- `document.querySelector(".hello h1")` allows us to search for an element using **css notation**.
  - `.querySelector` returns only the first element if there's many.
  - Instead, `document.querySelectorAll("")` shows an array of every elements that matches condition.

<br/>

## Events
- **Event**: click, enter, cursor on, etc.
- JavaScript can listen to those events.

### `.addEventListener("event", function)` 
- Specify which event you care about.
- e.g. `title.addEventListener("click", function)`: when "click"ed, we want to execute the "function".
- Parenthesis in the function`()` means 'press play immediately'.
  - We don't want to play the function immediately in `addEventListener`.
  - We just want to pass the function 'name' without `()` to JavaScript so that JS can press play instead of us when users clicked something.
  - **Do not put parenthesis in the callback.**

### How to find `event` name
1. search mdn or
2. on*eventname* series from `console.dir()` e.g. onClick

#### (fyi) 2 ways
- title.onClick = handleTitleClick
- title.addEvenetListener("click", handleTitleClick)

<br/>

## Recap
```
const h1 = document.querySelector("div.hello:first-child h1");

function handleTitleClick() {
    const currentColor = h1.style.color;
    let newColor;
    if (currentColor === "blue") {
        newColor = "tomato";
    } else {
        newColor = "blue";
    }
    h1.style.color = newColor;
}

h1.addEventListener("click", handleTitleClick);
```
1) click event 발생 및 함수 실행
2) currentColor 변수 선언 후 `h1.style.color` 값 복사 (getter)
3) `newColor` 변수 선언
4) `currentColor` 현재 값 확인
5) 조건에 따라 `newColor`에 "tomato" or "blue" 값 대입
6) 마지막으로 `h1.style.color`에 `newColor`값 대입 (setter)


