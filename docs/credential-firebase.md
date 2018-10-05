---
id: credential-firebase
title: Credential in Firebase
sidebar_label: Firebase
---

We need your Firebase private key to access more control in your Firebase, such as more complete APIs, and storage APIs.

## Generating Firebase credential

Visit your Firebase console, and navigate to **Project settings** > **Service accounts** > **Generate new private key**, after downloading the private key and place wherever you want to put in the project.

![firebasesdk](/img/firebasesdk.gif)

## Setup Firebase credential in `canner.cloud.js`

In order to let Canner platfrom access to your Firebase you have to upload the credentials.

In your `canner.cloud.js`, setup `env` settings using `FirebaseCert` in `canner-credential`.

**Example**

```js
const {FirebaseCert} = require("canner-credential");

module.exports = {
  env: {
    default: [new FirebaseCert(require("path to your credential"))],
    test: [new FirebaseCert(require("path to your credential"))]
  }
}
```

> Best practice: You should **ignore** your credentials in your git repository.