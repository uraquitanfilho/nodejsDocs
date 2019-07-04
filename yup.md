# Validation using YUP package

> YUP is a package used to validate informations sent by client.

- Go to terminal and install YUP

```shell
yarn add yup
```

## How to import YUP ?

> Yup does not have an expert default, so to correct use you need import like:

```js
import * as Yup from "yup";
```

## How to Use ?

> To understand how to use, Let's validate email and password before make a new token
> on the **src/app/controllers/SessionController.js** file

- Import Yup and add the validation code like it:

```js
...
import * as Yup from 'yup';
...
async store(req, res) {
    const schema = Yup.object().shape({
      email: Yup.string()
        .email()
        .required(),
      password: Yup.string()
        .required()
        .min(6),
    });
    if (!(await schema.isValid(req.body))) {
      return res
        .status(400)
        .json({ error: 'Validation fails. Check email and password' });
    }
    ...
}
```
