---
title: API Reference

language_tabs:
  - shell
  - javascript

toc_footers:

includes:
  - operators
  - errors

search: true
---

# Introduction

Welcome to the Nuodata API! You can use our API to access your Nuodata database, each view or table that has some authorization access is an API point. We will give your more details as we describe the API points.

# Authentication

Nuodata API is for now without authentication but we are working on it to bring to you very soon. In the meantime you can still use the API to build your database.

# Build your schema

To build your database schema or add, update or delete data manually you can use a GUI client. Nuodata recommends

* PSequel http://www.psequel.com/ provides a clean and simple interface for you to perform common PostgreSQL tasks quickly. It is free of charge.
* Postico https://eggerapps.at/postico/ makes PostgreSQL approachable.

You can follow [https://wiki.postgresql.org/wiki/Community_Guide_to_PostgreSQL_GUI_Tools](this guide) for a comprehensive list of applications you can use to connect to PostgreSQL.

# API

## Fetch your table or view data

Fetch the records of your table or view, filter, limit and order according to your needs.

```shell
curl -X GET 'https://mydb.db.nuodata.io/data/users?limit=2&name=like::J*'
```

```javascript
  // fetch
  fetch('https://mydb.db.nuodata.io/data/users?limit=2&name=like::J*').then(function(response) {
    response.json().forEach(function(value) {
      console.log(value.name);
    });
  });
```

> It should return a json

```json
[  
  {
    "name": "John",
    "age": 22
  },
  {
    "name": "Jessie",
    "age": 30
  }
]
```

### HTTP Request

`GET https://<your-database-name>.db.nuodata.io/data/<table-or-view-name>`

### Query Parameters

Parameter | Default | Example | Description
--------- | ------- | -------- | ---
limit     | none    | 25 | To limit the number of records to return
column-name | `eq::<operand>` | `<operator>::<operand>` | To filter the data given some column
order | none | `<column-name>::<desc|asc>` | To order your data given some column, use the default view/table ordering if nothing is specified.

The end point returns an array of records, or an empty array if no records are in the table. If you want to fetch only one record, you can limit the number of result returned but it will still return an array.

## Update your table or view data

Update the records of your table or view, select using filter and limit according to your needs.

```shell
# Update
curl -X PATCH 'https://mydb.db.nuodata.io/data/users?limit=2&name=like::J*'
```

```javascript
  // fetch
  fetch('https://mydb.db.nuodata.io/data/users?limit=2&name=like::J*', {
    method: 'PATCH',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify({
      age: 30
    })
  }).then(function(response) {
    response.json().forEach(function(value) {
      console.log(value.name);
    });
  });
```

> It should return a json of the data that was updated

```json
[  
  {
    "name": "John",
    "age": 3,
    "created_at":"2016-08-26T09:34:23.898Z",
    "updated_at":"2016-08-26T09:34:23.898Z"
  },
  {
    "name": "Jessie",
    "age": 30,
    "created_at":"2016-08-26T09:34:23.898Z",
    "updated_at":"2016-08-26T09:34:23.898Z"
  }
]
```

### HTTP Request

`PATCH https://<your-database-name>.db.nuodata.io/data/<table-or-view-name>`

### Headers

`Content-Type: application/json`

### Query Parameters

Parameter | Default | Example | Description
--------- | ------- | -------- | ----------
limit     | none    | 25 | To limit the number of records to return
column-name | `eq::<operand>` | `<operator>::<operand>` | To filter the data given some column

<aside class="warning">
  You must provide a filter for this request, mass update of a whole table is not allowed so as to prevent mistakes.
</aside>

### Body

```json
{
  "column-name": "value"
}
```

## Insert data into your table or view

Insert records in your table or view.

```shell
# Update
curl -X POST 'https://mydb.db.nuodata.io/data/users?limit=2&name=like::J*'
```

```javascript
  // fetch
  fetch('https://mydb.db.nuodata.io/data/users?limit=2&name=like::J*', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    }
    body: JSON.stringify({
      name: "Somebody",
      age: 30
    })
  }).then(function(response) {
    response.json().forEach(function(value) {
      console.log(value.name);
    });
  });
```

> It should return a json of the data that was inserted

```json
[  
  {
    "name": "Somebody",
    "age": 30,
    "created_at":"2016-08-26T09:34:23.898Z",
    "updated_at":"2016-08-26T09:34:23.898Z"
  }
]
```

### HTTP Request

`POST https://<your-database-name>.db.nuodata.io/data/<table-or-view-name>`

### Headers

`Content-Type: application/json`

### Body

```json
{
  "column-name": "value"
}
```


## Fetch your table or view data

Fetch the records of your table or view, filter, limit and order according to your needs.

```shell
curl -X DELETE 'https://mydb.db.nuodata.io/data/users?limit=2&name=like::J*'
```

```javascript
  // fetch
  fetch('https://mydb.db.nuodata.io/data/users?limit=2&name=like::J*', {
    method: 'DELETE'
  }).then(function(response) {
    response.json().forEach(function(value) {
      console.log(value.name);
    });
  });
```

> It should return a json

```json
[  
  {
    "name": "John",
    "age": 22,
    "created_at":"2016-08-26T09:34:23.898Z",
    "updated_at":"2016-08-26T09:34:23.898Z"
  },
  {
    "name": "Jessie",
    "age": 30,
    "created_at":"2016-08-26T09:34:23.898Z",
    "updated_at":"2016-08-26T09:34:23.898Z"
  },
  {
    "name": "Somebody",
    "age": 30,
    "created_at":"2016-08-26T09:34:23.898Z",
    "updated_at":"2016-08-26T09:34:23.898Z"
  }
]
```

### HTTP Request

`DELETE https://<your-database-name>.db.nuodata.io/data/<table-or-view-name>`

### Query Parameters

Parameter | Default | Example | Description
--------- | ------- | -------- | ---
limit     | none    | 25 | To limit the number of records to return
column-name | `eq::<operand>` | `<operator>::<operand>` | To filter the data given some column

The end point returns an array of deleted records, or an empty array if no records were deleted in the table.

<aside class="warning">
  You must provide a filter for this request, mass update of a whole table is not allowed so as to prevent mistakes.
</aside>
