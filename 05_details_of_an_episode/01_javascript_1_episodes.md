Let's move to the fourth feature. To be able to display the episodes of each season first let's create an `Episodes` component and an `EpisodeDetail` component as well which is very similar to the `ShowDetail` component we created before.
Our `Episodes` component will look like this:

```jsx
import React from "react";
import { Table } from "react-bootstrap";
import { Link } from "react-router-dom";

function Episodes(props) {
  let episodesRows = props.episodes.map((episode, i) => (
    <tr key={episode.id}>
      <td>
        <Link to={`/episode/${episode.id}`}>{`Episode ${++i}: ${
          episode.name
        }`}</Link>
      </td>
    </tr>
  ));
  return (
    <Table hover>
      <tbody>{episodesRows}</tbody>
    </Table>
  );
}

export default Episodes;
```

There's nothing much going on in this component as you can see we are just mapping through the episodes that were sent through props and displaying each one as a `Link` that takes us to the specific episode's detail page when we click on it.
In order for that to work we need to create our `EpisodeDetail` page which will look like this:

//Add loading state/component to EpisodeDetail

```jsx
import React, { Component } from "react";

class EpisodeDetail extends Component {
  state = {
    selectedEpisode: null
  };

  componentDidMount() {
    this.getEpisode(this.props.match.params.episodeID);
  }

  getEpisode(episodeID) {
    const episode = this.props.episodes.find(
      episode => episode.id === +episodeID
    );
    if (episode) {
      this.setState({
        selectedEpisode: episode
      });
    }
  }

  render() {
    const episode = this.state.selectedEpisode;
    const episodeName = `${episode.name}`;
    return (
      <div className="container-fluid">
        <div className="row">
          <div className="col">
            <h3>{episodeName}</h3>
            <img
              src={episode.image.original}
              className="img-thumbnail img-fluid"
              alt={episodeName}
            />
          </div>
          <div className="col">
            <h3>Summary:</h3>
            <p>{episode.summary}</p>
            <h5>Season: {episode.season}</h5>
          </div>
        </div>
      </div>
    );
  }
}

export default EpisodeDetail;
```

Let's discuss what's happening in the code:

- We added a state to hold the value of the `selectedEpisode` which is the episode the user clicks on from the list.
- We added the `getEpisode` method which is going to get the `selectedEpisode` from the list of `episodes` by iterating through the list of `episodes` to find the episode that matches the ID in the parameter. Then we set the `selectedEpisode` state to have the value of `episode`.
- In `componentDidMount` we added a call to the `getEpisode` method and here's where we started to take advantage of our `Router` since it gave us access to the dynamic parameter `episodeID` through `this.props.match.params.episodeID`. The `react-router-dom` library passes in a prop called `match` into every `Route` that is rendered. Inside this match object is another object called `params`. This holds all matching params where the key is the name we specified when creating the route, and the value is the actual value in the URL. Thus, we basically took the value that the `episodeID` parameter holds and we sent it to the `getEpisode` method to find the `selectedEpisode`.

The value of the URL parameter gets updated with the correct ID of the episode that the user clicks on using the `Link` component we mentioned earlier.

Let's not forget to update our `App` with the new `Route` for the `EpisodeDetail` component like this:


```jsx
...
import EpisodeDetail from "./Components/EpisodeDetail";

//Data
...
import episodes from "./Data/episodes";

function App() {
  return (
    <div>
      <Switch>
...
        <Route
          path="/episode/:episodeID"
          render={props => <EpisodeDetail {...props} episodes={episodes} />}
        />
        <Redirect to="/" />
      </Switch>
    </div>
  );
}

export default App;
```

And the final step is to update the `SeasonRow` component to render the `Episodes` component instead of the word "hello" like this:

```jsx
import React from "react";
import { Accordion, Card, Button } from "react-bootstrap";

//Components
import Episodes from "./Episodes";

function SeasonRow(props) {
  return (
...
      <Accordion.Collapse eventKey={props.id}>
        <Card.Body>
            <Episodes episodes={props.season} />
        </Card.Body>
      </Accordion.Collapse>
    </Card>
  );
}

export default SeasonRow;
```

And there you have it! Now our show detail has all the information you need.

![yaay](https://media3.giphy.com/media/3ov9k7AbzUYmckXSQE/giphy.gif)
