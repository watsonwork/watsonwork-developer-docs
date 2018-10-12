---
copyright: 'Copyright IBM Corp. 2018'
link: 'get-space-template'
is: 'beta'
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
Headers: 'Content-Type: application/graphql' , 'x-graphql-view: PUBLIC, BETA'
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

<div class="try-it-now">
  <a href="https://developer.watsonwork.ibm.com/tools/graphql?query=%7B%0A%20%20spaceTemplate(id:%20%22template-id%22)%20%7B%0A%20%20%20%20name%0A%20%20%20%20requiredApps%20%7B%0A%20%20%20%20%20%20items%20%7B%0A%20%20%20%20%20%20%20%20id%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%0A%20%20%20%20properties%20%7B%0A%20%20%20%20%20%20items%20%7B%0A%20%20%20%20%20%20%20%20id%0A%20%20%20%20%20%20%20%20type%0A%20%20%20%20%20%20%20%20displayName%0A%20%20%20%20%20%20%20%20...%20on%20SpaceListProperty%20%7B%0A%20%20%20%20%20%20%20%20%20%20defaultValue%0A%20%20%20%20%20%20%20%20%20%20acceptableValues%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20id%0A%20%20%20%20%20%20%20%20%20%20%20%20displayName%0A%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20...%20on%20SpaceTextProperty%20%7B%0A%20%20%20%20%20%20%20%20%20%20defaultValue%0A%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20...%20on%20SpaceBooleanProperty%20%7B%0A%20%20%20%20%20%20%20%20%20%20defaultStringValue%0A%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%0A%20%20%20%20spaceStatus%20%7B%0A%20%20%20%20%20%20defaultValue%0A%20%20%20%20%20%20acceptableValues%20%7B%0A%20%20%20%20%20%20%20%20id%0A%20%20%20%20%20%20%20%20displayName%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D" target="_blank">Try it now.</a>
</div>

Don’t forget to replace the "template-id" argument with the ID of a real template.

For more information see [Space Templates](../guides/V1_space_template_main.md)
