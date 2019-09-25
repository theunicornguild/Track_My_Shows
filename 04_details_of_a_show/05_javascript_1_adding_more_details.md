So far our `ShowDetail` only "shows" lol a summary of the show, but we'd want our detail page to actually show specific details, so in the following steps we are going to add a list of seasons inside the detail page and also when you click on a specific season you should see the list of episodes. Similarly, when you click on an episode you should move to its detail page to see its details.
First, let's create 2 components called `Seasons` and `SeasonRow` inside our `Components` folder.
Then for styling purposes let's install `react-bootstrap` using the following command:

```bash
$ yarn add react-bootstrap
```

Inside our `ShowDetail` component we are going to render `Seasons` and send the show's seasons as props to it like this:

```jsx
...
//Components
import Seasons from "./Seasons";

class ShowDetail extends Component {
...
  render() {
    const show = this.state.selectedShow;
    const showName = `${show.name}`;
    return (
...
          <div className="col">
            <h3>Summary:</h3>
            <p>{show.summary}</p>
            <h3>Seasons:</h3>
            <Seasons seasons={show.seasons} />
          </div>
        </div>
      </div>
    );
  }
}

export default ShowDetail;
```

Then in our `Seasons` component we will map through the seasons and send each season as a prop to `SeasonRow` like this:

```jsx
import React from "react";
import { Accordion } from "react-bootstrap";

//Components
import SeasonRow from "./SeasonRow";

function Seasons(props) {
  let rows = props.seasons.map((season, i) => (
    <SeasonRow season={season} key={season[0].id} id={i} />
  ));
  return <Accordion>{rows}</Accordion>;
}

export default Seasons;
```

You may not be familiar with `Accordions`, so what they basically do is restrict Card components to only open one at a time. You'll also notice that we are sending and an `id` as a prop, and you'll know why when we write our `SeasonRow` component next.
Our `SeasonRow` will look like this:

```jsx
import React from "react";
import { Accordion, Card, Button } from "react-bootstrap";

function SeasonRow(props) {
  return (
    <Card>
      <Card.Header>
        <Accordion.Toggle as={Button} variant="link" eventKey={props.id}>
          Season {props.season[0].season}
        </Accordion.Toggle>
        <span className="float-right">{props.season.length} Episodes</span>
      </Card.Header>
      <Accordion.Collapse eventKey={props.id}>
        <Card.Body>"episodes"</Card.Body>
      </Accordion.Collapse>
    </Card>
  );
}

export default SeasonRow;
```

Let's explain a few things:
`AccordionToggle` provides a button that switches between each `AccordionCollapse` component, and for each `AccordionCollapse` component you need an `eventKey` to distinguish between them which is why we sent an `id` that was mentioned earlier.
**_Note_**:`props.season` is actually an array of episodes, and each episode has a key called `season` which gives us the season's number that this episode belongs to. I know the way these data were named is kind of confusing lol. This is what happens when you don't create the data yourself lol.
Okay moving on, so far in our card body we have the word "hello" in it, but in the next steps we are going to display the actual episodes of each season. Our `ShowDetail` currently should look like this:

![showDetail](https://i.imgur.com/J8NvN0n.png)
