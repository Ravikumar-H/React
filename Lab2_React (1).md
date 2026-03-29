# Lab 2 – Passing Props from Parent to Child Components

## Question

Develop a React application that demonstrates the use of **props** to pass data from a parent component to child components. Include a parent `App`, a `Header` child that shows a title, and a `Footer` child that shows copyright text — all receiving their content as props from `App`.

---

## Program

### `App.jsx`

```jsx
import Header from './Header';
import Footer from './Footer';

const App = () => {
  return (
    <div style={{ textAlign: 'center' }}>
      <Header title="React Props Demo" />
      <main>
        <h2>Welcome to the React Props Example!</h2>
        <p>This demonstrates passing props from parent to child components.</p>
      </main>
      <Footer copyright="© 2025 MyReactApp. All rights reserved." />
    </div>
  );
};

export default App;
```

### `Header.jsx`

```jsx
import PropTypes from 'prop-types';

const Header = ({ title }) => {
  return (
    <header>
      <h1>{title}</h1>
    </header>
  );
};

Header.propTypes = {
  title: PropTypes.string.isRequired,
};

export default Header;
```

### `Footer.jsx`

```jsx
import PropTypes from 'prop-types';

const Footer = ({ copyright }) => {
  return (
    <footer>
      <p>{copyright}</p>
    </footer>
  );
};

Footer.propTypes = {
  copyright: PropTypes.string.isRequired,
};

export default Footer;
```

---

## Topics

- **What this program does** — The `App` component holds the data (title and copyright text) and passes them down to `Header` and `Footer` as props. Each child just receives and displays whatever it's given.

- **Props** — Short for "properties". The way a parent component sends data to a child. Like function arguments but for components. Read-only inside the child.

- **Destructuring props** — `({ title })` directly unpacks the `title` prop from the props object. Cleaner than writing `props.title`.

- **PropTypes** *(new in Lab 2)* — A type-checking library. `PropTypes.string.isRequired` means the prop must be provided and must be a string. Gives a warning in the console if violated.

- **Multiple component files** *(new in Lab 2)* — Unlike Lab 1 (single file), this lab splits the UI into `App.jsx`, `Header.jsx`, and `Footer.jsx`. Each is a separate file that exports its component.

- **Semantic HTML tags** *(new in Lab 2)* — `<header>`, `<main>`, `<footer>` are used instead of generic `<div>`s. They convey meaning to browsers and screen readers.

- **No useState here** — This lab is purely about data flow (parent → child). No interactivity or state changes.
