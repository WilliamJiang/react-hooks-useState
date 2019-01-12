useState() Hook Example
========================

Quick Start
------------
```bash
$ cd react-hooks
$ yarn start
$ open locahost:3000
```

Description
-----------
State are an essential part of React. They allow us to declare state variables that hold data that will be used in our app. With class components, state is usually defined like this:

```javascript
class Example extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
  }
}
```          

Before hooks, state was usually only used in a class component but as mentioned above, Hooks allows us to add state to a functional component.

Let's see an example below. Here, we'll be building a switch for a lightbulb SVG, which will change color depending on the value of the state. To do this, we'll be using the useState hook.

Here's the complete code (and runnable example) -- we'll walk through what's going on below.

```javascript
import React, { useState } from "react";
import ReactDOM from "react-dom";

import "./styles.css";

function LightBulb() {
  let [light, setLight] = useState(0);

  const setOff = () => setLight(0);
  const setOn = () => setLight(1);

  let fillColor = light === 1 ? "#ffbb73" : "#000000";

  return (
    <div className="App">
      <div>
        <LightbulbSvg fillColor={fillColor} />
      </div>

      <button onClick={setOff}>Off</button>
      <button onClick={setOn}>On</button>
    </div>
  );
}

function LightbulbSvg(props) {
  return (
    <svg width="56px" 
        height="90px" 
        viewBox="0 0 56 90" 
        version="1.1">
      {/* 
        svg definition truncated, but you 
        can see the whole code example here:
        https://codesandbox.io/s/mpnoljl19?from-embed
        */}
    </svg>
  );
}

const rootElement = document.getElementById("root");
ReactDOM.render(<LightBulb />, rootElement);
```

Our Component is a Function
---------------------------

In the code block above, we start by importing `useState` from react. `useState` is a new way to use the capabilities that this.state would have offered.

Next, notice that this component is a function and not a class. Interesting!

Reading and Writing State
-------------------------

Within this function, we call useState to create a state variable:

```javascript
let [light, setLight] = useState(0);
```

**useState is used to declare a state variable** and can be initialized with any type of value (unlike state in classes, which were required to be an object).

As seen above, we use destructuring on the return value of `useState`.

1. The first value, light in this case, is the current state (sort of like this.state) and
1. The second value is a function used to update the state (first) value (like the traditional this.setState).

Next, we create two functions that each set the state to different values, 0 or 1.

```javascript
const setOff = () => setLight(0);
const setOn = () => setLight(1);
```

We then use these functions as event handlers to the buttons in the view:

```javascript
<button onClick={setOff}>Off</button>
<button onClick={setOn}>On</button>
```

React Tracks the State
----------------------

When the "On" button is pressed, setOn is called, which will call setLight(1). The call to setLight(1) **updates the value of light on the next render**. This can feel a bit magical, but what is happen is that **React is tracking the value of this variable** and it will pass in the new value when it re-renders this component.

Then, we use the current state (light) to determine whether the bulb should be "on" or not. That is, we set the fill color of the SVG depending on the value of light. If light is 0 (off), then the fillColor is set to #000000 (and if it's 1 (on), fillColor is set to #ffbb73).

There are lots of Hooks
-----------------------

The code above covers only the useState hook, but there are many more! In the book, we also cover:

1. useEffect Hook - for causing side-effects
1. useContext Hook - for accessing context (without a class!)
1. useRef Hook - for accessing a Ref
1. How to make your own custom hooks and
1. How to test your hooks
