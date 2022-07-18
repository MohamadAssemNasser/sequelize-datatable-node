New Sequelize Datatables
====================

Server-side datatables with Sequelize.

#### Support

* Node.js v7.6 & later
* Sequelize v6

#### Instalation

```
yarn add new-sequelize-datatables
```

#### API

```js
datatable(
  model: SequelizeModel required,
  config: Object required,
  params: Object,
  options: Object
) -> Promise<Object>
```

This function takes three arguments to produce output for datatables.

* `model` - `required` - is the sequelize model.
* `config` - `required` - is config sent by jQuery datatables to our server.
* `params` - options for sequelize query.
* `options` - library specific options. See below


**Options**

* `caseInsensitive: Boolean` - A flag for postgresql dialec. If this is set to `true`, `ILIKE` will be used instead of `LIKE` Default to `false`.
* `replaceRegexp` - A workaround in case dialect does not support native regex, but you need to search for list of exact matches, passed as regex expression, `^((?!debug|info.*)$`. See working example: http://live.datatables.net/kopafape/1/edit

#### Example Usage

```js
const datatable = require(`new-sequelize-datatables`);
const model = require(`./path/to/sequelize-model`); // Sequelize model

// assuming you are using express

route.get(`/datasource`, (req, res) => {
  datatable(model, req.query, {})
    .then((result) => {
      // result is response for datatables
      res.json(result);
    });
});
```