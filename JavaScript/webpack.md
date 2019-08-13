> ****WIP***

# Webpack

* Module Bundler
* Task Runner
* Build

## 1.1. Introduction

    Webpack is a module bundler. Webpack can take care of bundling alongside a separate task runner. However, the line between bundler and task runner has become blurred thanks to community developed webpack plugins. Sometimes these plugins are used to perform tasks that are usually done outside of webpack, such as cleaning the build directory or deploying the build.

## 1.2. Project initialization

* `npm init` -> Initialize project 
* `npm install webpack --save-dev` -> Install webpack
* `npm install webpack-dev-server --save-dev` -> Installs dev server (Optional)


## 2. Webpack initialize

There are two methods.

1. Using package.json
2. Using webpack config file

## 2.1. Using package.json (Not advised)

1. Add script rule in `package.json`:

	```js
		//...
		"scripts": {
			// Build
			"build": "webpack src/js/app.js dist/js/bundle.js"
			// Prod build
			"build:prod": "webpack src/js/app.js dist/js/bundle.js -p"
			// building and serving via webpack-dev-server 
		    "build": "webpack-dev-server --entry ./src/js/app.js --output-filename ./dist/js/bundle.js"
		  },
		  ....
	```

2. Running

	Run `npm run build` or `npm run build:prod` to run scripts.

## 2.2. Using webpack config files

1. create `webpack.config.js` file

	```js
		// webpack.config.js
		const path = require('path');
		var webpack = require('webpack');
		module.exports = {
		  entry: './src/js/app.js',
		  output: {
		    path: path.resolve(__dirname, 'dist/js/'),
		    filename: 'bundle.js',
		    publicPath: '/dist/js'
		  },
		  module: {
		    rules: [
		      {
		        test: /\.css$/,
		        // loader: 'css-loader'
		        use: [
		          'style-loader',
		          'css-loader'
		        ]
		      }
		    ]
		  },
		  plugins: [
		    new webpack.ProgressPlugin(),
		  ]
		};
	```

2. Using css libraries `npm install css-loader style-loader --save-dev`

3. importing css to js for loading

	```js
	import "../css/style.css";
	// Remaining javascript goes here
	alert('hi');
	console.log('hello');
	```

4. Updating package.json

	```js
		// package.json
		...
		"scripts": {
		  "test": "echo \"Error: no test specified\" && exit 1",
		  "start": "webpack-dev-server",
		  "build": "webpack -p"
		},
		...
	```

## 3. Libraries and Plugin

`npm install sass-loader node-sass css-loader extract-text-webpack-plugin babel-core babel-preset-es2015 --save-dev`

# 3.1. Libraries

	```js
		// webpack.config.js
		const path = require('path');
		var ExtractTextPlugin = require('extract-text-webpack-plugin');
		var extractPlugin = new ExtractTextPlugin({
			filename: 'main.css'
		});

		module.exports = {
		  entry: './src/js/app.js',
		  output: {
		    path: path.resolve(__dirname, 'dist/js/'),
		    filename: 'bundle.js',
		    publicPath: '/dist/js'
		  },
		  module: {
		    rules: [
		      {
		        test: /\.js$/,
		        use: [
		        	{
		        		loader: 'babel-loader',
		        		options: {
		        			presets: ['es2015']
		        		}
		        	}
		        ]
		      },
		      {
		      	test: /\.scss$/,
		      	use: extractPlugin.extract({
		      		use: ['css-loader', 'sass-loader']
		      		})
		      }
		    ]
		  },
		  plugins: [
		    extractPlugin
		  ]
		};
	```