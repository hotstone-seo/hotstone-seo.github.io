---
layout: page
title: HotStone Client Usage
parent: Getting Started
nav_order: 2
---

# Walkthrough

[HotStone Client](https://www.npmjs.com/package/hotstone-client) is a Javascript library used by server-side-rendering (SSR) web app to get HTML tag data for every requesting page.
Then, HTML tag data can be rendered with [React Helmet](https://github.com/nfl/react-helmet).

This page will guide you to initiate a simple SSR web app and use **HotStone Client** upon it.
If you already have a SSR web app, you can jump to [HotStone Client Usage](#hotstone-client-usage) to know how to use **HotStone Client**.

Or, you can read full source code that is availabe on <https://github.com/hotstone-seo/hotstone-workshop>

## Initiate A Simple SSR Web App

We will use [Create React SSR App](https://create-react-ssr-app.dev/) to easily setup a React SSR app.

```bash
$ npx create-react-ssr-app ssr-app
$ cd ssr-app
$ npm install
$ npm install react-helmet serialize-javascript
```

Modify `src/server/index.js` to get a bare minimum SSR app that ready to integrate with **HotStone Client**

```js
// src/server/index.js
import path from 'path';
import express from 'express';
import React from 'react';
import { Helmet } from 'react-helmet';
import ReactDOMServer from 'react-dom/server';
import serialize from 'serialize-javascript';
import App from '../App';

const publicPath = path.join(__dirname, '/public');
const app = express();

app.use(express.static(publicPath));

const template = ({ body, helmet }, data) => {
    return `
      <!DOCTYPE html>
      <html ${helmet.htmlAttributes.toString()}>
        <head>
          ${helmet.title.toString()}
          ${helmet.meta.toString()}
          ${helmet.link.toString()}
          ${helmet.script.toString()}
        </head>
        <body ${helmet.bodyAttributes.toString()}>
          <div id="root">${body}</div>
          <script>window.__data = ${serialize(data)}</script>
        </body>
      </html>
    `
}

app.get('*', (req, res, next) => {
    (async function() {
      try {
        const data = {}

        const appString = ReactDOMServer.renderToString(<App />);
        const helmet = Helmet.renderStatic();
   
        res.send(template({ body: appString, helmet: helmet }, data));
      } catch(error) {
        next(error);
      }
    })();
   });

export default app;
```

For convenience, let's remove big React logo at `src/App.js`

```javascript
// src/App.js
import React from 'react';

// import logo from './logo.svg';
import './App.css';

function App() {
  return (
    <div className="App">
      <header className="App-header">
        {/* <img src={logo} className="App-logo" alt="logo" /> */}
        <p>
          Edit <code>src/App.js</code> and save to reload.
        </p>
        <a
          className="App-link"
          href="https://reactjs.org"
          target="_blank"
          rel="noopener noreferrer"
        >
          Learn React
        </a>
      </header>
    </div>
  );
}

export default App;
```

Run SSR web app:

```bash
$ npm run start
```

If it's successfully running, open <http://localhost:3000>

## HotStone Client Usage

Install **HotStone Client**

```bash
$ npm install hotstone-client
```
