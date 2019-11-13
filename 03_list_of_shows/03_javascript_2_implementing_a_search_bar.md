To make our project more user friendly let's implement a search bar for our list of shows. In order to do that we need to create a new component and let's call it `SearchBar`. It will be inside our components folder `src/Components/SearchBar`.
Before starting to write the code let's install some required packages for FontAwesome. FontAwesome is a font and icon toolkit based on CSS and LESS. In order to start using it we need to install the following packages:

```shell
$ yarn add @fortawesome/fontawesome-svg-core
$ yarn add @fortawesome/free-solid-svg-icons
$ yarn add @fortawesome/react-fontawesome
```

Now let's begin to write our `SearchBar` component. Initially our component will look like this:

```jsx
import React, { Component } from "react";
import { FontAwesomeIcon } from "@fortawesome/react-fontawesome";
import { faSearch } from "@fortawesome/free-solid-svg-icons";

class SearchBar extends Component {
  state = { query: "" };

  handleChange = event => {
    this.setState({ query: event.target.value });
  };

  render() {
    return (
      <div className="form-group col-lg-6 col-12 mx-auto">
        <div className="input-group my-3">
          <input
            className="form-control"
            type="text"
            value={this.state.query}
            onChange={this.handleChange}
          />
          <div className="input-group-append">
            <span className="input-group-text">
              <FontAwesomeIcon icon={faSearch} />
            </span>
          </div>
        </div>
      </div>
    );
  }
}

export default SearchBar;
```

Take some time, let it sink in, and try to understand what's happening in the code before moving to the next step.

![waiting](https://media1.tenor.com/images/da7d905afc93a70b640406c5949e1021/tenor.gif?itemid=9562336)

Okay, so far our `SearchBar` simply takes whatever the user types in the input field and sets it as the state's `query` value through the `OnChange` attribute and the `handleChange` method. Now we need to actually display our `SearchBar` inside our `HomePage`, soooo what do you think the next step is?

![thinking](https://media1.giphy.com/media/MsWnkCVSXz73i/giphy.gif)

Correct! We need to import the `SearchBar` into the `HomePage` and render it near the top of the page like this:

```jsx
...
import SearchBar from "./SearchBar";

class HomePage extends Component {
...
        <div className="col-12">
          <SearchBar />
          <ShowsList shows={shows} />
        </div>
...
export default HomePage;
```

Now we have our `SearchBar` displayed on the page, but it's not really doing anything. We need to build its functionality, so that it filters the list of shows, and we'll do that in the next step, so for now just take your time and think about how we're going to implement that.

![think](https://thumbs.gfycat.com/DismalMixedCheetah-small.gif)
