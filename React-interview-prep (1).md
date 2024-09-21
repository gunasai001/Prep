# Frontend JavaScript Frameworks (React) - Deep Dive

## React Fundamentals

### Components: Functional and Class Components

React applications are built using components, which are reusable pieces of UI. There are two types of components:

1. Functional Components:
   - Introduced in React 16.8 with hooks
   - Simpler syntax, easier to read and test
   - Use hooks for state and lifecycle features
   
   Example:
   ```jsx
   function Welcome(props) {
     return <h1>Hello, {props.name}</h1>;
   }
   ```

2. Class Components:
   - Traditional way of writing components
   - Extend from React.Component
   - Have access to lifecycle methods
   
   Example:
   ```jsx
   class Welcome extends React.Component {
     render() {
       return <h1>Hello, {this.props.name}</h1>;
     }
   }
   ```

### Props: Passing Data Between Components

Props (short for properties) are a way to pass data from parent to child components. They are read-only and help make your components reusable.

Example:
```jsx
function ParentComponent() {
  return <ChildComponent name="John" age={30} />;
}

function ChildComponent(props) {
  return <p>{props.name} is {props.age} years old.</p>;
}
```

### State: Managing Local Component State

State represents the internal data of a component that can change over time. When state changes, React re-renders the component.

In class components:
```jsx
class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = { count: 0 };
  }
  
  incrementCount = () => {
    this.setState((prevState) => ({ count: prevState.count + 1 }));
  }

  render() {
    return (
      <div>
        <p>Count: {this.state.count}</p>
        <button onClick={this.incrementCount}>Increment</button>
      </div>
    );
  }
}
```

In functional components (using hooks):
```jsx
function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}
```

### JSX: Syntax Extension for React

JSX is a syntax extension for JavaScript that looks similar to XML or HTML. It allows you to write HTML-like code in your JavaScript files, making it easier to describe what the UI should look like.

Example:
```jsx
const element = <h1 className="greeting">Hello, world!</h1>;
```

JSX gets transformed into regular JavaScript function calls:
```javascript
const element = React.createElement(
  'h1',
  {className: 'greeting'},
  'Hello, world!'
);
```

### Lifecycle Methods (for Class Components)

Lifecycle methods are special methods that get called at different phases of a component's life. The main lifecycle phases are:

1. Mounting: 
   - constructor()
   - render()
   - componentDidMount()

2. Updating:
   - shouldComponentUpdate()
   - render()
   - componentDidUpdate()

3. Unmounting:
   - componentWillUnmount()

Example:
```jsx
class LifecycleDemo extends React.Component {
  componentDidMount() {
    console.log('Component mounted');
  }

  componentDidUpdate(prevProps, prevState) {
    console.log('Component updated');
  }

  componentWillUnmount() {
    console.log('Component will unmount');
  }

  render() {
    return <div>Lifecycle Demo</div>;
  }
}
```

### Virtual DOM and Reconciliation Process

The Virtual DOM is a lightweight copy of the actual DOM. When state changes in a React application:

1. React creates a new Virtual DOM tree
2. It compares this new tree with the previous one (diffing)
3. It calculates the minimum number of changes needed to update the real DOM
4. It updates the real DOM in a single batch (reconciliation)

This process makes React efficient in updating the UI.

## React Hooks

Hooks are functions that let you "hook into" React state and lifecycle features from functional components.

### useState: Managing State in Functional Components

useState allows functional components to have state.

Example:
```jsx
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}
```

### useEffect: Side Effects in Functional Components

useEffect lets you perform side effects in functional components. It's a combination of componentDidMount, componentDidUpdate, and componentWillUnmount.

Example:
```jsx
import React, { useState, useEffect } from 'react';

function Example() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `You clicked ${count} times`;
  }, [count]); // Only re-run the effect if count changes

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}
```

### useContext: Consuming Context in Functional Components

useContext makes it easy to consume context in functional components without nesting.

