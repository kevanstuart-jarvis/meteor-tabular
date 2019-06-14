orderin:tabular
=========================

A fork of the meteor package aldeed:meteor-tabular to modify the behaviour of the allowFields option to include / exclude specific columns - and then hide those columns on the frontend.

## Installation

```bash
$ meteor add orderin:tabular
```

## Broken behaviour from Aldeed/meteor-tabular

You can optionally provide an `allowFields` function to control which clients can get the published data. These are used by the built-in publications on the server only.

```js
TabularTables.Books = new Tabular.Table({
  // other properties...
  allowFields(userId, fields) {
    return false; // don't allow this person to subscribe to the data
  }
});
```

## The problem
From the documentation: "If you need to be sure that *certain fields are never published* or if different users can access different fields, use `allowFields`."

Mongo uses projection documents that filter fields from the query. The current repository doesn't allow this for more intricate projections.

*Note: allowFields returns a mongo projection document although with the exception of the _id field, you cannot combine inclusion and exclusion statements in projection documents. Please see https://docs.mongodb.com/manual/tutorial/project-fields-from-query-results/*

