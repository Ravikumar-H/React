# Lab 1 – Dynamic Input Display with useState

## Question

Use Vite to set up a new React project. Edit `App.jsx` to include a stateful component with `useState`. Add an input field and a `<h1>` element that displays text based on the input. Dynamically update the `<h1>` content as the user types.

---

## Program

### `App.jsx`

```jsx
import { useState } from 'react';
import './App.css';

function App() {
  const [text, setText] = useState('');

  return (
    <div className="App">
      <input
        type="text"
        placeholder="Type something..."
        value={text}
        onChange={(e) => setText(e.target.value)}
      />
      <h1><strong>You Typed: {text}</strong></h1>
    </div>
  );
}

export default App;
```

---

## Topics

- **What this program does** — Renders an input box. Whatever the user types is instantly shown inside a `<h1>` tag below it. No button click needed — it reacts on every keystroke.

- **useState** — A React hook that lets a functional component hold and update a value. `useState('')` initializes `text` as an empty string. `setText(...)` updates it.

- **Controlled Input** — The `<input>` element's `value` is tied to the state variable `text`. React owns the value, not the browser DOM.

- **onChange event** — Fires every time the user types a character. `e.target.value` gives the current string in the input box, which is passed to `setText`.

- **JSX expression `{text}`** — Curly braces inside JSX are used to embed JavaScript values or expressions directly into the HTML-like markup.

- **Two-way binding** — State → input value (controlled), input event → state update. This creates a live sync between what's typed and what's displayed.
