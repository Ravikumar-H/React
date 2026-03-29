# Lab 4 – To-Do List Application with useState

## Question

Develop a To-Do List application using React functional components. It should allow users to add tasks, mark them as completed or pending (with visual differentiation), and delete tasks from the list.

---

## Program

### `App.jsx`

```jsx
import { useState } from 'react';

const ToDoFunction = () => {
  const [tasks, setTasks] = useState([]);
  const [taskInput, setTaskInput] = useState('');

  const addTask = () => {
    if (taskInput.trim() !== '') {
      setTasks([...tasks, { text: taskInput, completed: false }]);
      setTaskInput('');
    }
  };

  const toggleTask = (index) => {
    const updatedTasks = [...tasks];
    updatedTasks[index].completed = !updatedTasks[index].completed;
    setTasks(updatedTasks);
  };

  const deleteTask = (index) => {
    const updatedTasks = tasks.filter((_, i) => i !== index);
    setTasks(updatedTasks);
  };

  return (
    <div style={styles.container}>
      <h1>React To-Do List</h1>
      <div>
        <input
          type="text"
          value={taskInput}
          onChange={(e) => setTaskInput(e.target.value)}
          placeholder="Enter a task..."
          style={styles.input}
        />
        <button onClick={addTask} style={styles.addButton}>Add Task</button>
      </div>

      <ul style={styles.list}>
        {tasks.map((task, index) => (
          <li key={index} style={task.completed ? styles.completedTask : styles.pendingTask}>
            <span onClick={() => toggleTask(index)} style={{ cursor: 'pointer' }}>
              {index + 1}. {task.completed ? '✔' : '✘'} {task.text}
            </span>
            <button onClick={() => deleteTask(index)} style={styles.deleteButton}>🗑</button>
          </li>
        ))}
      </ul>
    </div>
  );
};

const styles = {
  container: {
      textAlign: 'center',
      fontFamily: 'Arial,
      sans-serif',
      marginTop: '50px'
    },
  input: {
      padding: '10px',
      fontSize: '16px',
      width: '250px'
    },
  addButton:{
      marginLeft: '10px',
      padding: '10px',
      fontSize: '16px',
      cursor: 'pointer'
    },
  list: {
      listStyleType: 'none',
      padding: 0,
      marginTop: '20px'
    },
  pendingTask: {
      padding: '10px',
      fontSize: '18px',
      borderBottom: '1px solid #ddd',
      display: 'flex',
      justifyContent: 'space-between',
      alignItems: 'center',
  },
  completedTask: {
      padding: '10px',
      fontSize: '18px',
      textDecoration: 'line-through',
      color: 'gray',
      borderBottom: '1px solid #ddd',
      display: 'flex',
      justifyContent: 'space-between',
      alignItems: 'center',
    },
  deleteButton: {
    background: 'none',
      border: 'none',
      fontSize: '18px',
      cursor: 'pointer'
  },
};

export default ToDoFunction;
```

---

## Topics

- **What this program does** — A task manager where users type a task, add it to a list, toggle it between completed/pending by clicking, and delete it. Completed tasks appear with a strikethrough and gray color.

- **Array as state** *(new in Lab 4)* — Unlike previous labs which stored a string or number, this lab stores an **array of objects** in state: `[{ text: "...", completed: false }, ...]`. Each task is an object with two fields.

- **Spread operator `[...tasks, newTask]`** *(new in Lab 4)* — Creates a new array with all existing tasks plus the new one. React requires immutability — you cannot push directly into state; you must create a new array.

- **`.map()` to render a list** *(new in Lab 4)* — Loops over the tasks array and returns a `<li>` JSX element for each task. This is the standard React way to render dynamic lists.

- **`key` prop** *(new in Lab 4)* — `key={index}` is required when rendering a list with `.map()`. React uses it to track which list items changed, were added, or removed efficiently.

- **`.filter()` to delete** *(new in Lab 4)* — `tasks.filter((_, i) => i !== index)` returns a new array that excludes the task at the given index. The `_` ignores the task value since only the index is needed.

- **Conditional styling** — `task.completed ? styles.completedTask : styles.pendingTask` switches between two style objects based on the task's status. Completed tasks get `textDecoration: 'line-through'`.

- **`.trim()` validation** — `taskInput.trim() !== ''` prevents adding blank or whitespace-only tasks.

- **`toggleTask`** — Copies the array with spread, flips the `completed` boolean at the given index, then sets the new array as state. Direct mutation of state is avoided.
