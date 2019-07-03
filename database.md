# Relational Database

> to use relational Database there are a package called **sequelize** so:
> was used the postgresSQL so we need 2 packages pg and pg-hstore

```shell
yarn add sequelize
yarn add sequelize-cli -D
yarn add pg pg-hstore
```

- We need sequelize-cli to make commands to management database with commands on the terminal

* on the root folder **src** create a new file called **.sequelizerc**

  > Will export the path to **src/config/database**, **migration**, **models** ...

* **.sequelize** file contains:

```javascript
/**
 * ps: this file dont works with import/export so we will import with
 * old form using require.
 *
 * resolve: to works in mac, win, linux. makes a default folder struct
 */
const { resolve } = require("path");

module.exports = {
  config: resolve(__dirname, "src", "config", "database.js"),
  "models-path": resolve(__dirname, "src", "app", "models"),
  "migrations-path": resolve(__dirname, "src", "database", "migrations"),
  "seeders-path": resolve(__dirname, "src", "database", "seeds")
};
```

# src/config/database.js

```javascript
/**
 * we need to use the old import form using require because this file will be
 * access by command line and by project. And command line only allow old form
 */

// support to: mysql, mariadb, sqlite, postgresql, mssql
// to use postgres needs: yarn add pg pg-hstore
module.exports = {
  dialect: "postgres",
  host: process.env.DB_HOST,
  username: process.env.DB_USER,
  password: process.env.DB_PASS,
  database: process.env.DB_NAME,
  define: {
    timestamps: true,
    underscored: true, // to allow table_name format
    underscoredAll: true
  }
};
```

# How to use Sequelize

> to use, we need sequelize-cli package to use with yarn in line command

```shell
yarn sequelize migration:create --name=create-users
```

- go to **src/database/migrations/DATE_GENERATE-create-users.js**

```javascript
module.exports = {
  up: (queryInterface, Sequelize) => {
    return queryInterface.createTable("users", {
      id: {
        type: Sequelize.INTEGER,
        allowNull: false,
        autoIncrement: true,
        primaryKey: true
      },
      name: {
        type: Sequelize.STRING,
        allowNull: false
      },
      email: {
        type: Sequelize.STRING,
        allowNull: false,
        unique: true
      },
      password_hash: {
        type: Sequelize.STRING,
        allowNull: false
      },
      created_at: {
        type: Sequelize.DATE,
        allowNull: false
      },
      updated_at: {
        type: Sequelize.DATE,
        allowNull: false
      }
    });
  },

  down: queryInterface => {
    return queryInterface.dropTable("users");
  }
};
```

## How to execute migrate

```shell
yarn sequelize db:migrate
```

<a href="README.md"><img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSJNVZV7wCi99hzuk8g0M21gtKq9bUCEUEhMIsYjYT3HqcoeDx1PA" width="90"></a>
