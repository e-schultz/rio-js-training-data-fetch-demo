# Data Fetch Demo - Class Component

Recall, that during the mounting phase of the React Lifecycle, it will invoke

- constructor
- render
- `componentDidMount`

It is a common pratice, and also mentioned in the [React Documentation](https://reactjs.org/docs/react-component.html#componentdidmount) to use the `componentDidMount` hook to fetch data.

For this exercise, we will be building a simple search for HackerNews and listing the results.

The API we will be using to query is:

`https://hn.algolia.com/api/v1/search?query=`

## Exercise One

In the `HackerNewsSearch` component:

- set an initial state property called `results` that is an empty array.
  - _note_ it is common to do `this.state = ....` in the constructor.
- this is the only time it is ok to directly mutate the state,
- any other time - use `this.setState({})`
- implement the `componentDidMount` lifecycle method
  - Use fetch to query Hackers News for `react`,
  - the url will be: `https://hn.algolia.com/api/v1/search?query=react`
- Once fetch resolves
  - update the component state with the results
- Implement the `render` method to display the list of results, see notes on the API response format below.
- The list should display the title - and be a link to the article.
- When rendering a list of components, you should specify a key attribute.
- You can use `objectID` as the value for the key.
  Keys help React identify which items have changed, are added, or are removed. Keys should be given to the elements inside the array to give the elements a stable identity: [React Docs for more details](https://reactjs.org/docs/lists-and-keys.html#keys)

```html
<ul>
    <li><a href="https://code.facebook.com/posts/300798627056246">Relicensing React, Jest, Flow, and Immutable.js<a></li>
</ul>

```

## API Response

The result from the API contains quite a bit of data. The full schema is blow, however the key values we care abbout are the `hits` array, which is the result object.

For this pratice, we only care about:

- title
- url
- objectID

```json
{
  "hits": [
    {
      "title": "Relicensing React, Jest, Flow, and Immutable.js",
      "url": "https://code.facebook.com/posts/300798627056246",
      "objectID": "15316175"
    }
  ],
  "nbHits": 143847,
  "page": 0,
  "nbPages": 50,
  "hitsPerPage": 20,
  "processingTimeMS": 3,
  "exhaustiveNbHits": false,
  "query": "react",
  "params": "advancedSyntax=true\u0026analytics=false\u0026query=react"
}
```

## Full Results Object

```json
{
  "hits": [
    {
      "created_at": "2017-09-22T21:51:56.000Z",
      "title": "Relicensing React, Jest, Flow, and Immutable.js",
      "url": "https://code.facebook.com/posts/300798627056246",
      "author": "dwwoelfel",
      "points": 2280,
      "story_text": null,
      "comment_text": null,
      "num_comments": 498,
      "story_id": null,
      "story_title": null,
      "story_url": null,
      "parent_id": null,
      "created_at_i": 1506117116,
      "relevancy_score": 7675,
      "_tags": ["story", "author_dwwoelfel", "story_15316175"],
      "objectID": "15316175",
      "_highlightResult": {
        "title": {
          "value": "Relicensing \u003cem\u003eReact\u003c/em\u003e, Jest, Flow, and Immutable.js",
          "matchLevel": "full",
          "fullyHighlighted": false,
          "matchedWords": ["react"]
        },
        "url": {
          "value": "https://code.facebook.com/posts/300798627056246",
          "matchLevel": "none",
          "matchedWords": []
        },
        "author": {
          "value": "dwwoelfel",
          "matchLevel": "none",
          "matchedWords": []
        }
      }
    }
  ],
  "nbHits": 143847,
  "page": 0,
  "nbPages": 50,
  "hitsPerPage": 20,
  "processingTimeMS": 3,
  "exhaustiveNbHits": false,
  "query": "react",
  "params": "advancedSyntax=true\u0026analytics=false\u0026query=react"
}
```
