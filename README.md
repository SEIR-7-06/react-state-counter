# React State

<br>

## Learning Objectives

- Understand how state is used to manage a component that changes over time
- Set up state for a component

<br>

## What is State
---

<br>

State is a concept we are actually already familiar with.

You may hear someone refer to "the state of the country" or the "state of affairs". Or perhaps the "state of my bedroom". Any of these things could be in many different states. If we were to describe the state of a bedroom we could say that the bedroom is clean or the bedroom is messy. The key is that the bedroom will not stay in one particular state and will change over time.

### State in React

**_We use state in our React components to handle information that will change over time._**

State is simply a JavaScript object for storing this information.

If we think about a dropdown navigation on a website, we know that sometimes the dropdown navigation will be open, and sometimes it will be closed. The important thing that we know that this will change over time. For this reason we want to store this information in state.

It may look something like this, indicating that the navigation is open.

```js
state = {
  navIsOpen: true
}
```

If we think about an input field for a form, the input could be empty, or it could have text typed into it. But we do know that the value will change, so we want to use state to keep track of that value.

It might look something like this.

```js
state = {
  inputValue: 'type text in here...'
}
```

The best way to really understand this concept is to build a React app that uses state. Let's get started.

<br>

## Code Along: Build a Counter App
---

<br>

To illustrate how state works in React we will be building a simple counter app that will look like this.

![counter app](./images/counter-app.png)

The app will allow us to increase or decrease a number by clicking buttons. If we click "Decrement" we want to see the count go down. If we click "Increment" we want to see the count go up.

Take a moment to think about what information in our app will change over time. And what values will we want to store in our state object.

<br>

## Set Up
---

<br>

Let's start by setting up a React app with the command line tool, Create React App.

```bash
npx create-react-app counter-app
```

Now we can start the server and view our application at `localhost:3000`
```bash
npm start
```

<br/>

---

<br/>

We'll start by removing the boilerplate code in `App.js` and replace it with our own code. `App.js` should look something like this, although feel free to make it your own.

```js
import './App.css';

function App() {
  return (
    <div className="App">
      <h1>React Counter</h1>
    </div>
  );
}

export default App;
```

We should now see our changes automatically update in the browser. _The Create React App server can be buggy, and from time to time you may have to manually refresh the browser to see your changes._

<br/>

## Class Components

---
<br/>

So far we have been defining all of our components as functions. These functions take in **props** as parameters and return **JSX**.

Another way to define a component is using a JavaScript **class**. Using a class will allow us add **state** to our component.

We'll start by importing the **React** library into `App.js` at the top of the file.

```js
import React from 'react';
```

We'll now convert our **functional component** into a **classed-based component**. It will look something like this. Let's type it out and then we'll talk about what is going on.

```js
import React from 'react';
import './App.css';

class App extends React.Component {

  render() {
    return (
      <div className="App">
        <h1>React Counter</h1>
      </div>
    );
  }

}

export default App;
```

Here are the changes we've made.

- We've replaced the `function` keyword with the `class` keyword followed by the name of our component. In this example we defined an `App` class that extends `React.Component` and in doing so we just defined an App component.
- We've added a `render` method to our class and include our return statement inside of the `render` method.
- Double check all of your parentheses and curly braces and make sure they are in the right place.
- When this component is rendered, the `render` function willed be called returning the **JSX** and rendering it to the page.

If you save your file and go back to your browser, you should see the App component rendering to the page exactly as before!

<br/>

## Add the UI Elements

---
<br/>

Now we'll go ahead and add the UI elements to make our app interactive. Let's add the count and the two buttons into the return statement of the `render` method.

It will look like this.

```js
import React from 'react';
import './App.css';

class App extends React.Component {

  render() {
    return (
      <div className="App">
        <h1>React Counter</h1>

        <p>Count: 0</p>

        <button>Decrement -</button>
        
        <button>Increment +</button>
      </div>
    );
  }
}

export default App;
```

Save the file, and we should see our UI updates in the browser!

The buttons wont do anything yet, but we get a sense of what our app is supposed to do. If we click the "Decrement" button, we want to see the count decrease by 1 on the page. If we click the "Increment" button, we want to see the count increase by 1 on the page.

<br>

## Adding State
---

<br>

We know that the count will change over time. For this reason we want to store this value in state.

To add state to our component, we'll add an instance property to our class called `state` and we'll set `state` to an object. It will look like this.

```js
...

class App extends React.Component {

  state = {}

  render() {
    return (
      <div className="App">
        <h1>React Counter</h1>

        <p>Count: 0</p>

        <button>Decrement -</button>
        
        <button>Increment +</button>
      </div>
    );
  }
}

...
```

React is expecting this property to specifically be called `state` and we aren't allowed to use another variable name in this case.

<br>

## Storing Values in State
---

Now let's store the count in state. Create a property in the state object called count and set it's value to zero.

```js
...

class App extends React.Component {

  state = {
    count: 0
  }

  render() {
    return (
      <div className="App">
        <h1>React Counter</h1>

        <p>Count: 0</p>

        <button>Decrement -</button>
        
        <button>Increment +</button>
      </div>
    );
  }
}

...
```

State is simply an object that stores all of the information about our component that we know will change over time.

<br>

## Referencing State

At the moment our count in our **JSX** is hard-coded to zero and it doesn't yet have to ability to change. Instead of hard-coding a value we'll reference the count property from state.

In our **JSX**, we'll change `Count: 0` to `Count: {this.state.count}`.

```js
...

class App extends React.Component {

  state = {
    count: 0
  }

  render() {
    return (
      <div className="App">
        <h1>React Counter</h1>

        <p>Count: {this.state.count}</p>

        <button>Decrement -</button>
        
        <button>Increment +</button>
      </div>
    );
  }
}

...
```

Anytime we want to insert JavaScript into **JSX** we'll use the curly brace syntax `{}` and insert our JavaScript inbetween the two tags.

In this case we're referencing the `count` property in our `state` object.

### Why Do We Use "this"

Think back to our lesson on object oriented programming. We used classes as blueprints to create many instances of a certain type of object. Whenever we wanted to reference properties on the instance of a class we used `this` to reference the instance. When an App component get's created we are creating an instance of the `App` class

**Note:** _The key idea here is, when we want something to change on the page we update state and then React will automatically update our UI for us._



===============================================================

TODO: Include hungry for more on state w/React Hooks
