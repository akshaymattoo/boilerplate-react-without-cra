# boilerplate-react-without-cra

This is a React project setup where we are not using standard CRA. CRA is a great tool but for a small project or a quick proptype, it can be a big overhead sometimes. Also learning about things how they actually work is great. 
Say in the current project we want to make some changes in webpack by this project we can easily learn about thigs. We get a quick understanding of the below things.

- How things are structured in React?
- How React understand JSX and converts it to ES5 JS?
- What webpack is?
- ESLint for following standard Airbnb practices.
- Testing react with react-testing-library.

Before we dive into setup I recommend doing all the steps manually. If you have some idea beforehand you can also git clone the project start working on your idea.

# Setup basic React functioning

We will be using npm to set up the project
- mkdir <directory_name>
 Choose the directory_name at your convinienece. 
 - cd <directory_name>
- npm init -y
 The above command initializes the package.json file. This file has content about dependencies what the project depends on. We can find dependencies in `devDependencies` and `dependencies` sections. This file has some metadata information as well. 
- npm i react react-dom
 The above command will install `react` and `react-dom`. We can see that in `dependencies`. Also you will see `node_modules` directory under root.
- mkdir src
- touch src/index.js
- touch src/App.js
- touch src/App.css
- mkdir public
- touch public/index.html
- npm i -D @babel/core @babel/preset-env @babel/preset-react webpack webpack-cli webpack-dev-server babel-loader css-loader style-loader html-webpack-plugin

The above command will install all the dependencies we need to setup. We can see all of them under `devDependencies`.
Open the code in the editor of choice.

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
// module bundler. Intelligently bundles all the files that we can access in index.js

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
Open App.js file and paste the below content.
```
import React from 'react';
import './App.css';

function App (){
	return(
		<div className="app">
			React Boiler plate
		</div>
	)
}
export default App;
```

Open App.css and paste the below content

```
* {
  margin:0;
  box-sizing: border-box;
}

.app {
  text-align: center;
  font-weight: bold;
  font-size: 5em;
}
```

run `npm run start` from the root directory. This will open a page at port 3000. You will see some text on the screen.We can change the port in `start` in `package.json`.
Up to this point, we have a simple text displayed on the screen. Our app is fully functional. You can add some comonents to it and start working.
For any confusion please refer to the code in the repository.

#Configure ESLint in the project.
Why do we need ESLint. ESLint helps us keep the code consistent. Say you have someone working and you want to ensure same structure we can ensure that through ESLint. In this project we will be using `airbnb` style guide.

- npx eslint --init

The above command will ask some questions how you want to configure your eslint to be. Below is what I recommend for this project.
```
? How would you like to use ESLint? To check syntax, find problems, and enforce code style
? What type of modules does your project use? JavaScript modules (import/export)
? Which framework does your project use? React
? Where does your code run? Browser
? How would you like to define a style for your project? Use a popular style guide
? Which style guide do you want to follow? Airbnb (https://github.com/airbnb/javascript)
? What format do you want your config file to be in? JSON
```
Once you hit `Y` to install it will create a `.eslint.json` file and install some dependencies for it. You can see the dependencies in `devDependencies`. 
# Please feel free to open issues if you find anything wrong with the instructions
 
 Url to file issues: https://github.com/akshaymatoo/boilerplate-react-without-cra/issues