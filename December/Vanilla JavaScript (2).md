***WIP***

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
- Check a class name existence
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
