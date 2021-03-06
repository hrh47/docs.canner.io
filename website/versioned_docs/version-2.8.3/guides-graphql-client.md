---
id: version-2.8.3-guides-graphql-client
title: GraphQL Client
sidebar_label: GraphQL Client
original_id: guides-graphql-client
---

`GraphqlClient` let you connect your own GraphQL server with Canner, just new a `GraphqlClient` instance and put it into the `<root>` tag. 

> ***Note that, your GraphQL **must** follow [openCRUD](https://github.com/opencrud/opencrud)***

## Usage

**canner.schema.js**
```js
import CannerScript from 'canner-script';
import {GraphqlClient} from 'canner-graphql-interface';

const graphqlClient = new GraphqlClient({
  uri: "http://localhost:4000/graphql",
  credentials: "same-origin"
});

export default () => (
  <root graphqlClient={graphqlClient}>
    {/* ... your schema */}
  </root>
)
```

## Available Arguements

```
{
  uri: string,
  headers?: any,
  fetch?: any,
  includeExtensions?: boolean,
  credentials?: string,
  fetchOptions?: any,
  useGETForQueries?: boolean
}
```