Example:
```jsx
import React, { useContext } from 'react';

const ThemeContext = React.createContext('light');

function ThemedButton() {
  const theme = useContext(ThemeContext);
  return <button style={{ background: theme }}>I am styled by theme context!</button>;
}
```

### useRef: Accessing DOM Elements or Storing Mutable Values

useRef returns a mutable ref object whose .current property is initialized to the passed argument. It's commonly used to access DOM elements directly.

Example:
```jsx
import React, { useRef } from 'react';

function TextInputWithFocusButton() {
  const inputEl = useRef(null);
  const onButtonClick = () => {
    inputEl.current.focus();
  };
  return (
    <>
      <input ref={inputEl} type="text" />
      <button onClick={onButtonClick}>Focus the input</button>
    </>
  );
}
```

### useMemo: Memoizing Expensive Computations

useMemo is used to memoize expensive computations so that they are only recomputed when one of their dependencies changes.

Example:
```jsx
import React, { useMemo } from 'react';

function ExpensiveComputation({ a, b }) {
  const memoizedValue = useMemo(() => {
    // Expensive computation here
    return a * b * Math.random();
  }, [a, b]);

  return <div>{memoizedValue}</div>;
}
```

### useCallback: Memoizing Functions

useCallback returns a memoized version of the callback that only changes if one of the dependencies has changed. It's useful for optimizing child component re-renders.

Example:
```jsx
import React, { useCallback } from 'react';

function ParentComponent() {
  const [count, setCount] = useState(0);

  const incrementCount = useCallback(() => {
    setCount(prevCount => prevCount + 1);
  }, []);

  return <ChildComponent onIncrement={incrementCount} />;
}
```

### Custom Hooks: Creating Reusable Stateful Logic

Custom hooks allow you to extract component logic into reusable functions. They start with "use" and can call other hooks.

Example:
```jsx
import { useState, useEffect } from 'react';

function useWindowWidth() {
  const [width, setWidth] = useState(window.innerWidth);
  
  useEffect(() => {
    const handleResize = () => setWidth(window.innerWidth);
    window.addEventListener('resize', handleResize);
    return () => {
      window.removeEventListener('resize', handleResize);
    };
  }, []);

  return width;
}

// Usage
function MyComponent() {
  const width = useWindowWidth();
  return <div>Window width is {width}</div>;
}
```

## Context API

The Context API provides a way to pass data through the component tree without having to pass props down manually at every level.

### Creating and Providing Context

Example:
```jsx
import React from 'react';

const ThemeContext = React.createContext('light');

function App() {
  return (
    <ThemeContext.Provider value="dark">
      <Toolbar />
    </ThemeContext.Provider>
  );
}
```

### Consuming Context with useContext Hook

Example:
```jsx
import React, { useContext } from 'react';

function ThemedButton() {
  const theme = useContext(ThemeContext);
  return <button style={{ background: theme }}>I am styled by theme context!</button>;
}
```

### Use Cases for Global State Management

Context is great for:
- Theming
- User authentication status
- Language preferences
- Any data that needs to be accessible by many components at different nesting levels

## React Router

React Router is the standard routing library for React.

### Setting Up Routes

Example:
```jsx
import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';

function App() {
  return (
    <Router>
      <Switch>
        <Route exact path="/" component={Home} />
        <Route path="/about" component={About} />
        <Route path="/users" component={Users} />
      </Switch>
    </Router>
  );
}
```

### Route Parameters and Query Strings

Example:
```jsx
<Route path="/users/:id" component={User} />

// In the User component
function User({ match }) {
  return <h2>User ID: {match.params.id}</h2>;
}
```

### Nested Routing

Example:
```jsx
function Users({ match }) {
  return (
    <div>
      <h2>Users</h2>
      <Route path={`${match.path}/:id`} component={User} />
    </div>
  );
}
```

### Programmatic Navigation

Example:
```jsx
import { useHistory } from 'react-router-dom';

function HomeButton() {
  let history = useHistory();

  function handleClick() {
    history.push('/home');
  }

  return <button onClick={handleClick}>Go home</button>;
}
```

