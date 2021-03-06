---
id: data-source-firestore
title: Firestore
sidebar_label: Firestore
---

## Install Dependencies

```shell
$ yarn add firebase-admin @gqlify/server @gqlify/firestore
```

## Download serviceAccount.json
To connect to your Firebase, Canner CLI needs the `serviceAccount.json` of your Firebase App to access data.

![get Firebase serviceAccount.json](assets/firebasesdk.gif)

## Use is `canner.server.js`

**canner.server.js**
```js
const {FirestoreDataSource} = require('@gqlify/firestore');
const admin = require('firebase-admin');
const cert = require('/path/to/serviceAccount.json');

exports.dataSources = {
  firestore: args => new FirestoreDataSource({
    config: {
      credential: admin.credential.cert(cert),
      databaseURL: `https://${cert.project_id}.firebaseio.com`
    },
    collection: args.key,
  }),
}
```

**canner.schema.js**
```js
export default (
  <root>
    <array keyName="posts" dataSource={{name: 'firestore'}}>
      {/* ... */}
    </array>
  </root>
)
```
<!-- WIP
## Use is `canner.cloud.js`

`canner.cloud.js` is used for Canner Cloud version. It supports sandbox feature, so you have to set the different dataSources in different environments.

**canner.server.js**
```js
const admin = require('firebase-admin');
const {FirestoreDataSource} = require('@gqlify/firestore');

const cert = require('/path/to/serviceAccount.json');
const databaseUrl = 'https://databaseName.firebaseio.com';

exports.dataSources = {
  // default env
  default: {
    firestore: args => new FirestoreDataSource({
      config: {
        credential: admin.credential.cert(cert),
        databaseURL,
      },
      path: args.key,
    }),
  }
}
```

**canner.schema.js**
```js
export default (
  <root>
    <array keyName="posts" dataSource={{name: 'firestore'}}>
      {/* ... */}
    </array>
  </root>
)
``` -->
