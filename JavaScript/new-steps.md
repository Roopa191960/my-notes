## STEPS:
* Initialize project: `npm init -y`
* Install webpack: `npm i -D webpack webpack-cli webpack-dev-server`
* Add `"build": "webpack"` in package.json scripts node.
* Create `./src/index.js` `./src/index.html` files in src directory.
* Run `npm run build`
* Install html dependencies: `npm i -D html-plugin html-loader html-webpack-plugin`
* Add webpack configuration in `webpack.conf.js` file.
* Add `"start:dev": "webpack-dev-server"` in package.json scripts node.
* Install babel support `npm i -D @babel/core babel-loader @babel/preset-env`
* Install Image/File support `npm i -D file-loader`
* Install SASS-CSS support `npm i -D file-loader node-sass css-loader style-loader sass-loader mini-css-extract-plugin`
* Create `src/styles/main.sass` & import same in `index.js`
* Using bootstrap: ``

## FILES: 
```js
// webpack.config.js
const htmlWebpackPlugin = require("html-webpack-plugin");
const miniCssExtractPlugin = require("mini-css-extract-plugin");

module.exports = {
    module:{
        rules:[{
            test: /\.(png|svg|gif)$/,
            use:[{
                loader: "file-loader",
            }]
        },
        {
            test: /\.html$/,
            use:[{
                loader: "html-loader",
                options:{ minimize: false }
            }]
        },
        {
            test: /\.js$/,
            exclude: /node_modules/,
            use: [{
                loader: "babel-loader"
            }]
        },
        {
            test: /\.scss$/,
            use: [
                "style-loader",
                "css-loader",
                "sass-loader"
            ]
        }]
    },
    plugins:[
        new htmlWebpackPlugin({
            template: "./src/index.html",
            filename: "./index.html"
        }),
        new miniCssExtractPlugin({
            filename: "[name].css",
            chunkFilename: "[id].css"
        })
    ]
}
```

```js
// index.js
import { bro } from './bro';
import 'bootstrap';
import './styles/main.scss';
console.log(bro('Dude'));
```

```scss
// main.scss
@import "~bootstrap/scss/bootstrap";

$bg : skyblue;
body{
    background: $bg;
}
```

```html
