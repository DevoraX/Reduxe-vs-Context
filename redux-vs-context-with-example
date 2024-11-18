
# Redux vs Context API in React

## Introduction
React offers multiple ways to manage state in your applications. Two of the most popular approaches are **Redux** and **Context API**. This article compares these two methods and provides examples using a simple To-Do List application.

## What is Redux?
Redux is a state management library that provides a centralized store to manage the state of your application. It uses actions and reducers to handle state changes in a predictable way.

### Pros of Redux
- Centralized and predictable state management.
- Easy to debug with Redux DevTools.
- Suitable for large applications with complex state.

### Cons of Redux
- Requires a lot of boilerplate code.
- Might be overkill for small applications.

## What is Context API?
Context API is a built-in feature in React that allows you to share state across components without prop drilling. It's a simpler alternative to Redux for managing state in smaller applications.

### Pros of Context API
- No additional libraries needed.
- Simple to use for small to medium-sized apps.
- Less boilerplate compared to Redux.

### Cons of Context API
- Can lead to performance issues with frequent re-renders.
- Limited features compared to Redux.

## To-Do List Example
Below are two implementations of a To-Do List application using **Redux** and **Context API**.

### Version 1: Using Redux

#### `store.js`
```javascript
import { createStore } from 'redux';

const initialState = {
  todos: []
};

const reducer = (state = initialState, action) => {
  switch (action.type) {
    case 'ADD_TODO':
      return { ...state, todos: [...state.todos, action.payload] };
    case 'REMOVE_TODO':
      return { ...state, todos: state.todos.filter((todo, index) => index !== action.payload) };
    default:
      return state;
  }
};

const store = createStore(reducer);
export default store;
```

#### `App.js`
```javascript
import React, { useState } from 'react';
import { Provider, useDispatch, useSelector } from 'react-redux';
import store from './store';

const App = () => {
  const [input, setInput] = useState('');
  const todos = useSelector((state) => state.todos);
  const dispatch = useDispatch();

  const addTodo = () => {
    dispatch({ type: 'ADD_TODO', payload: input });
    setInput('');
  };

  const removeTodo = (index) => {
    dispatch({ type: 'REMOVE_TODO', payload: index });
  };

  return (
    <div>
      <h2>Redux To-Do List</h2>
      <input value={input} onChange={(e) => setInput(e.target.value)} />
      <button onClick={addTodo}>Add</button>
      <ul>
        {todos.map((todo, index) => (
          <li key={index} onClick={() => removeTodo(index)}>{todo}</li>
        ))}
      </ul>
    </div>
  );
};

export default function ReduxTodo() {
  return (
    <Provider store={store}>
      <App />
    </Provider>
  );
}
```

### Version 2: Using Context API

#### `TodoContext.js`
```javascript
import React, { createContext, useState } from 'react';

export const TodoContext = createContext();

export const TodoProvider = ({ children }) => {
  const [todos, setTodos] = useState([]);

  const addTodo = (todo) => setTodos([...todos, todo]);
  const removeTodo = (index) => setTodos(todos.filter((_, i) => i !== index));

  return (
    <TodoContext.Provider value={{ todos, addTodo, removeTodo }}>
      {children}
    </TodoContext.Provider>
  );
};
```

#### `App.js`
```javascript
import React, { useContext, useState } from 'react';
import { TodoContext, TodoProvider } from './TodoContext';

const TodoList = () => {
  const { todos, removeTodo } = useContext(TodoContext);
  return (
    <ul>
      {todos.map((todo, index) => (
        <li key={index} onClick={() => removeTodo(index)}>{todo}</li>
      ))}
    </ul>
  );
};

const AddTodo = () => {
  const [input, setInput] = useState('');
  const { addTodo } = useContext(TodoContext);

  const handleAdd = () => {
    addTodo(input);
    setInput('');
  };

  return (
    <div>
      <input value={input} onChange={(e) => setInput(e.target.value)} />
      <button onClick={handleAdd}>Add</button>
    </div>
  );
};

const App = () => (
  <TodoProvider>
    <h2>Context API To-Do List</h2>
    <AddTodo />
    <TodoList />
  </TodoProvider>
);

export default App;
```

## Conclusion
Both Redux and Context API offer powerful solutions for managing state in React applications. Redux is more suited for large, complex applications, while Context API is a great choice for simpler projects.

## 📜 License
This project is licensed under the MIT License.
