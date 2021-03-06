Let's add some UX features. We are going to add a navigation bar on top of every page that takes you to the `HomePage` when you click on it no matter where you are.
To do that let's create a new component and let's call it `TopNavBar` then all we need to do is add a `Link` that's going to take us to the `HomePage`, and that's it! it's really that simple, so our `TopNavBar` code will be the following:

```jsx
import React, { Component } from "react";
import { Link } from "react-router-dom";

class TopNavBar extends Component {
  render() {
    return (
      <nav className="navbar navbar-expand-lg navbar-light bg-light mb-3">
        <Link className="navbar-brand" to="/">
          HOME
        </Link>
      </nav>
    );
  }
}

export default TopNavBar;
```

Then let's render our `TopNavBar` in our `App.js` like this:

```jsx
import React from "react";
....

//Components
...
import TopNavBar from "./Components/TopNavBar";

...

function App() {
  return (
    <div>
      <TopNavBar />

      <Switch>
        ...
      </Switch>
    </div>
  );
}

export default App;
```

![navbar](https://i.imgur.com/KfD3jsq.jpg)

So now whenever a user wants to go back to the home page he/she can easily click on the word `HOME` and that's it.

![easy](https://media0.giphy.com/media/3o7btNa0RUYa5E7iiQ/giphy.gif)
