`React Router` is a react library that allows us to simulate moving between pages, but in reality it changes the components that we're rendering based on what's in our URL bar. So, we are basically tricking the user into believing that he is moving from one page to another while the only thing that's changing is actually the components being rendered.

`React Router` provides us with components that we can use to "navigate" the user to different parts of our project like: `<Switch>`, `<Route>`, `<Link>` etc.
First, let's begin with setting up our router, and in order to do that we need to install the following packages:

```shell
$ yarn add react-router
$ yarn add react-router-dom
```

Then in our `src/index.js` we need to add the following:

```jsx
...
import { BrowserRouter } from 'react-router-dom';
...
ReactDOM.render((
  <BrowserRouter>
    <App/>
  </BrowserRouter>
), document.getElementById('root'))
```

As you probably already know `<App>` is where we're rendering all our components. Moreover, `<BrowserRouter>` is what we need to wrap our `<App>` component with in order to allow our application to render a component based on the URL, and it gives us access to the `history` prop which can be used to call functions to navigate between `routes`.

In the previous step, we created our `ShowDetail` page and in order for us to display this page we'll need to render it in our `src/App`, but if you recall we are currently rendering our `HomePage` there, so this leaves us with 2 options we either remove the `HomePage` and render `ShowDetail` instead or we render both at the same time which is going to be messy and doesn't make sense. This is where `React Router` comes in handy. We can specify which component we want to render based on the URL, so let's do that by adding a route to our `HomePage` like this:

```jsx
import React from "react";
import { Route } from "react-router-dom";

//Components
import HomePage from "./Components/HomePage";

function App() {
  return (
    <div>
      <Route path="/" component={HomePage} />
    </div>
  );
}

export default App;
```

- `<Route/>`: is the main component that defines which URL displays our component.
- `path`: is where we can assign the URL names we want to use.
- `component`: is where we can assign which component we want to display with the given URL.

We can also add another `Route` for our `ShowDetail`, but before we do that let's add a `Switch` to wrap our `Routes` with it because if we don't use a `Switch` every component that matches the URL will be rendered on the page for example: a component with this URL `/home` and another one with this URL `/home/shows` both of them will be rendered because a part of their URLs matches the path of the `Route`, so a solution to that is adding a `Switch` then we can add our second `Route`, and now our `App` will look like this:

```jsx
import React from "react";
import { Switch, Route, Redirect } from "react-router-dom";

//Components
import ShowDetail from "./Components/ShowDetail";
import HomePage from "./Components/HomePage";

//Data
import shows from "./Data/shows";

function App() {
  return (
    <div>
      <Switch>
        <Route exact path="/" component={HomePage} />
        <Route
          path="/show/:showID"
          render={props => <ShowDetail {...props} shows={shows} />}
        />
        <Redirect to="/" />
      </Switch>
    </div>
  );
}

export default App;
```

You will notice a few new things that were added:

- `<Switch>`: as we mentioned before, `<Switch>` renders the first child `<Route>` that matches the URL only. Without it, all components that include similar paths will render because they all match a part of the path.
- `exact`: is a keyword that specifies that the URL should be exactly the same as what's written in the URL bar.
- `render`: is a prop that takes in an anonymous function that will return jsx elements or usually another component. We use it when we want to send props to the component being rendered, and as shown in the code above we are sending `shows` as a prop to our `ShowDetail` component.
- `{...props}`: the `...` notation is used to spread the keys and values of an object. That way we can pass extra props to our component without worrying about overriding important props.
- `/:showID`: the `:` means that it's a dynamic parameter so it's part of the path URL. We will explain more about url parameters later on, and you'll understand why we need them.
- `<Redirect/>`: is usually used to redirect the user to another component based on some conditions. The way we put it in our code ensures that if the URL in the URL bar doesn't match any of the defined `Routes`, the code will automatically go to the `<Route path="/" .../>`.

Now that our `Router` is ready, let's see how we are going to use it to render our `ShowDetail` page in the next step.
