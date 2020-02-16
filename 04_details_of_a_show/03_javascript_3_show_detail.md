Before going back to our `ShowDetail` component to make some changes. There's something that we need to add first. Since our data file is huge, we'll need a loading state which we'll create the following component for and its purpose will be explained later on. Let's create a `Loading` component inside our `src/Components` folder and add the following code to it:

```jsx
import React from "react";
import { FontAwesomeIcon } from "@fortawesome/react-fontawesome";
import { faSpinner } from "@fortawesome/free-solid-svg-icons";

const Loading = () => (
  <div className="spinner mx-auto text-center">
    <FontAwesomeIcon icon={faSpinner} spin size="4x" />
  </div>
);

export default Loading;
```

After making some changes our updated `ShowDetail` component will look like this:

```jsx
import React, { Component } from "react";
import Loading from "./Loading";

class ShowDetail extends Component {
  state = {
    selectedShow: null,
    loading: true
  };

  componentDidMount() {
    this.getShow(this.props.match.params.showID);
  }

  getShow(showID) {
    const show = this.props.shows.find(show => show.id === +showID);
    if (show) {
      this.setState({
        selectedShow: show,
        loading: false
      });
    }
  }

  render() {
    if (this.state.loading) return <Loading />;
    else {
      const show = this.state.selectedShow;
      const showName = show.name;
      return (
        <div className="container-fluid">
          <div className="row">
            <div className="col">
              <h3>{showName}</h3>
              <img
                src={show.image.original}
                className="img-thumbnail img-fluid"
                alt={showName}
              />
            </div>
            <div className="col">
              <h3>Summary:</h3>
              <p>{show.summary}</p>
            </div>
          </div>
        </div>
      );
    }
  }
}

export default ShowDetail;
```

Let's discuss some of the changes that we made:

- We removed the data import because now we are sending the `shows` via props.
- We added a state to hold the value of the `selectedShow` which is the show the user clicks on from the list.
- We added the `getShow` method which is going to get the `selectedShow` from the list of `shows` by iterating through the list of `shows` to find the show that matches the ID in the parameter. Then we set the `selectedShow` state to have the value of the variable `show`.
- In `componentDidMount` we added a call to the `getShow` method and here's where we started to take advantage of our `Router` since it gave us access to the dynamic parameter `showID` that we mentioned in the previous step through `this.props.match.params.showID`. The `react-router-dom` library passes in a prop called `match` into every `Route` that is rendered. Inside this `match` object is another object called `params`. This holds all matching params where the key is the name we specified when creating the route, and the value is the actual value in the URL. Thus, we basically took the value that the `showID` parameter holds and we sent it to the `getShow` method to find the `selectedShow`.
- In the render method we changed the `show` value to take its value from the `selectedShow` state.
- We added a loading state because it might take a while for `getShow` to actually update the state with the `selectedShow`, so in order to prevent an error from popping up, we added a loading state that will render a `Loading` component until the show gets "found".

Now we need to actually update the value of the URL parameter with the correct ID of the show that the user clicks on, but how are we going to do that? Think about it for a while before moving to the next step.

![thinking](https://media2.giphy.com/media/DfSXiR60W9MVq/giphy.gif)
