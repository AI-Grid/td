---
sidebar_position: 2
---

# Manual

Install TeleDrive with manual installation.

## Prerequisite

Get started by installing all needed services and define all variables.

### What you'll need

- [PostgreSQL](https://www.postgresql.org/) version 14.2 or above:

  Install with this command (Ubuntu):

  ```shell
  sudo apt install postgresql -y
  ```

- [Node.js](https://nodejs.org/en/download/) version 16.14.2 or above:

  Install LTS version with command:

  ```shell
  sudo apt install nodejs -y    # if, using Ubuntu

  # install node version
  npm i -g n
  n stable
  ```

- [Yarn](https://yarnpkg.com/getting-started/install) version 1.22.17 or above:

  Install with npm:

  ```shell
  npm i -g yarn
  ```

- Define all server variables in `./server/.env`, you can copy from `./server/.env.example`

  ```shell
  cp ./server/.env.example ./server/.env
  ```

  Explanation:

  | env                    | required | description                                           |
  | ---------------------- | -------- | ----------------------------------------------------- |
  | ENV                    | no       | Hide the logs for production, default: develop        |
  | PORT                   | no       | Port for running API, default: 4000                   |
  | TG_API_ID              | yes      | Application ID from your Telegram App                 |
  | TG_API_HASH            | yes      | Application hash from Telegram App                    |
  | DB_HOST                | no       | Database host URI, default: localhost                 |
  | DB_NAME                | yes      | Database name                                         |
  | DB_PORT                | no       | Database port, default: 5432                          |
  | DB_USERNAME            | yes      | Database username                                     |
  | DB_PASSWORD            | yes      | Database password                                     |
  | API_JWT_SECRET         | yes      | Random string for encrypt JWT web token               |
  | FILES_JWT_SECRET       | yes      | Random string for encrypt public files                |

- Define all web variables in `./web/.env`, you can copy from `./web/.env.example`

  ```shell
  cp ./web/.env.example ./web/.env
  ```

   Explanation:

  | env                   | required | description                                                       |
  | --------------------- | -------- | ----------------------------------------------------------------- |
  | REACT_APP_API_URL     | no       | Base URL for the API, default: `''` (empty string)                |
  | REACT_APP_TG_API_ID   | yes      | Application ID from your Telegram App *(for experimental features)* |
  | REACT_APP_TG_API_HASH | yes      | Application hash from Telegram App  *(for experimental features)*   |

### Database preparation

You need to create and import the database schema.

- Create database

  Login as *postgres* user:

  ```shell
  psql -U postgres

  # or
  sudo su - postgres
  psql
  ```

  Then, run:

  ```shell
  CREATE DATABASE teledrive;
  ```

- Import schema

  Exit from psql (with `\q`) and run this command:

  ```shell
  psql teledrive < ./server/src/model/migrations/dump.sql
  ```

**Note.** *If you follow the instructions above then you need to fill the server variables:*
- `DB_NAME`: teledrive
- `DB_USERNAME`: postgres


### Dependencies installation

Install all dependencies with yarn:

```shell
yarn install
```

## Build:

```shell
yarn workspaces run build
```

## Run:

```shell
cd server && node dist/index.js
```

Done! You can now open [localhost:4000](http://localhost:4000) in your browser 🎊

## Upgrade

Upgrade to the latest version of TeleDrive with this command:

```shell
git pull origin main             # or, staging for the latest updates

yarn install                     # install
yarn workspaces run build        # build
cd server && node dist/index.js  # run
```

Next, you can deploy TeleDrive with [Vercel](/docs/deployment/vercel) or [PM2](/docs/deployment/pm2).