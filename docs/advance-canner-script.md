---
id: advance-canner-script
title: About canner-script (JSX for Canner)
sidebar_label: canner-script
---
## Why

`canner-script` is a sugar syntax of Canner CMS schema. In order to, make Canner's developers declare schema in a declarative and intuitive way.

```js
// jsx
<root>
  <object keyName="info">
    <string keyName="name">
  </object>
</root>
```

is equivalent to 

```js
// schema in JSON
{
  info: {
    type: 'object',
    items: {
      name: {
        type: 'string',
      }
    }
  }
}
```

## How

We use `babel` with the `bable-plugin-transform-react-jsx` plugin to parse `jsx` syntax. Choose the `canner-script` as the builder of `jsx` by adding these two lines at the beginning of `canner.schema.js`. ***This is required***.

```js
/** @jsx c */
import c from 'canner-script';
```

***Input***
> NOTE: The comment on the top, it declares `canner-script` as the builder of react, and is **required**.

```jsx
/** @jsx c */
import c from 'canner-script';

modules.export = (
  <root>
    <object keyName="info">
      <string keyName="name">
    </object>
  </root>
);
```

***Output***

```jsx
c('root', null, 
  c('object', {name: 'info'}, 
    c('string', {name: 'name'})
  )
)

// canner-script will internally create a schema object with visitors as below:
{
  schema: info: {
    name: 'info',
    type: 'object',
    items: {
      name: {
        name: 'name',
        type: 'string'
      }
    }
  },
  visitors: []
}
```

## Valid schema syntax

### JSX Tags
There are serveral available tags, as listed below.

***Types***: Represents the data types of the data:

- string
- boolean
- number
- date
- mapPoint
- file
- relation
- array
- object

***Layout***: Layout of CMS blocks and appearance

- Collapse
- Block

***Query and miscellaneous***:

- root (Outermost tag, the root)
- toolbar
  - sort
  - filter
  - pagination


### Wrapped in &lt;root/&gt;

The jsx schema **must** be wrapped in the `root` tag. `root` will return object with two keys, `schema` and `visitors`. `schema` contains the data structure and `visitors` contains the inputs for our `compiler` to build the complete `componentTree`.


***Incorrect***

```jsx
module.exports = (
  <object keyName="test">
    {
      /* other schema */
    }
  </object>
);

// which means
// {
//   type: 'object',
//   name: 'test',
//   items: ...
// }
```

***Correct***
```jsx
module.exports = (
  <root>
    <object keyName="test">
      {
        /* other schema */
      }
    </object>
  </root>
);

// which means
// {
//   schema: {
//     test: {
//       type: 'object',
//       name: 'test',
//       items: ...
//     }
//   },
//   visitors: []
// }
```

### Type tags

Type tags are the most basic UI component for CMS.  For example you could create a editor for string.

Using editor UI:

```js
<string ui="editor">
```

Every UI component should pass a keyName, which matchs to the key name of your data source.

For example, your data is like below

```js
{
  content: "This is your content"
}
```

So your `keyName` should define as `content`

```js
<string ui="editor" keyName="content">
```

> Further information
> - [Antd CMS components docs](https://canner.github.io/antd-cms-component-docs)
> - [API of CMS components](api-components.md) 

### Layout tags

Layout tags is use to create grids, containers, and blocks in CMS. This allows your CMS to create customized design layouts for customized visual design.

Every layout tag will generate a new `visitor` that is inserted into the `visitors` array, which will be collected in `root` tag.

For example, there are three fields `name`, `nickname`, and `note` in the `info` object, and we can use `block` tag to seperate the three fields into two different blocks.

***without block***
```jsx
/** @jsx c */
import c from 'canner-script';

module.exports = <root>
  <object keyName="info">
    <string keyName="name" />
    <string keyName="nickname" />
    <string keyName="note" ui="editor"/>
  </object>
</root>
```

***with block***
```jsx
/** @jsx c */
import c, {Block} from 'canner-script';

module.exports = <root>
  <object keyName="info">
    <Block>
      <string keyName="name" />
      <string keyName="nickname" />
    </Block>
    <Block>
      <string keyName="note"  ui="editor"/>
    </Block>
  </object>
</root>
```

> Further information
> - [Advance layout introduction](advance-layout.md)  
