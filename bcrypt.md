# How to Crypt Password

> There are extension called bcrypt. So first lets install it

```shell
yarn add bcrypt
```

## import and use

```js
import bcrypt from 'bcrypt';

...
YOUR_VARIABLE = await bcrypt.hash(YOUR_PASSWORD,8);
```

## To compare

```js
  checkPassword(password) {
    return bcrypt.compare(password, YOUR_DATABASE_PASSWORD_HASH);
  }
```
