## raw value
- What programmers chose to write e.g. String, Int      
- Might make mistakes and JavaScript won't let us know which one is wrong(just showing error sign).     
- So instead of writing down raw value repeatedly we keep them in variables such as const.     
- Then JavaScript would specify which variable is wrong(in error).     

## `classList`
- classList allows us to work with a list of class names
  - `h1.classList.contain("className")`   
  - `h1.classList.remove("className")`    
  - `h1.classList.add("className")`   

```
const h1 = document.querySelector("div.hello:first-child hi");

function handleTitleClick() {
  const clickedClass = "clicked";
  if (h1.classList.contains(clickedClass)) {
    h1.classList.remove(clickedClass);
  } else {
    h1.classList.add(clickedClass);
  }
}

h1.addEventListener("click", handleTitleClick);
```

### toggle
- Check if a class name exist or not.
  - exist -> remove
  - doesn't exist -> add
- so the above lengthy code with `.contains`, `.remove`, `.add` could be replaced with below:
```
const h1 = document.querySelector("div.hello:first-child hi");

function handleTitleClick() {
  h1.classList.toggle("clicked"); //여기서는 반복해서 쓰이지 않으니 raw value 그대로 적어주기  
}

h1.addEventListener("click", handleTitleClick);
```
- but still, it's important to know the history of this toggle function.

## `.getElementById()`, `.querySelector()`
```
const loginForm = document.getElementById("login-form");
```
```
const loginForm = document.querySelector("#login-form");
```
- querySelector로는 tagName, Id 모두 검색 가능하니 selector 함께 명시해주기

<br/>

## check validity
- Never trust users, always test validation. e.g. required, length
- To trigger the validation of the input
  1. `if~else`
    ```
    function onLoginSubmit() {
    const userName = loginInput.value;
    if (userName === "") {
        alert("plz write your name :)");
    } else if (userName.length > 15) {
        alert("your name is too long :(")
    }
    console.log(userName);
    }
    ```
  2. Inside the element
    - e.g. `<input required maxlength="15" type="text" placeholder="What is your name?" />`
    - **input should be inside of the form tag**.

<br/>

## `<input type="submit">`
- Form will be submitted if we press the button or entere. 
  1. Form is being submitted,
  2. then the whole website will be refreshed

### Q. How to save the value w/o the page refreshing?
  - Refreshing is a default behavior of `form submit`.
  - Browsers are configured to do so.
  - We can stop this default behavior by `.preventDefault()`.

### eventListener's first argument
- Every eventListners has **information** about the event just occured in their first argument.
- We just need to make a space for those extra information then JS will fill the space automatically.
- As a convention, we usually name the first argument 'event'.

### `.preventDefault()`
- eventListener의 첫번째 argument 안에 있는 기본 function
- Stop default behaviors(e.g. refreshing)


