# JWT

> Jason Web Tokens. Used to authentication

- JWT have 3 parts:

* Headers - define the token type to frontEnd knows about
* Payload - you can add infos like id, name, emails
* Assignure - anti-editing security

> Install a new extension:

```shell
yarn add jsonwebtoken
```

## Create a file: src/config/auth.js

> Will contain your secret key and token expiration
> Use .env File to configure both

```json
export default {
  secret: process.env.APP_SECRET,
  expiresIn: process.env.APP_EXPIRE,
};
```

## New controller based in User model called SessionController.js

> Will be used to gererate the Token used email + password

```js
import jwt from "jsonwebtoken";
import crypto from "crypto";
import User from "../models/User";
import authConfig from "../../config/auth";

class SessionController {
  async store(req, res) {
    const { email, password } = req.body;
    const user = await User.findOne({ where: { email } });
    /**
     * checking email
     */
    if (!user) {
      return res.status(401).json({ error: "User not found" });
    }

    /**
     * check password
     */
    if (!(await user.checkPassword(password))) {
      return res.status(401).json({ error: "Password does not match" });
    }

    const { id, name } = user;
    return res.json({
      user: {
        id,
        name,
        email
      },
      token: jwt.sign(
        { id },
        crypto
          .createHash("md5")
          .update(authConfig.secret)
          .digest("hex"),
        { expiresIn: authConfig.expiresIn }
      )
    });
  }
}

export default new SessionController();
```

## Make a new folder src/app/middlewares and add a new file _auth.ts_

> This middleware will be inject on the routes.js file to protect all routes that is necessary to have an authentication.

```js
import jwt from "jsonwebtoken";
import { promisify } from "util";
import authConfig from "../../config/auth";

export default async (req, res, next) => {
  /**
   * getting token from header Authorization
   */
  const authHeader = req.headers.authorization;
  if (!authHeader) {
    return res.status(401).json({ error: "Token not provided" });
  }
  const [, token] = authHeader.split(" ");
  try {
    const decoded = await promisify(jwt.verify)(token, authConfig.secret);
    req.userId = decoded.id;
  } catch (err) {
    return res.status(401).json({ error: "Token not provided" });
  }
  return next();
};
```

## Edit src/routes.js to add new middleware

> There are a rule about it: middleware are sequential so, you need to know always the correct place to add.
> routes.js file example

```js
import { Router } from "express";
/**
 * use this area to import your controllers
 */

import UserController from "./app/controllers/UserController";
import SessionController from "./app/controllers/SessionController";

import authMiddleware from "./app/middlewares/auth";

const routes = new Router();

/**
 * Use this area to add your routes
 * ex: routes.get('/', ExampleController.index);
 */

routes.get("/sessions", SessionController.store); // to make token
routes.get("/users", UserController.index); //to list users (OPTIONAL)
/*
* ATTENTION: All routes in this area will not be protected. Here you can add public routes that don't need authentications
(Add Before middleware  authMiddleware)
*/

routes.use(authMiddleware);
/**
 * All routes bellow routes.use(authMiddleare) need to be authenticate with the TOKEN
 */

export default routes;
```

> <a href="README.md"><img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSJNVZV7wCi99hzuk8g0M21gtKq9bUCEUEhMIsYjYT3HqcoeDx1PA" width="90"></a>
