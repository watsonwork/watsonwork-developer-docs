---
copyright: 'Copyright IBM Corp. 2018'
link: 'reacting-users'
is: 'future'
---

# Query for Users Reacting to a Message

## Concepts

The _reactingUsers_ query allows the user to get all users who reacted to a message with a specified reaction.  The query accepts a Message ID (targetId) and a reaction as arguments, and optional paging information.


## Schema

### Reacting Users Query



```graphql
type QueryRoot {
  ...
reactingUsers(targetId: ID!, reaction: String!, before: String, after: String, first: Int, last: Int): ReactingUserCollection}

type ReactingUser {
  reacted: Date
  user: Person
}

type ReactingUserCollection {
  totalCount: Int
  pageInfo: PageInfo!
  items: [ReactingUser]!
}

```

## Example Request

~~~~
Method: POST
URL: https://api.watsonwork.ibm.com/graphql
Headers: 'Content-Type: application/graphql' , 'x-graphql-view: PUBLIC, EXPERIMENTAL'
Body:
{
  query {
    reactingUsers(targetId: "5a9ee86ee4b0cb1ca3dfef33", reaction: "?") {
      totalCount
      items {
        user {
          email
          displayName
          id
        }
        reacted
      }
      pageInfo {
        hasNextPage
        hasPreviousPage
        endCursor
        startCursor
      }
    }
  }
}
~~~~
