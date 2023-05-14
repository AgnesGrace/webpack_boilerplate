# Webpack Setup

We are going to setup Webpack.The goal is to create a `webpack-starter` boilerplate that you can re-use in future applications. So you can alsways make use of this boiler plate, just extract the `webpack_boilerplate` that we are going to add.

Let's start off by creating a folder called `webpack_boilerplate`. Open it with your text editor and run `yarn init` to create a package.json file.

Create a `src` folder and a `dist` folder. The `src` folder is where we are going to put our source code. The `dist` folder is where we are going to put our bundled code which is used for production.

Create an `index.html` file in the `dist` folder. We'll put some boilerplate HTML. We are going to create a `script` tag and point it to a file called `bundle.js`. This file does not exist yet. This is the output file that Webpack is going to create for us.

Now, create a file called `index.js` in the `src` folder. This will be the entry point for our application.

## Installing Webpack

Now we are going to install Webpack. Run `yarn add -D webpack webpack-cli`. We use the `-D` to save as a `development dependency`. Meaning this is a dev tool and it won't be used in production. This will get put in the `devDependencies` section in the package.json file.

## .gitignore

Let's create a `.gitignore` file. We don't want to commit the `node_modules` folder to GitHub. We also don't want to commit the `dist` folder. We are going to create that folder when we build our application. We are going to add the `dist` folder to the `.gitignore` file.

```js
node_modules
dist
```

## Create Build Script

Let's open up the `package.json` file and create a build script which is a command that we can run to take our source code and bundle it into our production files.

```json

"scripts": {
  "build": "webpack"
}
```

## Create webpack.config.js

Next, create a `webpack.config.js` file with

```js
const path = require('path')
module.exports = {
  node: 'development',
  entry: './src/index.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js',
  },
}
```

Now, let's run `yarn build`. This will run the build script. We should see a `bundle.js` file show up in the `dist` folder.

## Loaders

Next we add loaders, so we can add `css-loader` and `style-loader` as devDependencies. First, we run `yarn add -D css-loader style-loader` then configure them in the `webpack.config.js` as follows:

```js
const path = require('path')
module.exports = {
  mode: 'development',
  entry: './src/index.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js',
  },
  module: {
    rules: [
      {
        test: /\.css$/,
        use: ['style-loader', 'css-loader'],
      },
    ],
  },
}
```

then create a `css` folder in the `src` add `style.css` file and add any style of your choice, for instance

```css
body {
  color: blue;
}
```

Now we can easily import this file in the `index.js`

```js
import './css/style.css'
```

The beauty of this is that we don't have to incluse the stylesheet in our `index.html`, remember how you import `css` in for instance ` React`. Also we don't include it in the dist folder because it is all bundled...
Hence, your production file is very clean.

# Plugins

We add html plugin by following prety much similar steps as loaders, so we install it as devDepencies and also configure...

with `html-webpack-plugin` set up, we can delete the `dist` folder and whenever we run `yarn build`, the `html-webpack-plugin` creates the dist automatically with an `index.html` and also our `bundle.js`. This is nice⭐️

Now the `webpack.config.js` looks like this

```js
const path = require('path')
const htmlWebpackPlugin = require('html-webpack-plugin')
module.exports = {
  mode: 'development',
  entry: './src/index.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js',
  },
  module: {
    rules: [
      {
        test: /\.css$/,
        use: ['style-loader', 'css-loader'],
      },
    ],
  },
  plugins: [
    new htmlWebpackPlugin({
      title: 'Webpack App Boilerplate',
      filename: 'index.html',
      template: '/src/index.html',
    }),
  ],
}
```

The `template: '/src/index.html'` is important, because this keeps the content of our html so we don't loose them whenever we run build. So we added `index.html` in the `src` which looks like this

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title><%=htmlWebpackPlugin.options.title %></title>
  </head>
  <body>
    <h1><%=htmlWebpackPlugin.options.title %></h1>
    <h2>This is amazing</h2>
  </body>
</html>
```

Finally,we added the babel loader and our webpack config looks like

```js
const path = require('path')
const htmlWebpackPlugin = require('html-webpack-plugin')
const MiniCssExtractPlugin = require('mini-css-extract-plugin')
module.exports = {
  mode: 'development',
  entry: './src/index.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js',
  },
  module: {
    rules: [
      {
        test: /\.css$/,
        use: [MiniCssExtractPlugin.loader, 'css-loader'],
      },
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: {
          loader: 'babel-loader',
          options: {
            presets: ['@babel/preset-env'],
          },
        },
      },
    ],
  },
  plugins: [
    new htmlWebpackPlugin({
      title: 'Webpack App Boilerplate',
      filename: 'index.html',
      template: '/src/index.html',
    }),
    new MiniCssExtractPlugin(),
  ],
  devServer: {
    static: {
      directory: path.resolve(__dirname, 'dist'),
    },
    port: 3001,
    open: true,
    compress: true,
    historyApiFallback: true,
  },
}
```

Visit `link https://www.npmjs.com/package/html-webpack-plugin` for more detailed explanation.

Have fun!!!
