Before jumping to the list page let's create a landing page that's going to render the list page. In this project we are going to use Bootstrap a lot to style our components, so let's install it using the following command:

```shell
$ yarn add bootstrap
```

Now let's move to the interesting part. First, let's create a new folder called `Components` inside our `src` folder `src/Components`. This step in not necessary but it's good practice and it makes it easier for you to find your files later. Inside your newly created Components folder let's create our new component which is our landing page, and let's call it `HomePage`. So the current foldering structure looks like this `src/Components/HomePage.js`.

Our `HomePage` component is going to look like this:

```jsx
import React, { Component } from "react";
import ShowsList from "./ShowsList";

//Data
import shows from "../Data/shows";

class HomePage extends Component {
  render() {
    return (
      <div className="container-responsive">
        <div className="col-12">
          <ShowsList shows={shows} />
        </div>
      </div>
    );
  }
}

export default HomePage;
```

There's not much going on in here, so basically `HomePage` is going to get the list of shows from the `shows` file that we created when we `setup` our project and it's going to send it to `ShowsList` component which we will create in the next step.
