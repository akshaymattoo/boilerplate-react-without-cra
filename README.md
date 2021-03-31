# boilerplate-react-without-cra

This is a React project setup where we are not using standard CRA. CRA is a great tool but for small project or a quick proptype it can be a big overhead sometime. Also learning about things how they actually work is great. 
Say in the current project we want to make some changes in webpack by this project we can easily learn about thigs. We get a quick understanding about the below things.

- How things are strutured in React?
- How React understands JSX and converts it to ES5 JS?
- What webpack is?
- ESLint for follow standard Airbnb practices.
- Testing react with react-testing-library.


# Setup basic React functioning

We will be using npm to setup the project
- mkdir <directory_name>
 Choose the directory_name as per your convinienece. 
 - cd <directory_name>
- npm init -y
 The above command initialises the package.json file. This file has content about dependencies what project depends on. We can find dependencies in `devDependencies` and `dependencies` section. This file has some metadata information as well. 
- npm i react react-dom
 The above command will install `react` and `react-dom`. We can see that in `dependencies`. 
- mkdir src
- touch src/index.js
- touch src/app.js
- touch src/app.css
- mkdir public
- touch index.html
- npm i -D @babel/core @babel/preset-env @babel/preset-react webpack webpack-cli webpack-dev-server babel-loader css-loader style-loader html-webpack-plugin

The above command will install all the dependencies we need to setup. We can see all of them under `devDependencies`.
Open the code in editor of choice.

Open public/index.html and paste the below content
```
<!DOCTYPE html>
<html>
<head>
	<title>React boiler plate</title>
</head>
<body>
	<div id='root'></div>
</body>
</html>

```
- touch webpack.config.js
Open webpack.config.js and paste the below content.

```
// module bundler . Inteligently bundles all the files that we can access in index.js

const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
  entry: './src/index.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'main.js',
  },
  devServer: {
    historyApiFallback: true,
  },
  resolve: {
    modules: [__dirname, 'src', 'node_modules'],
    extensions: ['*', '.js', '.jsx', '.tsx', '.ts'],
  },
  module: {
    rules: [
      { test: /\.(js)$/, exclude: /node_modules/, use: 'babel-loader' },
      {
        test: /\.jsx?$/,
        exclude: /node_modules/,
        loader: require.resolve('babel-loader'),
      },
      { test: /\.css$/, use: ['style-loader', 'css-loader'] },
      {
        test: /\.(png|j?g|svg|gif)?$/,
        use: 'file-loader',
      }
    ],

  },
  mode: 'development',
  plugins: [
    new HtmlWebpackPlugin({
      template: path.resolve(__dirname, 'public/index.html'),
      filename: 'index.html',
    })
  ]
};

```
Open package.json file and paste the below content under scripts 

```
"start": "webpack serve --port 3000 --hot --open",
"build": "webpack --mode production",
```

Add the section in package.json

```
"babel": {
  "presets": [
    "@babel/preset-env",
    "@babel/preset-react"
  ]
},
```

Open index.js file and paste the below content
```
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';

ReactDOM.render(<App />, document.getElementById('root'));

```
Open app.js file and paste the below content.
```
import React from 'react';
import './app.css';

function App (){
	return(
		<div className="app">
			React Boiler plate
		</div>
	)
}
export default App;
```

Open app.css and paste the below content

```
* {
	margin:0;
  box-sizing: border-box;
}

.app {
	display: flex;
	margin:0 auto;
}

```


# Please feel free to open issues if you find anything wrong in the instruction 
 
 Url to file issues : https://github.com/akshaymatoo/boilerplate-react-without-cra/issues