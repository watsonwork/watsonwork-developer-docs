---
copyright: 'Copyright IBM Corp. 2017'
link: 'graphql-api'
is: 'published'
---

## GraphQL API

**GraphQL** is an easy to use and very powerful method for minimizing round trips and eliminating over fetching of data.  Through a declarative query language using a JSON-like syntax over HTTP, you can request exactly the data you need across any number of micro-services and get back a tailored response in a single round trip. You get access to all the resources you need from Watson Work Services, bundled into a single request. This allows you to build high performing apps using the Watson Work Services Platform.

Here's a quick example to illustrate this. Let's say you wanted to request your first three spaces and their members.  The GraphQL query would look like this.  

```
query getSpaces {
  spaces(first: 3) {
    items {
      title
      members {
        items {
          displayName
        }
      }
    }
  }
}
```

The query is able to scan what would typically be multiple end points, and return back only the specific attributes you requested, in this case the title of each space, the members in those spaces, but only by their display name.

```
{
  "data": {
    "spaces": {
      "items": [
        {
          "title": "Support Team",
          "members": {
            "items": [
              {
                "displayName": "Kelvin Gifford"
              },
              {
                "displayName": "Michael Street"
              },
              {
                "displayName": "Jonas Rossi"
              }
            ]
          }
        },
        {
          "title": "Development Leads",
          "members": {
            "items": [
              {
                "displayName": "Charles Marron"
              },
              {
                "displayName": "Angie Dartmouth"
              },
              {
                "displayName": "Kelvin Gifford"
              },
              {
                "displayName": "Jonas Rossi"
              }
            ]
          }
        },
        {
          "title": "Platform Team",
          "members": {
            "items": [
              {
                "displayName": "Angus Smythe"
              },
              {
                "displayName": "Michael Street"
              },
              {
                "displayName": "Vern Schmidt"
              },
              {
                "displayName": "Jonas Rossi"
              }
            ]
          }
        }
      ]
    }
  }
}
```

The fact that this app could retrieve specific attributes in a single request is what's really awesome about GraphQL.

GraphQL provides more than queries too. You can create objects and make updates through mutations. With a **mutation** you create or update an object and then also tune the response, just as in a query, to get exactly what you want.

In this example, we are creating a space with the title, "Space title demo" and we are asking for the `id` and the `title` back as the space object.

```
mutation createSpace {
  createSpace(input: { title: "Space title demo"}){
    space {
      id
      title
    }
  }
}
```

And here's what is returned. Exactly what we asked for!

```
{
  "data": {
    "createSpace": {
      "space": {
        "id": "1234567890abcdef12345678",
        "title": "Space title demo"
      }
    }
  }
}
```

<p class="tip"><strong>TIP:</strong> Throughout the doc you'll see these buttons to "Try it now".  That means you can try the example code using our <a href="https://developer.watsonwork.ibm.com/tools/graphql">GraphQL Explorer</a>.  You can also browse the Watson Work Services data model and make your own GraphQL requests dynamically. Go ahead, run this mutation to create a space.</p>

<a href="https://developer.watsonwork.ibm.com/tools/graphql?query=mutation%20createSpace%20%7B%0A%20%20createSpace(input%3A%20%7Btitle%3A%20%22Space%20title%20demo%22%2C%20members%3A%20%5B%22%22%5D%7D)%20%7B%0A%20%20%20%20space%20%7B%0A%20%20%20%20%20%20id%0A%20%20%20%20%20%20title%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D%0A" target="_blank"> Try it now</a>

You can use the GraphQL endpoint with two different content types:
 - `Content-type: application/graphql`, documented [here:](../references/V1_graphql_raw.yml)
 - `Content-type: application/json`, documented [here:](../references/V1_graphql_json.yml)
