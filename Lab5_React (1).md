# Lab 5 – Dynamic Image Gallery with Component Composition

## Question

Develop a React application that demonstrates **component composition** and props. Create a `FigureList` parent and a `BasicFigure` child component. `FigureList` renders multiple `BasicFigure` components dynamically, passing image URLs and captions as props. Users can add or remove images. Include hover animations.

---

## Program

### `App.jsx`

```jsx
import FigureList from "./FigureList";

function App() {
  return (
    <div>
      <FigureList />
    </div>
  );
}

export default App;
```

### `BasicFigure.jsx`

```jsx
const BasicFigure = ({ src, caption, onRemove }) => {
  return (
    <div className="image-card">
      <img src={src} alt="Gallery" />
      <div className="caption">{caption}</div>
      <button onClick={onRemove}>Remove</button>
    </div>
  );
};

export default BasicFigure;
```

### `FigureList.jsx`

```jsx
import { useState } from "react";
import BasicFigure from "./BasicFigure";
import "./FigureList.css";

const initialImages = [
  { src: "https://images.unsplash.com/photo-1507525428034-b723cf961d3e", caption: "Image 1" },
  { src: "https://images.unsplash.com/photo-1523961131990-5ea7c61b2107", caption: "Image 2" },
  { src: "https://images.unsplash.com/photo-1506748686214-e9df14d4d9d0", caption: "Image 3" },
];

const FigureList = () => {
  const [images, setImages] = useState(initialImages);

  const addImage = () => {
    const randomId = Math.floor(Math.random() * 1000);
    const newImage = {
      src: `https://picsum.photos/400/300?random=${randomId}`,
      caption: `Image ${images.length + 1}`,
    };
    setImages([...images, newImage]);
  };

  const removeImage = (index) => {
    setImages(images.filter((_, i) => i !== index));
  };

  return (
    <div className="container">
      <h1>Dynamic Image Gallery</h1>
      <div className="buttons">
        <button onClick={addImage}>Add Image</button>
      </div>
      <div className="gallery">
        {images.map((image, index) => (
          <BasicFigure
            key={index}
            src={image.src}
            caption={image.caption}
            onRemove={() => removeImage(index)}
          />
        ))}
      </div>
    </div>
  );
};

export default FigureList;
```

### `FigureList.css`

```css
.container { text-align: center; padding: 20px; }
.buttons { margin-bottom: 20px; }
button { margin: 5px; padding: 10px 15px; font-size: 16px; border: none; cursor: pointer; background-color: green; color: white; border-radius: 5px; }
button:hover { background-color: darkgreen; }
.gallery { display: flex; flex-wrap: wrap; justify-content: center; gap: 15px; }
```

### `index.css`

```css
.image-card { width: 180px; height: 180px; text-align: center; overflow: hidden; border-radius: 10px; background: white; box-shadow: 2px 2px 10px rgba(0,0,0,0.1); transition: transform 0.3s ease-in-out; }
.image-card:hover { transform: scale(1.05); }
.image-card img { width: 100%; height: 55%; object-fit: cover; border-top-left-radius: 10px; border-top-right-radius: 10px; }
.caption { padding: 5px; font-size: 14px; font-weight: bold; }
```

---

## Topics

- **What this program does** — Displays a gallery of images in a grid. Users can add a new random image or remove any existing one. Images animate on hover. The gallery is built using two components — `FigureList` manages the data, `BasicFigure` renders each card.

- **Component composition** *(new in Lab 5)* — A design pattern where a parent component (`FigureList`) renders multiple instances of a child component (`BasicFigure`). The parent owns the data; the child only knows how to display one item.

- **Passing a function as prop (`onRemove`)** *(new in Lab 5)* — `onRemove={() => removeImage(index)}` passes a function down to the child as a prop. The child calls it via `onClick={onRemove}`. This allows a child to trigger a state change in the parent — the only way a child can "communicate upward".

- **External data array (`initialImages`)** *(new in Lab 5)* — The starting list of images is defined outside the component as a constant. This is then passed into `useState` as the initial value.

- **`Math.floor(Math.random() * 1000)`** *(new in Lab 5)* — Generates a random integer used as a query param in the Picsum URL to fetch a different random image each time.

- **CSS `transition` + `:hover` for animation** *(new in Lab 5)* — `transition: transform 0.3s ease-in-out` on `.image-card` makes the scale change animate smoothly. `.image-card:hover { transform: scale(1.05) }` enlarges the card slightly when hovered.

- **`object-fit: cover`** *(new in Lab 5)* — Ensures the image fills its container without distortion, cropping edges if needed. Essential for uniform gallery card sizes.

- **CSS Flexbox for the gallery grid** *(new in Lab 5)* — `display: flex; flex-wrap: wrap; gap: 15px` arranges the cards side by side and wraps them to the next row when there's no more horizontal space.

- **Separation of concerns across files** *(extended from Lab 2)* — Logic lives in `FigureList.jsx`, individual card UI in `BasicFigure.jsx`, layout styles in `FigureList.css`, and card styles in `index.css`. Each file has one clear responsibility.
