---
layout: default
title: Javascript Summary
nav_order: 2
parent: javascript
grand_parent: Computer Language
---


## example:

```javascript
book = {
    id: 2,
    title: "The Cyberiad",
    publicationDate: "1965-01-01",
    author: "Stanislaw Lem",
    genres: [
      "science fiction",
      "humor",
      "speculative fiction",
      "short stories",
      "fantasy",
    ],
    hasMovieAdaptation: false,
    pages: 295,
    translations: {},
    reviews: {
      goodreads: {
        rating: 4.16,
        ratingsCount: 11663,
        reviewsCount: 812,
      },
      librarything: {
        rating: 4.13,
        ratingsCount: 2434,
        reviewsCount: 0,
      },
    },
  }
```

## Destructuring

### Get value from object

```javascript
const { title, author, pages, publicationDate, genres } = book;
```

## Rest/Spread Operator

```javascript
const [primaryGenre, secondaryGenre, ...otherGenres] = genres;
```
### Append new value to existing object

```javascript
const newGenres = [... genres, "new genre"];
```
### Update existing value

```javascript
const newBook = {...book, moviePublicationDate: "12-12-2034", pages: 1201} //override pages
```

## Template Literals

```javascript
const summary =`${title} is a Movie`
```

## Ternaries 
```javascript
 isTrue? "Open": "Close"
```

## Arrow Functions

```javascript
const summary = (e)=> setSale(e.target.value)
```

## Short-Circuited Functions

```javascript

```

## Operators: && || ??


```javascript
const count = book.reviews.librarything.reviewsCount ?? "no data" // if reviewsCount is not defined
```

## Optioanl Chaining

```javascript
  const literature = book.reviews?.librarything?.reviewsCount ?? 0
```

## The Array map Method


```javascript
const essentialData = books.map((book) => ({title: book.title, 
    author: book.author,
    reviewsCount: getTotalReviewCount(book)
}))
```

## The Array filter Method

```javascript
const longBooks = books.filter((book) => book.pages > 500).filter((book) => book.hasMovieAdaptation)
```

## The Array reduce Method

```javascript
const pagesAllBooks = books.reduce((sum, book) => sum + book.pages, 0)
```
## The Array sort Method

```javascript
const arr = [3,7,1,9,6]
const sorted = arr.slice().sort((a,b) => a - b)
```
## Working with Immutable Array

### Add the new element

```javascript
const booksAfterAdd = [...books, newBook]
```

### Delete the element

```javascript
const booksAfterAdd = [...books, newBook]
```
### Update the element

```javascript
const bookAfterUpdate = booksAfterDelete.map(book => book.id===1 ? {...book, pages:200}:book)
```
### JavaScript Async Operations

```javascript
fetch('https://jsonplaceholder.typicode.com/todos/1')
      .then(response => response.json())
      .then(json => console.log(json))
console.log("jonas")

async function getTodos(){
  const res = await fetch("https://jsonplaceholder.typicode.com/todos/1")
  const data = await res.json()
  return data
}
const todo = await getTodos()
console.log(todo)
```
```javascript
```
```javascript
```
```javascript
```
```javascript
```
```javascript
```
```javascript
```
```javascript
```
```javascript
```
```javascript
```
```javascript
```
```javascript
```
```javascript
```
