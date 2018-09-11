---
copyright: 'Copyright IBM Corp. 2018'
link: 'offering-space-templates'
is: 'beta'
---

# Get Offering Space Templates

Some space templates are associated with particular product offerings. 
Using the offeringSpaceTemplates query, a user can fetch a collection of the templates to which they have access by virtue of the offerings to which they are subscribed.

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
Headers: 'Content-Type: application/graphql' , 'x-graphql-view: PUBLIC, BETA'
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
