# Experimenting with `@babel/preset-env`

## With options

### `"useBuiltIns": "entry"`

- `.babelrc`

```
{
  "presets": [
    [
      "@babel/preset-env",
      {
        "useBuiltIns": "entry",
        "targets": "> 0.25%, not dead"
      }
    ]
  ]
}
```

- `index.js`

```js
require("@babel/polyfill");

function codeToBundleGoesHere() {
  var list = [1, 2, 3, 4, 5];
  var res = list.includes(3)
}

module.exports = codeToBundleGoesHere
```

#### Webpack output:

```shell
Hash: 99c4b883d6f1cc58b88a
Version: webpack 4.29.0
Time: 1450ms
Built at: 01/28/2019 6:08:29 PM
    Asset     Size  Chunks             Chunk Names
bundle.js  412 KiB    main  [emitted]  main
Entrypoint main = bundle.js
[./index.js] 5.73 KiB {main} [built]
[./node_modules/webpack/buildin/harmony-module.js] (webpack)/buildin/harmony-module.js 573 bytes {main} [built]
    + 243 hidden modules
```

### `"useBuiltIns": "usage"`

- `.babelrc`

```
{
  "presets": [
    [
      "@babel/preset-env",
      {
        "useBuiltIns": "usage",
        "targets": "> 0.25%, not dead"
      }
    ]
  ]
}
```

- `index.js`

```js
function codeToBundleGoesHere() {
  var list = [1, 2, 3, 4, 5];
  var res = list.includes(3)
}

module.exports = codeToBundleGoesHere
```

#### Webpack output:

```shell
Hash: 9b22e49762beb125db3f
Version: webpack 4.29.0
Time: 697ms
Built at: 01/28/2019 6:07:47 PM
    Asset      Size  Chunks             Chunk Names
bundle.js  31.2 KiB    main  [emitted]  main
Entrypoint main = bundle.js
[./index.js] 181 bytes {main} [built]
[./node_modules/webpack/buildin/harmony-module.js] (webpack)/buildin/harmony-module.js 573 bytes {main} [built]
    + 31 hidden modules
```


## Output

`usage` is deemed [experimental](https://babeljs.io/docs/en/babel-preset-env#usebuiltins-usage-experimental).
It does however remove the need of adding a `require("@babel/polyfill");` in the entry of your app and reduces
the final bundle by a wooping 92.4%.
