---
copyright: 'Copyright IBM Corp. 2018'
link: 'offering-space-templates'
is: 'experimental'
---

# Get Offering Space Templates

A user can fetch their offering space templates. These are the templates associated with the offerings the user has.

## Schema

### Fetch Offering Space Templates

```graphql
type QueryRoot {
  ...
  offeringSpaceTemplates: SpaceTemplateCollection!
}
```


## Example request

~~~~
Method: POST
URL: https://api.watsonwork.ibm.com/graphql
Headers: 'Content-Type: application/graphql' , 'x-graphql-view: PUBLIC, EXPERIMENTAL'
Body:
{
  offeringSpaceTemplates {
    items {
      id
    }
  }
}
~~~~

For more information see [Space Templates](../guides/V1_space_template_main.md)