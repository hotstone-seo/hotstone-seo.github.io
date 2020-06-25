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

# to use 'renderHelmetTags'
$ npm install react
```

### On Server-Side

To initiate `HotStoneClient`, it requires two mandatory arguments and last optional argument:

```js
// src/server/index.js
import { HotStoneClient } from 'hotstone-client'
// ...
const hotstoneURL = 'http://localhost:8089'
const clientKey = 'Otdu1qe.A5eKbNQ3Kj26kiTQmwWAmzaQGk5uYmSI'
const fetchOpts = { cacheManager: `./hotstone-local-cache` } // enable local cache
const client = new HotStoneClient(hotstoneURL, clientKey, fetchOpts)
// ...
```

- (mandatory) `hotstoneURL`: URL of **HotStone Provider**
- (mandatory) `clientKey`: To interact with **HotStone Provider**, it needs client key. Get client key from **HotStone UI** / Dashboard on menu `Client Keys`
- (optional) `fetchOpts`: Under the hood, **HotStone Client** uses [make-fetch-happen](https://www.npmjs.com/package/make-fetch-happen). We can pass [extra fetch options](https://www.npmjs.com/package/make-fetch-happen#extra-options) to get additional features, i.e. local caching with `{ cacheManager: './hotstone-local-cache' }`

**HotStone Client** has two main functions :
- `match(<path>)`: retrieve SEO rule data of a page by matching its  request page path.
- `tags(<rule>, <locale>)`: retrieve HTML tag data associated with given rule and locale.

Let's call these functions on `src/server/index.js`

```js
// src/server/index.js
import { HelmetWrapper } from '../hotstone'
// ...
app.get('*', (req, res, next) => {
    (async function () {
        try {
            const rule = await client.match(req.path);
            const tags = await client.tags(rule, "en_US");
            const data = { tags }

            const appString = ReactDOMServer.renderToString(
                <HelmetWrapper tags={tags}>
                    <App />
                </HelmetWrapper>
            );
            const helmet = Helmet.renderStatic();
            res.send(template({ body: appString, helmet: helmet }, data));
        } catch (error) {
            next(error);
        }
    })();
});
// ...
```

`data` that contains `tags` also passed on to `window.__data`

### `HelmetWrapper`

If you notice, there is a wrapper component that receives `tags`.
This component simply renders `tags` as HTML tag using `renderHelmetTags` provided by **HotStone Client**.

Remember, `HelmetWrapper` is not part of **HotStone Client** package. It's just a sample component to demonstrate how to use `renderHelmetTags` with React Helmet.

```javascript
// src/hotstone/index.js
import React from 'react'
import Helmet from 'react-helmet'
import { renderHelmetTags } from 'hotstone-client/lib/react';

class HelmetWrapper extends React.Component {
  constructor(props) {
      super(props);

      const { tags } = props;
      this.state = { tags };
  }

  render() {
      const { tags } = this.state;
      return (
          <div>
              <Helmet>{renderHelmetTags(tags)}</Helmet>
          </div>
      );
  }
}

export { HelmetWrapper }
```
