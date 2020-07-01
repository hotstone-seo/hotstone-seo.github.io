---
layout: page
title: HotStone Client Config
parent: Advanced
nav_order: 1
---

# HotStonce Client Config

```js
import { HotStoneClient } from 'hotstone-client'
// ...
const hotstoneURL = 'http://localhost:8089'
const clientKey = 'Otdu1qe.A5eKbNQ3Kj26kiTQmwWAmzaQGk5uYmSI'
const fetchOpts = { cacheManager: `./hotstone-local-cache` } // enable local cache
const client = new HotStoneClient(hotstoneURL, clientKey, fetchOpts)
// ...
```

## Mandatory

- `hotstoneURL`: URL of **HotStone Provider**
- `clientKey`: To interact with **HotStone Provider**, it needs client key. Get client key from **HotStone UI** / Dashboard on menu `Client Keys`

## Optional

- `fetchOpts`: Under the hood, **HotStone Client** uses [make-fetch-happen](https://www.npmjs.com/package/make-fetch-happen).

### Fetch Config: `fetchOpts`

We can pass [extra fetch options](https://www.npmjs.com/package/make-fetch-happen#extra-options) to get additional features.

#### Set Timeout

```javascript
const fetchOpts = { timeout: 30 * 1000 } // in ms
```

#### Local Caching

Local caching with cache directory `./hotstone-local-cache`

```javascript
const fetchOpts = { cacheManager: `./hotstone-local-cache` }
```
