# GARAIO REM GraphQL API

GARAIO REM implements a [GraphQL](https://graphql.org) API to communicate with a GARAIO REM instance. In order to use it, you

- need the url of the GARAIO REM endpoint that runs the GraphQL backend
- know your authentication credentials

Contact [info@garaio-rem.ch](mailto:info@garaio-rem.ch) to get this information.

Since GraphQL is self documenting, you won't find the API specs here. See "Schema Documentation" for further infos. Every request in GraphQL is a `POST` request with the Query inside the body.
In GraphiQL (the webinterface of GraphQL) you have the keyboard shortcut `ctrl`+`space` for the autocompletion.

Find out what's new in the [Changelog](Changelog.md)

## Versioning

The master branch in this repository reflects current development. If you need the specs for a specific release, have a look at the corresponding branch.

## Authentication

Send a `POST` request to `/external/graphql/authenticate/token`, eg <https://demo.garaio-rem.net/external/graphql/authenticate/token>...

### As a service partner

with the following form data:

- grant_type: client_credentials
- client_id: \<your client id>
- client_secret: \<your client secret>

### As a GARAIO REM user

with the following form data:

- grant_type: password
- username: \<the user name>
- password: \<the user password>

#### Example

```bash
curl --request POST \
  --url 'https://demo.garaio-rem.net/external/graphql/authenticate/token' \
  --header 'content-type: application/x-www-form-urlencoded' \
  --data grant_type=client_credentials \
  --data client_id=<your client id> \
  --data client_secret=<your client secret>
```

### Using the access token

You will receive an access token in the response. Pass the access token in the authorization header for the following requests. Javascript example:

```javascript
const requestOptions = { headers: { Authorization: `Bearer ${accessToken}` } }
```

Access tokens have a short lifespan. They are good for a batch of queries, but do not store them for later use. If the token has expired, you'll get an error response and must authenticate again:

```json
{
  "errors": [
    {
      "extensions": {
        "code": "invalid_token"
      },
      "message": "token_expired"
    }
  ]
}
```

## Access Restrictions

Sensitive queries / mutations / fields are protected and not accessible unless we grant access to it, eg tenant / tenancy data. If you try to query fields without the required permissions you will get Not Authorized errors.

Contact us if you think you should have access to them.

## Paginated queries

In order to support very large databases with predictable query performance and system load, most of the root queries are paginated. In order to get the complete dataset, you must run the query more than one time, depending on the database you are querying.

Each paginated query returns a cursor and a page. Do not forget to query the cursor in order to know if you already got the complete dataset or not. If the cursor returns null, you've queried the last (or only) page.

The page size is 50 elements; If you query a database with 1001 properties, for example, you'll have to run 21 queries to get all properties. This value might change in the future, do not write code that expects the page size to be 50.

To get the first page, send null as the cursor argument or apply no cursor at all, like so:

```graphql
query {
  paginatedProperties(cursor: null) {
    cursor
    page {
      reference
    }
  }
}
```

You'll get something like this in the response:

```json
{
  "data": {
    "paginatedProperties": {
      "cursor": "g3QAAAABZAAIcmVmZXJlbnptAAAABTEzMjIw",
      "page": [
        {
          "reference": "12004"
        }
        ...
      ]
    }
  }
}
```

To fetch the next page, use the received cursor string in the cursor argument:

```graphql
query {
  paginatedProperties(cursor: "g3QAAAABZAAIcmVmZXJlbnptAAAABTEzMjIw") {
    cursor
    page {
      reference
    }
  }
}
```

## Schema Documentation

We run a [reference server](https://demo.garaio-rem.net/external/graphql/graphiql) where you can explore the queries and mutations. If you want to extract the schema definition, use one of the many avaliable tools against <https://demo.garaio-rem.net/external/graphql>. Be aware some tools like Insomnia need the graphiql endpoint <https://demo.garaio-rem.net/external/graphql/graphiql> and some other tools like graphql playground not.
