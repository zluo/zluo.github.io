---
layout: default
title: react
Nav_order: 5
has_children: true
permalink: /docs/computer_lang/javascript
parent: Computer Language
---
## Working with Components, props and JSX

### 1. Rendering the root component and strict mode

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

### 2. Components as building blocks
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
### 3. What is JSX?

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
### 4. JavaScript logic in components

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

### 5. Styling React components
```javascript

const style ={color: "red", fontSize:"48px"}
return(
    <h1 style={style}>
)

<h1 style={{color:"red"}}>
```
### 6. Pssing and receiving props
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

```javascript```
```javascript```
```javascript```
```javascript```
```javascript```
```javascript```
```javascript```
```javascript```



