---
id: file-canner-schema-js
title: canner.schema.js
sidebar_label: canner.schema.js
---

`canner.schema.js` is the file describing the schema of your data, it's writed with `jsx` language which is just like html tag and easy to learn.

> Learn more about [Canner Schema](http://framework.canner.io/docs/guides-writing-schema.html)

**canner.schema.js**

> NOTE: you'will need to install `cannner-script`, know more about [Canner Script](http://framework.canner.io/docs/advance-canner-script.html)

```js
/** @jsx */
import c from 'canner-script';

export default (
  <root>
    <object keyName="info">
      <string keyName="name" />
    </object>
    <array keyName="posts" uiParams={{
      columns: [{
        title: 'Title',
        dataIndex: 'title'
      }]
    }}>
      <string keyName="title" />
      <string keyName="content" ui="textarea" />
    </array>
  </root>
)
```