# Lab 3 – Counter Application with useState

## Question

Create a Counter Application using React that displays the current counter value and provides **Increase**, **Decrease**, and **Reset** buttons. The counter should not go below 0. Allow the user to set a custom step value for how much to increment or decrement.

---

## Program

### `App.jsx`

```jsx
import { useState } from 'react';

const App = () => {
  const [count, setCount] = useState(0);
  const [step, setStep] = useState(1);

  const increase = () => setCount(count + step);

  const decrease = () => setCount(count - step >= 0 ? count - step : 0);

  const reset = () => setCount(0);

  return (
    <div style={styles.container}>
      <h1>Counter Application</h1>
      <h2>Counter Value: {count}</h2>

      <div>
        <label>Step Value: </label>
        <input
          type="number"
          value={step}
          onChange={(e) => setStep(Number(e.target.value))}
          style={styles.input}
        />
      </div>

      <div>
        <button onClick={increase} style={styles.button}>Increase</button>
        <button onClick={decrease} style={styles.button}>Decrease</button>
        <button onClick={reset} style={styles.resetButton}>Reset</button>
      </div>
    </div>
  );
};

const styles = {
  container: { textAlign: 'center', fontFamily: 'Arial, sans-serif', marginTop: '50px' },
  button: { margin: '10px', padding: '10px 20px', fontSize: '16px', cursor: 'pointer' },
  resetButton: { margin: '10px', padding: '10px 20px', fontSize: '16px', cursor: 'pointer', backgroundColor: 'red', color: 'white' },
  input: { marginLeft: '10px', padding: '5px', fontSize: '16px' },
};

export default App;
```

---

## Topics

- **What this program does** — Displays a number (counter) that the user can increase or decrease by a custom step value. The counter is prevented from going below 0. A reset button brings it back to 0.

- **Two useState hooks** *(new in Lab 3)* — Lab 1 used one state variable. Here, two are used: `count` for the current counter value and `step` for the increment/decrement amount. Both are managed independently.

- **Ternary operator for min-value guard** — `count - step >= 0 ? count - step : 0` prevents negative values. If subtracting would go below 0, it snaps to 0 instead.

- **onClick on buttons** — Each button has an `onClick` handler that calls a specific function (`increase`, `decrease`, `reset`). These functions call `setCount` to update state.

- **`Number(e.target.value)`** *(new in Lab 3)* — Input values are strings by default. Wrapping in `Number()` converts the string to a number before storing it in `step`.

- **`type="number"` input** *(new in Lab 3)* — Restricts the input to numeric values only and shows up/down arrows in the browser.

- **Inline styles via JS object** *(new in Lab 3)* — Instead of a CSS file, styles are defined as a JavaScript object (`const styles = { ... }`) and applied using `style={styles.button}`. CSS properties use camelCase (e.g., `backgroundColor` instead of `background-color`).
