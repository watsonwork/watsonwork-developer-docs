---
copyright: 'Copyright IBM Corp. 2018'
link: 'my-space-templates'
is: 'experimental'
---

# Get My Space Templates

Using the _mySpaceTemplates_ query, a user can fetch a collection of the space templates that they have created.

## Schema

### Fetch My Space Templates

```graphql
type QueryRoot {
  ...
  mySpaceTemplates: SpaceTemplateCollection!
}
```

## Example request

~~~~
Method: POST
URL: https://api.watsonwork.ibm.com/graphql
Headers: 'Content-Type: application/graphql' , 'x-graphql-view: PUBLIC, EXPERIMENTAL'
Body:
{
  mySpaceTemplates {
    items {
      id
    }
  }
}
~~~~

For more information see [Space Templates](../guides/V1_space_template_main.md)