### Protected Routes

Example:
```jsx
function PrivateRoute({ component: Component, ...rest }) {
  return (
    <Route
      {...rest}
      render={props =>
        isAuthenticated ? (
          <Component {...props} />
        ) : (
          <Redirect to="/login" />
        )
      }
    />
  );
}
```

## State Management

### Redux

Redux is a predictable state container for JavaScript apps.

#### Actions, Reducers, and Store

Actions:
```javascript
const ADD_TODO = 'ADD_TODO';
function addTodo(text) {
  return {
    type: ADD_TODO,
    text
  };
}
```

Reducers:
```javascript
function todoReducer(state = [], action) {
  switch (action.type) {
    case ADD_TODO:
      return [...state, { text: action.text, completed: false }];
    default:
      return state;
  }
}
```

Store:
```javascript
import { createStore } from 'redux';
const store = createStore(todoReducer);
```

#### Middleware (e.g., redux-thunk, redux-saga)

Redux Thunk example:
```javascript
function fetchTodos() {
  return function(dispatch) {
    return fetch('/api/todos')
      .then(response => response.json())
      .then(todos => dispatch({ type: 'RECEIVE_TODOS', todos }));
  };
}
```

#### Selectors and Reselect Library

Selectors:
```javascript
const getTodos = state => state.todos;
const getVisibilityFilter = state => state.visibilityFilter;

import { createSelector } from 'reselect';

const getVisibleTodos = createSelector(
  [getTodos, getVisibilityFilter],
  (todos, filter) => {
    switch (filter) {
      case 'SHOW_COMPLETED':
        return todos.filter(todo => todo.completed);
      case 'SHOW_ACTIVE':
        return todos.filter(todo => !todo.completed);
      default:
        return todos;
    }
  }
);
```

#### Redux Toolkit for Simplified Redux Usage

Example:
```javascript
import { createSlice } from '@reduxjs/toolkit';

const todosSlice = createSlice({
  name: 'todos',
  initialState: [],
  reducers: {
    addTodo: (state, action) => {
      state.push({ text: action.payload, completed: false });
    },
    toggleTodo: (state, action) => {
      const todo = state.find(todo => todo.id === action.payload);
      if (todo) {
        todo.completed = !todo.completed;
      }
    }
  }
});

export const { addTodo, toggleTodo } = todosSlice.actions;
export default todosSlice.reducer;
```

### MobX

MobX is a simple, scalable state management solution.

#### Observables, Actions, and Reactions

Example:
```javascript
import { makeObservable, observable, action, computed } from 'mobx';

class TodoStore {
  todos = [];

  constructor() {
    makeObservable(this, {
      todos: observable,
      addTodo: action,
      completedTodosCount: computed
    });
  }

  addTodo(text) {
    this.todos.push({ text, completed: false });
  }

  get completedTodosCount() {
    return this.todos.filter(todo => todo.completed).length;
  }
}
```

#### Computed Values

Example:
```javascript
import { makeObservable, observable, computed } from 'mobx';

class TodoList {
  todos = [];

  constructor() {
    makeObservable(this, {
      todos: observable,
      unfinishedTodoCount: computed
    });
  }

  get unfinishedTodoCount() {
    return this.todos.filter(todo => !todo.finished).length;
  }
}
```

#### MobX-React Integration

Example:
```jsx
import { observer } from 'mobx-react-lite';

const TodoListView = observer(({ todoList }) => (
  <div>
    <ul>
      {todoList.todos.map(todo => (
        <TodoView todo={todo} key={todo.id} />
      ))}
    </ul>
    Tasks left: {todoList.unfinishedTodoCount}
  </div>
));
```

This expanded guide provides a comprehensive overview of React and its ecosystem, including detailed explanations and code examples for each concept. It covers the core React concepts, hooks, routing, and state management solutions like Redux and MobX. This should give you a solid foundation for your interview preparation.