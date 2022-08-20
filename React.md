# React JS

### Create react Project
```js
npx create-react-app my-react-app
``` 

## Router

### Install react-router-dom
```js
npm i -D react-router-dom
```

### Usage of Router [BrowserRouter],Routes and Route

```js
import { BrowserRouter as Router, Routes, Route } from "react-router-dom";

export default function App() {
  return (
    <Router>
      <Routes>
        <Route path="/" element={<Layout />}>
          <Route index element={<Home />} />
          <Route path="blogs" element={<Blogs />} />
          <Route path="contact" element={<Contact />} />
          <Route path="*" element={<NoPage />} />
        </Route>
      </Routes>
    </Router>
  );
}
```
### Link

```js
import {Link} from "react-router-dom"

<Link to="/">Home</Link>
```

## Hooks

Hooks allow function components to have access to state and other React features. Because of this, class components are generally no longer needed.

### useState

```js
import React, { useState } from "react";
import ReactDOM from "react-dom";

function FavoriteColor() {
  const [color, setColor] = useState("red");

  return (
    <>
      <h1>My favorite color is {color}!</h1>
      <button
        type="button"
        onClick={() => setColor("blue")}
      >Blue</button>
    </>
  );
}
```

### useEffect

useEffect runs on every render. That means that when the count changes, a render happens, which then triggers another effect.

```js
mport { useState, useEffect } from "react";
import ReactDOM from "react-dom";

function Timer() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    setTimeout(() => {
      setCount((count) => count + 1);
    }, 1000);
  });

  return <h1>I've rendered {count} times!</h1>;
}

ReactDOM.render(<Timer />, document.getElementById('root'));
```
