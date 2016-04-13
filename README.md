# sails-hook-mongoat
[![NPM version][npm-image]][npm-url]
[![Build status][travis-image]][travis-url]
[![Dependency Status][daviddm-image]][daviddm-url]

Provides advanced mongo indexing options for sails.js models that use the sails-mongo adapter.

## Usage

    npm i sails-hook-mongoat

Then simply add an 'indexes' array property to your sails model(s) that you want to add custom indexers on.  This contains all your indexes.

Index properties:

 - **attributes** - an object with the attributes to index (can also be text indexes)
 - **options** (optional) - index options (see [Mongo Index Options](http://docs.mongodb.org/manual/reference/method/db.collection.createIndex/#options-for-all-index-types))

## Examples ##

**Creating a 'expires after' index**
```javascript
// MY MODEL WITH A DATE FIELD
module.exports = {
  attributes: {
    myDate: {
      type: 'date',
      required: true
    }
  },
  indexes: [
    {
      attributes: {
        myDate: 1
      },
      options: {
        expireAfterSeconds: 60  // expire 60s after myDate
      }
    }
  ]
};
```


**Creating a composite unique index**
```javascript
// MY EVENTS MODEL
module.exports = {
  attributes: {
    event_id: {
      type: 'integer',
      required: true
    },
    match_id: {
      type: 'integer',
      required: true
    }
  },
  indexes: [
    //event & match composite index
    {
      attributes: {
        event_id: -1,    // desc
        match: 1         // asc
      },
      options: {
        unique: true
      }
    }
  ]
};
```

## Maintained By
- [Mike Diarmid](https://github.com/salakar)

<img src='http://i.imgur.com/NsAdNdJ.png'>

[npm-image]: https://img.shields.io/npm/v/sails-hook-mongoat.svg?style=flat-square
[npm-url]: https://npmjs.org/package/sails-hook-mongoat
[travis-image]: https://img.shields.io/travis/teamfa/sails-hook-mongoat.svg?style=flat-square
[travis-url]: https://travis-ci.org/teamfa/sails-hook-mongoat
[daviddm-image]: http://img.shields.io/david/teamfa/sails-hook-mongoat.svg?style=flat-square
[daviddm-url]: https://david-dm.org/teamfa/sails-hook-mongoat
