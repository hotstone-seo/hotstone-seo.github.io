---
layout: page
title: HotStone Setup
parent: Getting Started
nav_order: 1
---

# HotStone Setup

## Requirements

- [Go (>v1.14)](https://golang.org/)
- [NodeJS (v12)](https://nodejs.org/)
- \* Main Database: [PostgreSQL (11)](https://www.postgresql.org/)
- \* Time-series Database for Analytic: [TimescaleDB](https://www.timescale.com/)
- \* Cache Storage: [Redis](https://redis.io/)
- Google Oauth2 Client ID & Client Secret (enabling user login using Google Account): [Setting up OAuth 2.0](https://support.google.com/cloud/answer/6158849?hl=en)

**Note**: For convenience on local development, HotStone repository already has `docker-compose.yml` so you can install [Docker](https://www.docker.com/) & [Docker Compose](https://docs.docker.com/compose/) to get that \* services easily run.

## How to Run on Local Environment

```bash
$ git clone https://github.com/hotstone-seo/hotstone-seo
$ cd hotstone-seo
```

HotStone uses [Typical-Go](https://github.com/typical-go/typical-go) as the build tool.

### Run Infrastructure Services

```bash
$ ./typicalw docker up        # Equivalent with `docker-compose up -d`
```

### Run Database Migration

* Main Database
  
  ```bash
  $ ./typicalw main-db create
  $ ./typicalw main-db migrate
  ```

* Analytic Database
  
  ```bash
  $ ./typicalw analyt-db create
  $ ./typicalw analyt-db migrate
  ```

### Configuration

**HotStone** load the configuration from environment variables or `.env` file.
If you run `./typicalw` for the first time, it will automatically generates `.env` file with default values for local development.
For local development, you only need set `AUTH_CLIENT_ID` & `AUTH_CLIENT_SECRET` with Google Oauth2 Client ID & Client Secret.

`.env`

```bash
APP_ADDRESS=:8089
APP_DEBUG=false
REDIS_HOST=localhost
REDIS_PORT=6379
REDIS_PASSWORD=redispass
REDIS_DB=0
REDIS_POOL_SIZE=20
REDIS_DIAL_TIMEOUT=5s
REDIS_READ_WRITE_TIMEOUT=3s
REDIS_IDLE_TIMEOUT=5m
REDIS_IDLE_CHECK_FREQUENCY=1m
REDIS_MAX_CONN_AGE=30m
PG_DBNAME=hotstone
PG_USER=postgres
PG_PASSWORD=pgpass
PG_HOST=localhost
PG_PORT=5432
ANALYT_DBNAME=hotstone_analyt
ANALYT_USER=postgres
ANALYT_PASSWORD=pgpass
ANALYT_HOST=localhost
ANALYT_PORT=5433
APP_COOKIE_SECURE=false
APP_JWT_SECRET=7wt5ecr3t
AUTH_JWT_SECRET=7wt5ecr3ß
AUTH_CLIENT_ID=<Google OAuth2 Client ID>
AUTH_CLIENT_SECRET=<Google OAuth2 Client Secret>
AUTH_CALLBACK=http://localhost:3000/auth/google/callback
AUTH_HOSTED_DOMAIN=tiket.com
AUTH_COOKIE_SECURE=false
AUTH_REDIRECT_SUCCESS=http://localhost:3000
AUTH_REDIRECT_FAILURE=http://localhost:3000/login
AUTH_LOGOUT_REDIRECT=http://localhost:3000
```
