So far we have our list page where we can see our list of shows, but what if we wanted to see the details of a specific show? That's our third `Backlog` card "you know what to do now :D".

As a user I want to be able to click on a specific show to read more information about it. In order for us to provide this for our users, we need to create a `ShowDetail` component and add it to our components folder `src/Components/ShowDetail.js`. Initially, our `ShowDetail` will look like this:

```jsx
import React, { Component } from "react";

//Data
import shows from "../Data/shows";

class ShowDetail extends Component {
  render() {
    const show = shows[0];
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

If we render this component we are going to get the details of the first show in the list of shows which makes it static. Now we need to think how are we going to make it dynamic so that we get the show that the user clicks on? What information do we need to have, and most importantly how are we going to move him from one page to another?
The answer to all these questions comes with something called `React Router` which is the exciting topic we are going to discuss/use in the next step.

![excited](https://66.media.tumblr.com/tumblr_mc3hg5VpQP1qcy0p7o1_400.gif)
