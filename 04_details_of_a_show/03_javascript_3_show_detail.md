//Add loading state/component for ShowDetail otherwise it will throw an error


Let's go back to our `ShowDetail` component to make some changes. Our updated component will look like this:

```jsx
import React, { Component } from "react";

class ShowDetail extends Component {
  state = {
    selectedShow: null
  };

  componentDidMount() {
    this.getShow(this.props.match.params.showID);
  }

  getShow(showID) {
    const show = this.props.shows.find(show => show.id === +showID);
    if (show) {
      this.setState({
        selectedShow: show
      });
    }
  }

  render() {
    const show = this.state.selectedShow;
    const showName = `${show.name}`;
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

export default ShowDetail;
```

Let's discuss some of the changes that we made:

- We removed the data import because now we are sending the `shows` via props.
- We added a state to hold the value of the `selectedShow` which is the show the user clicks on from the list.
- We added the `getShow` method which is going to get the `selectedShow` from the list of `shows` by iterating through the list of `shows` to find the show that matches the ID in the parameter. Then we set the `selectedShow` state to have the value of the variable `show`.
- In `componentDidMount` we added a call to the `getShow` method and here's where we started to take advantage of our `Router` since it gave us access to the dynamic parameter `showID` that we mentioned in the previous step through `this.props.match.params.showID`. The `react-router-dom` library passes in a prop called `match` into every `Route` that is rendered. Inside this `match` object is another object called `params`. This holds all matching params where the key is the name we specified when creating the route, and the value is the actual value in the URL. Thus, we basically took the value that the `showID` parameter holds and we sent it to the `getShow` method to find the `selectedShow`.
- In the render method we changed the `show` value to take its value from the `selectedShow` state.

Now we need to actually update the value of the URL parameter with the correct ID of the show that the user clicks on, but how are we going to do that? Think about it for a while before moving to the next step.

![thinking](https://media2.giphy.com/media/DfSXiR60W9MVq/giphy.gif)
