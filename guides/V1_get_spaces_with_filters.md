---
copyright: 'Copyright IBM Corp. 2018'
link: 'get-a-filtered-list-of-spaces'
is: 'experimental'
---
## Get a filtered list of spaces

**NOTE**: The graphql filter parameters are currently in the `EXPERIMENTAL` release and are only available with the following http request header:

      x-graphql-view: EXPERIMENTAL

The spaces query supports querying spaces by visibility and membership in the experimental view. You can get a filtered list of spaces with the _getSpacesWithFilters_ GraphQL query.


### Discover New Spaces
Want to explore new frontiers and find new spaces? Discover spaces within your team that you can check out and join with a filtered query:

```graphql
query getSpacesWithFilters {
  spaces(filterMembership: NOT_MEMBER, filterVisibility: [TEAM]) {
    items {
      id
      title
      description
      membersUpdated
      members {
        items {
          email
          displayName
        }
      }
      conversation{
        messages{
          items {
            content
          }
        }
      }
    }
  }
}
```
See it in action with our GraphQL tool and get a filtered list of spaces. <a href="https://developer.watsonwork.ibm.com/tools/graphql?query=query%20getSpaces%20%7B%0A%20%20spaces(first%3A%2050)%20%7B%0A%20%20%20%20items%20%7B%0A%20%20%20%20%20%20title%0A%20%20%20%20%20%20id%0A%20%20%20%20%20%20description%0A%20%20%20%20%20%20membersUpdated%0A%20%20%20%20%20%20members%20%7B%0A%20%20%20%20%20%20%20%20items%20%7B%0A%20%20%20%20%20%20%20%20%20%20email%0A%20%20%20%20%20%20%20%20%20%20displayName%0A%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20conversation%20%7B%0A%20%20%20%20%20%20%20%20messages%20%7B%0A%20%20%20%20%20%20%20%20%20%20items%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20content%0A%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D%0A" target="_blank">Try it now</a>
