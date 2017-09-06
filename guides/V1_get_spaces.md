---
copyright: 'Copyright IBM Corp. 2017'
link: 'get-a-list-of-spaces'
is: 'published'
---
## Get a list of spaces

If you need info for more than one space work smarter, not harder. You can get information on a list of spaces with the _getSpaces_ GraphQL query.

```
query getSpaces {
  spaces(first: 50) {
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
See it in action with our GraphQL tool and get a list of spaces. <a href="https://developer.watsonwork.ibm.com/tools/graphql?query=query%20getSpaces%20%7B%0A%20%20spaces(first%3A%2050)%20%7B%0A%20%20%20%20items%20%7B%0A%20%20%20%20%20%20title%0A%20%20%20%20%20%20id%0A%20%20%20%20%20%20description%0A%20%20%20%20%20%20membersUpdated%0A%20%20%20%20%20%20members%20%7B%0A%20%20%20%20%20%20%20%20items%20%7B%0A%20%20%20%20%20%20%20%20%20%20email%0A%20%20%20%20%20%20%20%20%20%20displayName%0A%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20conversation%20%7B%0A%20%20%20%20%20%20%20%20messages%20%7B%0A%20%20%20%20%20%20%20%20%20%20items%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20content%0A%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D%0A" target="_blank">Try it now</a>
