Our list component will render our list of shows which were sent from our `HomePage` through `props`. Let's call this component ShowsList and add it to our Components folder `src/Components/ShowsList.js`.

Before writing our `ShowsList` component let's add a tiny card component that's going to render a single show card, so let's call it `ShowCard` and it will look like this:

```jsx
import React from "react";

function ShowCard(props) {
  return (
    <div className="col-lg-4 col-md-6 col-12">
      <div className="card">
        <img
          src={props.show.image.original}
          className="card-img-top"
          alt="..."
        />
        <div className="card-body">
          <h5 className="card-title">{props.show.name}</h5>
          <p className="card-text">{props.show.summary}</p>
        </div>
      </div>
    </div>
  );
}

export default ShowCard;
```

This component simply receives a single show object sent via props from `ShowsList` and renders its content inside a bootstrap styled card.

Back to our `ShowsList` component, this is how it's going to look like:

```jsx
import React from "react";

//Components
import ShowCard from "./ShowCard";

function ShowsList(props) {
  let showCards = props.shows.map(show => (
    <ShowCard show={show} key={show.id} />
  ));
  return <div className="row">{showCards}</div>;
}

export default ShowsList;
```

Basically, our `ShowsList` takes a list of shows imported from our data file `shows` and it maps through them to convert each object into a card. Finally, the list of cards will be rendered on the page. Your list page should look like this:

![ShowsList](https://imgur.com/a/HwJRdHY)
