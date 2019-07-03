# ERROR Exceptions

> in production mode you can use

- [BUGSNAG](https://stackshare.io/bugsnag)
- [SENTRY](https://sentry.io)
  > express per default using async will not get errors. Whatever there are a extension
  > youch --> helps to show best error informations

```shell
yarn add express-async-errors
yarn add youch
```

- Now import on the **src/app.js** file
  > ps: You need import before routes import

```javascript
import Yarn from "yarn";
/*before routes*/
import "express-async-errors";
import routes from "./routes";
```

## Make a new function exceptionHandler() on src/app.js

> Let's create a new middleware to errors control. Will works only in development mode
> because have many internal informations that need help **DEVELOPERS** only

```js
 exceptionHandler() {
    this.server.use(async (err, req, res, next) => {
      if (process.env.NODE_ENV === 'development') {
        const errors = await new Youch(err, req).toJSON();
        return res.status(500).json(errors);
      }
      return res.status(500).json({ error: 'Internal Server Error!' });
    });
  }
```

- add this.exceptionHandler() to constructor method and exceptions errors will works.

<a href="README.md"><img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSJNVZV7wCi99hzuk8g0M21gtKq9bUCEUEhMIsYjYT3HqcoeDx1PA" width="90"></a>
