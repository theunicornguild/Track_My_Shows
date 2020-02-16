Our list component will render our list of shows which were sent from our `HomePage` through `props`. Let's call this component ShowsList and add it to our Components folder `src/Components/ShowsList.js`.

Before writing our `ShowsList` component let's add a tiny card component that's going to render a single show card, so let's call it `ShowCard` and it will look like this:

```jsx
import React from "react";

function ShowCard({ show }) {
  return (
    <div className="col-lg-4 col-md-6 col-12">
      <div className="card">
        <img src={show.image.original} className="card-img-top" alt="..." />
        <div className="card-body">
          <h5 className="card-title">{show.name}</h5>
          <p className="card-text">{show.summary}</p>
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

function ShowsList({ shows }) {
  let showCards = shows.map(show => <ShowCard show={show} key={show.id} />);
  return <div className="row">{showCards}</div>;
}

export default ShowsList;
```

Basically, our `ShowsList` takes a list of shows imported from our data file `shows` and it maps through them to convert each object into a card. Now, that we have our `ShowsList`, you can go back to the `HomePage` and uncomment the code that renders it. Finally, the list of cards will be rendered on the page. By now, your list page should look something like this:

![ShowsList](https://i.imgur.com/42rPa4s.png)

Now you have your list page, so you can move the card from `Doing` to `Done` and explore the list of shows you just built then git add, commit, and push your code.
