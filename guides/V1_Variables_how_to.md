---
copyright: 'Copyright IBM Corp. 2017'
link: 'what-are-variables'
is: 'published'
---
## What are Variables

Variables are a powerful concept in GraphQL that allows to reuse a query passing different values as the parameters of the datafetchers
(Datafetchers are methods in the schema that can retrieve data from other sources).

There are many benefits of using variables. The most obvious benefit is that it is a DRY (Don’t Repeat Yourself) approach which allows to
reuse the same query for multiple uses. Another benefit is that it allows to use some client side libraries like Relay or Apollo, which
build upon the use of variables. Some other additional benefits of using variables is that it allows to collect metrics around how many times
a particular query has been used (even if with different values), it might make caching easier and so on.

## How to use variables

In order to use variables we need to use the `Content-type: application/json` instead of `Content-type: application/graphql`.

The format of the json object when using that content type and sending variables is:

```json
{
  "query": "",
  "variables": {}
}
```

You can optionally add the `operationName`. In that case the format would be like this:


```json
{
  "operationName": "",
  "query": "",
  "variables": {}
}
```

An example query using variables could be:

```json
{
  "operationName": "getUser",
  "query": "query getUser($email: String){     person(email: $email) { id displayName  }  }",
  "variables": {"email": "username@domain.com"}
}
```

You can also send the variables as a stringified json, like this:

```json
{
  "operationName": "getUser",
  "query": "query getUser($email: String){     person(email: $email) { id displayName  }  }",
  "variables": "{\"email\": \"username@domain.com\"}"
}
```
