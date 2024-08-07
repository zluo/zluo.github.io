---
layout: default
title: react
Nav_order: 5
has_children: true
permalink: /docs/computer_lang/javascript
parent: Computer Language
---
## 1. Setup react
### 1.1. Create react application

    npx create-react-app usepopcorn

### 1.2. run react application
    npm start



## 2. Working with Components, props and JSX

### 2.1. Rendering the root component and strict mode

```html
<html lang="en">
  <head>
    <title>Fast React Pizza Co.</title> -->
  </head>
  <body>
    <div id="root"></div>
  </body>
</html>
```

```javascript
const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```

### 2.2 Components as building blocks
```html
function Order({ closeHour, openHour }) {
  return (
    <div className="order">
      <p>
        We're Open from {openHour}:00 to {closeHour}:00, come visit us or order
        online.
      </p>
      <button className="btn">Order</button>
    </div>
  );
}
```
### 2.3. What is JSX?

Extension of JavaScript that allows us to embed javascript, css and react components into HTML.

```Javascript
<header>
  <h1 style="color:re">Hello React!</h1>
</header>
```
through BABEL

```javascript
React.createElement(
    'header',
    null,
    React.createElement(
        'h1',
        {style: {color: 'red}},
        'Hello React!"
    )
)
```
### 2.4. JavaScript logic in components

code between {}
```javascript

function Pizza({ pizzaObj }) {
  //if (pizzaObj.soldOut) return null;

  return (
    <li className={pizzaObj.soldOut? 'pizza sold-out': "pizza"}>
      <img src={pizzaObj.photoName} alt={pizzaObj.name}></img>
      <div>
        <h3>{pizzaObj.name}</h3>
        <p>{pizzaObj.ingredients}</p>
        <span>{pizzaObj.soldOut? "SOLD OUT" : pizzaObj.price}</span>
      </div>
    </li>
  );
}
```

### 2.5. Styling React components
```javascript
const style ={color: "red", fontSize:"48px"}
return(
    <h1 style={style}>
)

<h1 style={{color:"red"}}>
```
### 2.6. Pssing and receiving props

props is data from the outside, and can be updated by the parent. Props are immutable. It's a one way data flow

```javascript
<Pizza pizzaObj={pizza} key={pizza.name} />
...
function Pizza({ pizzaObj }) {
  return (
    <li className={pizzaObj.soldOut? 'pizza sold-out': "pizza"}>
      <img src={pizzaObj.photoName} alt={pizzaObj.name}></img>
      <div>
        <h3>{pizzaObj.name}</h3>
        <p>{pizzaObj.ingredients}</p>
        <span>{pizzaObj.soldOut? "SOLD OUT" : pizzaObj.price}</span>
      </div>
    </li>
  );
}
```
### 2.7. The rules of JSX

1. like HTML, but can enter javascript mode with {}
1. javascript expressions examples: variables, arrays, objects, [].map(), ternary operations
1. not allowed (if/else, for, switch)
1. one root element

A piece of JSX is just a piece of javascript

```javascript
  const el = <h1>Hello React</h1>
  const el = React.createElement("h1", null, "Hello React!")
```
so 
1. we can place other JSX inside {}
1. we can write JSX anywhere inside a component (in if/else, assign to variables, pass it into functions )

### 8. Rendering List

```javascript
         <ul className="pizzas">
            {pizzas.map((pizza) => (
              <Pizza pizzaObj={pizza} key={pizza.name} />
            ))}
          </ul>
```
### 2.9. Conditional Rendering with &&

```javascript
  { isOpen && <p>open</p>}
```
### 2.10. Conditional Rendering with Ternaries

```javascript
      {isOpen ? (
        <Order closeHour={closeHour} openHour={openHour} />
      ) : (
        <p>we will open on {openHour}, come visit us or order online</p>
      )}
```

### 2.11. Destructuring Props
```javascript
    <Pizza pizzaObj={pizza} key={pizza.name} />
...
    function Pizza({ pizzaObj }) { ...}
```
### 2.12. React Fragment
```javascript
  <>
  ...
  </>
```
### 2.13. Setting classes and text conditionarly


```javascript
    <li className={pizzaObj.soldOut? 'pizza sold-out': "pizza"}>
    <span>{pizzaObj.soldOut? "SOLD OUT" : pizzaObj.price}</span>
```
## 3. State, Events and Forms

### 3.1 Handle events the React way
```javascript
  function handleNext() {
    if (step < 3) setStep((s) => s + 1);
  }
  <Button bgColor="#7950f2" textColor="#fff" onClick={handlePrevious}>

  <button className="close" onClick={() => setIsOpen((is) => !is)}>
```
### 3.2 state

1. what is state? 
    
    component's memory. component hold it through it lifecycle.
2. Updating component state triggers re-render the component.
   
### 3.3 Creatng a State Variable with useState
```javascriptP
  const [step, setStep] = useState(1);
```
1. step is the variable
2. setStep is the set method
3. 1 is the initial value.

### 3.4 Updating State Based on the Current State
use a callback function to update the state

```javascript
  setStep((s)=> s +1)
  setStep((s)=> s +1)
```
### 3.5 More thought about State
1. each component manager it's own state.
1. UI is a function of it's state. we view UI as a reflection of data.

$$ UI=f(state) $$

GuideLine

### 3.6 State Lift up

### 3.7 Derived State


### 3.8 Sorted List
```javascript
  sortedItems = items.slice().sort((a,b) => Number(a.packed) > Number(b.packed))

```
### 3.9 Children prop
```javascript
function Button({children}){
  return (
      <button className="button">{children}</button>
  )
}

<Button>AddFriend</Button>
```

## 4. Thinking in react, components, composition and resusability
### 4.1 Component Category
1. presentational components (logo, )
2. Stateful components
3. Structural Components (layout)
   
### 4.2 Component Composition
```javascript
  function Modal({chidren}){
    <div>
    {chidren}
    </div>
  }

  <Model>
    <Success />
  </Model>

  <Model>
    <Error />
  </Model>

```
### 4.3 prop drilling
  one solution is component composition

### Passing Element as Props
    <Box element={MovieList movies={movies} />

    function Box({element}){
      <Box>
      {element}
      </Box>
    }

### Proptypes

```javascript```





### Fetch Data

```javascript
useEffect(function () {
    async function fetchMovies() {
      setIsLoading(true);
      const res = await fetch(
        `http://www.omdbapi.com/?apikey=${KEY}&s=${query}`
      );
      const data = await res.json();
      setMovies(data.Search);
      setIsLoading(false);
    }
    fetchMovies();
  }, []);
```

### Handle Error

```javascript
  const [error, setError] = useState(false);

  try {
        if (data.Response === "False") 
          throw "Movie not found"
      } catch (err) {
        console.log(err);
        setError(err);
      } finally {
        setIsLoading(false);
      }

```

```javascript
    <ListBox>
          {isLoading && <Loader />}
          {!isLoading && !error && <MovieList movies={movies} />}
          {error && <Error message={error} />}
    </ListBox>
```

### What is useEffect dependency array

- Each time one of the dependencies changes, the effect will be executed again.
- Every state variable and prop used inside the effect must be included in the dependency array.
 