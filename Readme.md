# Brief introduction to Modules

Modules are just JavaScript files that we can import into other JavaScript files. We can then use the code that is in the module in the file that we import it into.

We need to export what we want from the file. This could be a function, a class or even just a variable value or an object. Modules can be our own files and code or they can be part of a package that we install using `NPM` (`Node Package Manager`) or `yarn` which is also a `package manager` for `Node.js`. If you want to use NPM modules in the front-end, you need to use a module bundler like Webpack.

Modules are important because they allow us to break our code into different files. This makes our code more organized and easier to maintain.

Modules are obviously **modular**, so we can reuse them where we want. You may have a module with some utilitly classes to do something. Where ever you want to use that, you can import it and use it easily.

Using a module bundler also means that we can use NPM packages. Therefore you have access to over a million 3rd-party modules over there to enhance your application.

Also, when you use something like Webpack or Parcel, you have access to tools to optimize your project.

## Types Of Modules in Javascript

There are different types of modules in JavaScript. The two main types are `CommonJS Modules` and `ES Modules` or `ES6 Modules`. `CommonJS Modules` are the modules that are usually used in Node.js. When you use a front-end framework like React, or Vue, you'll be using `ES Modules`.

ES Modules and CommonJS modules have a different syntax, but the idea is basically the same. We export what we want from a specific module/file and import it into another. We can export functions, classes, etc.

## Modules & The Browser

When it comes to using modules in the browser, there is support for `ESM` or `ES Modules` in newer browsers, however they're not supported in older browsers. So in order to use them, you will usually use a module bundler like `Webpack` or `Parcel` to bundle our modules into a single file that can be used in the browser.

I will be using yarn, but you can use npm.

So we have to folders, `common_js` which contains basics on how to use common_js which is the default node module and we also have `es_module` folder, which also shows how to use the ES module and an index.html file just to interact with the browser note that we added type here `<script src="app.js" type="module" defer></script>`

Since the `ES` module is not supported in older browsers, we need to use a bundler like `webpack` or `Parcel` which bundles our modules into a file that can be used in the browser.

# Webpack Module Bundler

A module bundler is a tool that takes all of your modules and bundles them into one or more files that can be used in the browser. There are a few popular module bundlers out there, but here, we focus on `Webpack`. There are some others such as `Vite`, `Parcel` and `Snowpack`.

It takes some time to get used to bundlers, but the good news is, once you create a boilerplate, you can use it for pretty much any project that you create.

## How It Works

The way Webpack and other bundlers work is that they take all of your JavaScript files and bundle them into one or more files that can be used in the browser. This allows you to create all kinds of files and modules, use NPM packages, import CSS files and other assets and much more. As you can see from this diagram. We write our code in the source or `src` folder, then we run it through Webpack which bundles it into one or more files that can be used in the browser.

<img src="images/webpack-loaders-and-plugins.png" width="650">
<img src="images/Build-Process-3.png" width="600">

The files in your `dist` or `build` which is `chunk files` folder are the files that you would use in production. You would upload those files to your server. The files in your `src` folder are the files that you would use during development. So you need to get used of the idea that you have `development` or `source` files and `production` or `build` files.

## Webpack Configuration

Webpack is configured using a file called `webpack.config.js`. This file is a JavaScript file that exports an object. The object contains all of the configuration for Webpack.

## Loaders

Loaders are used to process different types of files and convert them into modules that can be used in your application. For instance, if you want to import a CSS file into your JavaScript, you would use a CSS loader. If you want to import an image, you would use an image loader. There are loaders for pretty much anything you can think of. Babel is an example of loader. The Babel loader is commonly used. It is a transpiler that takes your modern JavaScript code and transpile it to older JavaScript that older browsers can understand. We'll look at Babel later.

## Plugins

Webpack also has something called plugins. Plugins are used to extend the functionality of Webpack. For instance, if you want to minify your JavaScript, you would use a minification plugin. If you want to extract your CSS into a separate file, you would use a CSS extraction plugin. We'll be using the `HTMLWebpack` plugin to automatically generate our HTML production files and the `WebpackDevServer` plugin to give us a nice auto reload dev server to work with.
