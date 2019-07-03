# Nodemon + Sucrase

> Nodemon used in DEV mode to continous live update
> Sucrase used in NodeJS to change **require()** for **import**

# Install

````shell
yarn add nodemon sucrase -D
```e
* In the root of project create a file called **nodemon.json** and add the bellow code:
> This is necessary to changes the default node executable to new sucrase-node executable
```json
{
  "execMap": {
    "js": "sucrase-node"
  }
}

````

- Edit **Package.json** and create or edit the **scripts** section

```json
...
scripts:{
  ...,
  "dev": "nodemon <PATH>/server.js"
}
...
```

- <PATH> you need changes to your correct path

### Now you need just enter in the terminal:

```shell
yarn dev
```

# Eslint + Prettier

> Prettier makes the beautiful code. adjuste lines, spaces...
> Go to terminal and ENTER:

```shell
yarn add eslint -D
```

> After install ENTER:

```shell
yarn eslint --init
```

### Will open a menu to choose some options:

> Choose:

- To check syntax, find problems, and enforce code style
- JavaScript modules(import/export)
- None of these (but you can choose was you prefer)
- Use space KEY to uncheck Browser and select Node
- Use a popular style guide
- Airbnb
- JavaScript
- Press Enter and Enter Y to install dependencies

> ESLINT per default uses NPM to dependence install. If you're using yarn needs make bellow:

- Remove package-lock.json
- go to terminal and enter to map dependencies into yarn files:

```shell
yarn
```

### Now, was generate a new file: _.eslintrc.js_

> Edit like this:

```javascript
module.exports = {
  env: {
    es6: true,
    node: true
  },
  extends: ["airbnb-base", "prettier"],
  plugins: ["prettier"],
  globals: {
    Atomics: "readonly",
    SharedArrayBuffer: "readonly"
  },
  parserOptions: {
    ecmaVersion: 2018,
    sourceType: "module"
  },
  rules: {
    "prettier/prettier": "error",
    /* per default all class method need use this but controllers and app will
    stay inside classes but would not necessary to use this */
    "class-methods-use-this": "off",
    "no-param-reassign": "off", //to allow receive and modify parameters
    camelcase: "off", //to allow variables
    /* To allow declare next variable and never uses it (this is important to
    middlewares) */
    "no-unused-vars": ["error", { argsIgnorePattern: "next" }]
  }
};
```

> We need install new packages

```shell
yarn add prettier eslint-config-prettier eslint-plugin-prettier -D
```

> create a file on the project root called **.prettierrc** Why? because prettier and eslint have some default different rules, then we need to override some rules

- add this code to your **.prettierrc** file

```json
{
  "singleQuote": true,
  "trailingComma": "es5"
}
```

> To check all files at same time go to terminal and enter:

```shell
yarn eslint --fix src --ext .js
```

_src -> root folder of project files_

### SETUP the plugin _EditorConfig for VS Code_

> default settings to others editors (sublime and others)

- Go to VSCode and go to Explore MENU.
- Press right click and choose last option **Generator .editorconfig**
- Edit like:

```
root = true

[*]
indent_style = space
indent_size = 2
charset = utf-8
trim_trailing_whitespace = true
insert_final_newline = true
```

# Make project folder

> To work with express is free.. you can make your own folder organization so, I will suggest:

- **src** root folder inside project name folder
- **src/app** folder will contain **controllers** and **models** folders
- **src/config** all configurations file. example: **datatase.js** that contains the string connection
- **src/database** will contain the **migrations** and the index.js to **SETUP** the path and database rules.

```
cd /<PATH>/project_name

 > src
   > app
     > controllers
     > models
   > config
     > database.js
   database
     > migrations
     > seeds
     > index.js
 > app.js
 > server.js
 > routes.js
```

<a href="README.md"><img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSJNVZV7wCi99hzuk8g0M21gtKq9bUCEUEhMIsYjYT3HqcoeDx1PA" width="90"></a>
