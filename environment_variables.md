# .env file

> Used to protect the secret informations and to share with others. So we will share only the structure to be modify after clone project. In this case is recommended make a file called **.env.example** with to be renamed after clone to **.env** and edit to correct parameters

- first: add .env to your .gitignore
- pattern file: each line contain key=value
- Add extension:

```shell
yarn add dotenv
```

> .env example File

```
APP_URL=http://localhost:3333
NODE_ENV=development

# Auth max 32 characters

APP_SECRET=ItCanBeAnyTextAsYouPrefer@#$%&*

# Database

DB_HOST=
DB_USER=
DB_PASS=
DB_NAME=

# Mongo

MONGO_URL=

# Redis

REDIS_HOST=127.0.0.1
REDIS_PORT=6379

# Mail

MAIL_HOST=
MAIL_PORT=
MAIL_USER=
MAIL_PASS=

# SENTRY

SENTRY_DSN=
```

## IMPORT

> Now you need import the **dotenv** extension in some files.
> **ATTENTION** need to be the first **import**

- add **import 'dotenv/config';** to files bellow:
  - src/app.js
  - src/lib/queue.js -> only if you're using redis
  - src/config/database.js - in this case import using old sintax: **require('dotenv/config')**

## Done, now to use you just call the global variable process

> example: process.env.KEY_NAME; like: process.env.HOST_URL

<a href="README.md"><img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSJNVZV7wCi99hzuk8g0M21gtKq9bUCEUEhMIsYjYT3HqcoeDx1PA" width="90"></a>
