---
copyright: 'Copyright IBM Corp. 2018'
link: 'get-space-template'
is: 'experimental'
---

# Get Space Template

A user can fetch details of a space template by passing its id to the _spaceTemplate_ query, provided the user either created
the template or is subscribed to the offering with which the template is associated.

## Schema

### Fetch A Space Template

```graphql
type QueryRoot {
  ...
  spaceTemplate(id: ID!): SpaceTemplate
}
```

## Example request

~~~~
Method: POST
URL: https://api.watsonwork.ibm.com/graphql
Headers: 'Content-Type: application/graphql' , 'x-graphql-view: PUBLIC, EXPERIMENTAL'
Body:
{
  spaceTemplate(id: "template-id") {
    name
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
    spaceStatus {
      defaultValue
      acceptableValues {
        id
        displayName
      }
    }
  }
}
~~~~

For more information see [Space Templates](../guides/V1_space_template_main.md)
