# JavaScript中的import与export

From: <https://medium.com/@etherealm/named-export-vs-default-export-in-es6-affb483a0910>

Named export:

```js
// imports
// ex. importing a single named export
import { MyComponent } from "./MyComponent";
// ex. importing multiple named exports
import { MyComponent, MyComponent2 } from "./MyComponent";
// ex. giving a named import a different name by using "as":
import { MyComponent2 as MyNewComponent } from "./MyComponent";

// exports from ./MyComponent.js file
export const MyComponent = () => {}
export const MyComponent2 = () => {}

import * as MainComponents from "./MyComponent";
// use MainComponents.MyComponent and MainComponents.MyComponent2 here
```

Default export:

```js
// import
import MyDefaultComponent from "./MyDefaultExport";

// export
const MyComponent = () => {}export default MyComponent;
```
