Alright now that our `SearchBar` is displayed on the page, let's make it functional. Basically, we want to filter our shows based on what the user types in the input field, so we need to create a function that does exactly that. We'll add this function to our `HomePage` component because it's where we imported our `shows` data. After adding the new functionality our `HomePage` component will look like this:

```jsx
import React, { Component } from "react";
import ShowsList from "./ShowsList";
import SearchBar from "./SearchBar";

//Data
import shows from "../Data/shows";

class HomePage extends Component {
  state = {
    filteredShows: shows
  };

  filterShows = query => {
    query = query.toLowerCase();
    let filteredShows = shows.filter(show => {
      return `${show.name}`.toLowerCase().includes(query.toLowerCase());
    });
    this.setState({ filteredShows: filteredShows });
  };

  render() {
    return (
      <div className="container-responsive">
        <div className="col-12">
          <SearchBar filterShows={this.filterShows} />
          <ShowsList filteredShows={this.state.filteredShows} />
        </div>
      </div>
    );
  }
}

export default HomePage;
```

Take your time first to understand what's happening in the code before reading its explanation.

![waiting](https://media.tenor.com/images/a48310348e788561dc238b6db1451264/tenor.gif)

Alright, so there are a few new things added/changed in the code which are:

- changed the state
- added the `filterShows` method
- sent `filterShows` as props to `SearchBar`
- changed the props that were sent to `ShowsList`

Let's start with the state: as you've probably have noticed we changed the name of `shows` in the state to `filteredShows` because we're going to filter them.

![duh](https://media.tenor.com/images/0fb5d4079ea1c2232c5f73ed263b06e7/tenor.gif)

And because we changed the name in the state we need to change it inside the prop that's being sent to `ShowsList`. Before we were sending `this.state.shows` now we'll send `this.state.filteredShows`. We also need to change the name of the props in `ShowsList.js` component from `shows` to `filteredShows` like this:

```jsx
import React from "react";

//Components
import ShowCard from "./ShowCard";

function ShowsList({ filteredShows }) {
  let showCards = filteredShows.map(show => (
    <ShowCard show={show} key={show.id} />
  ));
  return <div className="row">{showCards}</div>;
}

export default ShowsList;
```

Moving on, another important addition to the code is `filterShows` which is simply the method that's going to make our `SearchBar` work. Basically, it takes a `query` as a parameter and filters the list of shows based on that `query`. If the show's name includes the `query` it adds it to the returned list of shows variable called `filteredShows` then we set this variable's value to `filteredShows` in the state. Finally, we send the `filterShows` method as a prop to our `SearchBar` because we're going to use it there.

In our `SearchBar` component we are going to add the following:

```jsx
class SearchBar extends Component {
  state = { query: "" };

  handleChange = event => {
    this.setState({ query: event.target.value });
    this.props.filterShows(event.target.value); //call filterShows
  };
...
export default SearchBar;
```

There's nothing much here, we just added a function call to `filterShows` inside `handleChange` and we sent the `query` as an argument. That's pretty much it, now if you try to type something in the search bar it should filter what you see in the list page based on your input. Try it out and don't forget to push your code to github when you're done, and move the card from `Backlog` to `Done`.

![yaaay](https://media1.tenor.com/images/05a7505c225710ad1b77bc4caf7cd0bf/tenor.gif?itemid=5370842)
