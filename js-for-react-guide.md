# JavaScript Fundamentals for React Development

## 1. Variables and Modern Declaration
### let and const
Modern JavaScript uses `let` and `const` instead of `var`. 
- `let` is for variables that will be reassigned
- `const` is for values that won't change

```javascript
let count = 0;  // Can be reassigned
const API_URL = 'https://api.example.com';  // Cannot be reassigned
```

## 2. Arrow Functions
Essential for React components and callbacks.

```javascript
// Traditional function
function add(a, b) {
    return a + b;
}

// Arrow function
const add = (a, b) => a + b;

// Arrow function with single parameter
const double = num => num * 2;

// Arrow function with block body
const greet = name => {
    const greeting = `Hello, ${name}!`;
    return greeting;
};
```

## 3. Template Literals
Used for string interpolation and multiline strings.

```javascript
const name = 'John';
const greeting = `Hello, ${name}!
Welcome to our app.`;
```

## 4. Destructuring
Frequently used in React for props and state.

```javascript
// Object destructuring
const user = { name: 'John', age: 30 };
const { name, age } = user;

// Array destructuring
const colors = ['red', 'blue'];
const [primary, secondary] = colors;

// Function parameter destructuring
const UserComponent = ({ name, age }) => {
    return <div>{name} is {age} years old</div>;
};
```

## 5. Spread and Rest Operators
Essential for immutable state updates and prop passing.

```javascript
// Spread operator (...)
const oldArray = [1, 2, 3];
const newArray = [...oldArray, 4, 5];  // [1, 2, 3, 4, 5]

const oldObject = { name: 'John' };
const newObject = { ...oldObject, age: 30 };  // { name: 'John', age: 30 }

// Rest operator
const sum = (...numbers) => numbers.reduce((total, num) => total + num, 0);
```

## 6. Array Methods
Commonly used in React for rendering lists and managing state.

```javascript
// map
const numbers = [1, 2, 3];
const doubled = numbers.map(num => num * 2);  // [2, 4, 6]

// filter
const filtered = numbers.filter(num => num > 1);  // [2, 3]

// reduce
const sum = numbers.reduce((total, num) => total + num, 0);  // 6

// find
const found = numbers.find(num => num === 2);  // 2
```

## 7. Object Methods
Important for working with state and props.

```javascript
// Object.keys()
const user = { name: 'John', age: 30 };
const keys = Object.keys(user);  // ['name', 'age']

// Object.values()
const values = Object.values(user);  // ['John', 30]

// Object.entries()
const entries = Object.entries(user);  // [['name', 'John'], ['age', 30]]
```

## 8. Optional Chaining
Safely accessing nested properties.

```javascript
const user = {
    details: {
        address: {
            street: 'Main St'
        }
    }
};

// Safe property access
const street = user?.details?.address?.street;  // 'Main St'
const zip = user?.details?.address?.zip;  // undefined
```

## 9. Nullish Coalescing
Setting default values.

```javascript
const value = null;
const defaultValue = value ?? 'default';  // 'default'

const zero = 0;
const result = zero ?? 42;  // 0 (preserves zero)
```

## 10. Promises and Async/Await
Essential for handling API calls and side effects.

```javascript
// Promise
const fetchData = () => {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve({ data: 'Success' });
        }, 1000);
    });
};

// Async/Await
const getData = async () => {
    try {
        const response = await fetchData();
        console.log(response.data);
    } catch (error) {
        console.error(error);
    }
};
```

## 11. Modules
Understanding module system is crucial for React applications.

```javascript
// Exporting
export const helper = () => {
    // helper function
};
export default MainComponent;

// Importing
import MainComponent, { helper } from './components';
```

## 12. Ternary Operators
Commonly used in React for conditional rendering.

```javascript
// Ternary operator
const isLoggedIn = true;
const message = isLoggedIn ? 'Welcome back!' : 'Please log in';

// Conditional rendering in React
const Component = () => {
    return isLoggedIn ? <UserDashboard /> : <LoginForm />;
};
```

## Applying These Concepts in React

Here's a simple React component that combines many of these concepts:

```javascript
import React, { useState, useEffect } from 'react';

const UserProfile = ({ userId }) => {
    const [user, setUser] = useState(null);
    const [loading, setLoading] = useState(true);

    useEffect(() => {
        const fetchUser = async () => {
            try {
                const response = await fetch(`/api/users/${userId}`);
                const data = await response.json();
                setUser(data);
            } catch (error) {
                console.error(error);
            } finally {
                setLoading(false);
            }
        };

        fetchUser();
    }, [userId]);

    if (loading) return <div>Loading...</div>;

    const { name, email, preferences = {} } = user ?? {};

    return (
        <div>
            <h2>{name}</h2>
            <p>{email}</p>
            {preferences?.notifications && (
                <div>Notifications: {preferences.notifications ? 'On' : 'Off'}</div>
            )}
        </div>
    );
};

export default UserProfile;
```

This example demonstrates:
- Arrow functions
- Destructuring
- Optional chaining
- Nullish coalescing
- Async/await
- Modern array methods
- Conditional rendering
- Module exports

## Best Practices
1. Always use `const` unless you need to reassign values
2. Prefer arrow functions for consistency
3. Use destructuring for cleaner code
4. Keep functions pure when possible
5. Use modern array methods instead of loops
6. Handle null/undefined values safely
7. Use async/await for cleaner asynchronous code

Understanding these JavaScript fundamentals will make learning and working with React much easier and more efficient.
