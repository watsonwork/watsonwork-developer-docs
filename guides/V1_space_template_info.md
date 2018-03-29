---
copyright: 'Copyright IBM Corp. 2018'
link: 'space-template-info'
is: 'experimental'
---

# Space Template Info

In addition to those space properties documented publicly, you can add _templateInfo_ to your _space_ request in order to fetch
information about the template used to create a space.

## Schema

### Get Template Info

_templateInfo_ is a property of a _Space_ object which is exposed when you add `EXPERIMENTAL` to the `x-graphql-view` header.

```graphql
type Space {
...
  templateInfo: SpaceTemplateInfo
}
```

The _SpaceTemplateInfo_ object comprises a subset of the fields in the _Space Template_ type.

```graphql
type SpaceTemplateInfo {
  id: ID!
  name: String!
  description: String!
  spaceStatus: SpaceStatus!
  requiredApps: SpaceRequiredApplicationCollection
  properties: SpacePropertyCollection
  labelIds: [String]
  created: Date
  createdBy: Person
  updated: Date
  updatedBy: Person
}
```

## Example request

~~~~
Method: POST
URL: https://api.watsonwork.ibm.com/graphql
Headers: 'Content-Type: application/graphql' , 'x-graphql-view: PUBLIC, EXPERIMENTAL'
Body:
{
  space(id: "space-id") {
    title
    templateInfo {
      name
      description
      spaceStatus {
        defaultValue
        acceptableValues {
          id
          displayName
        }
      }
      requiredApps {
        items {
          id
        }
      }
      properties {
        items {
          id
          type
          displayName
          ... on SpaceListProperty {
            defaultValue
            acceptableValues {
              id
              displayName
            }
          }
          ... on SpaceTextProperty {
            defaultValue
          }
          ... on SpaceBooleanProperty {
            defaultStringValue
          }
        }
      }
    }
  }
}
~~~~

<a href="https://developer.watsonwork.ibm.com/tools/graphql?apiType=experimental&query=%7B%0A%20%20space(id:%20"space-id")%20%7B%0A%20%20%20%20title%0A%20%20%20%20templateInfo%20%7B%0A%20%20%20%20%20%20name%0A%20%20%20%20%20%20description%0A%20%20%20%20%20%20spaceStatus%20%7B%0A%20%20%20%20%20%20%20%20defaultValue%0A%20%20%20%20%20%20%20%20acceptableValues%20%7B%0A%20%20%20%20%20%20%20%20%20%20id%0A%20%20%20%20%20%20%20%20%20%20displayName%0A%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20requiredApps%20%7B%0A%20%20%20%20%20%20%20%20items%20%7B%0A%20%20%20%20%20%20%20%20%20%20id%0A%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20properties%20%7B%0A%20%20%20%20%20%20%20%20items%20%7B%0A%20%20%20%20%20%20%20%20%20%20id%0A%20%20%20%20%20%20%20%20%20%20type%0A%20%20%20%20%20%20%20%20%20%20displayName%0A%20%20%20%20%20%20%20%20%20%20...%20on%20SpaceListProperty%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20defaultValue%0A%20%20%20%20%20%20%20%20%20%20%20%20acceptableValues%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20id%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20displayName%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20...%20on%20SpaceTextProperty%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20defaultValue%0A%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20...%20on%20SpaceBooleanProperty%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20defaultStringValue%0A%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D" target="_blank">Try it now</a> in our GraphQL Explorer. Don't forget to replace the "space-id" argument with the ID of a real space.
