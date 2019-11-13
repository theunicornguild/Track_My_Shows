So basically what we want to do is when the user clicks on a specific show, we take him to its detail page using something called `<Link>` which is like an HTML anchor tag. If you recall our `ShowCard` component we are going to add the following modifications to it:

```jsx
import React from "react";
import { Link } from "react-router-dom";

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
          <Link className="btn btn-md btn-info" to={`/show/${props.show.id}`}>
            More
          </Link>
        </div>
      </div>
    </div>
  );
}

export default ShowCard;
```

We first imported `Link` from `react-router-dom` and then we simply added the following line of code:

```jsx
...
<Link className="btn btn-md btn-info" to={`/show/${props.show.id}`}>
    More
 </Link>
...
```

`Link` will look through all the `<Route/>` components nested in a `<Switch>` and render the corresponding component. Unlike the `<a href>` element tag, `<Link>` doesn't refresh the page so you don't need to keep making requests every time you're moving between components. In the code above, we are adding a link to the `ShowDetail` page and it takes the show's ID as a URL parameter which is the `showID` variable we mentioned in the previous step, and that is exactly how it will know which show will be displayed in our `ShowDetail` page, so now if you click on the `More` button you added to `ShowCard`, it will take you to the specific detail page of the selected show.

![ShowDetail](https://i.imgur.com/zytcM0y.png)

![yaay](https://media.tenor.com/images/2be8af5edb3dd3d5129a6f3b6bd712fa/tenor.gif)
