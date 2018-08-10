---
copyright: 'Copyright IBM Corp. 2018'
link: 'team-space-templates'
is: 'future'
---

# Get Team Space Templates

Some space templates are associated with particular teams. 
Using the **teamSpaceTemplates** query, a user with the appropriate permission (determined by the offering to which they are subscribed) can fetch a collection of the templates curated by their team admin.

## Schema

### Fetch Team Space Templates

```graphql
type QueryRoot {
  ...
  teamSpaceTemplates(teamId: String!): SpaceTemplateCollection
}
```

## Example request

~~~~
Method: POST
URL: https://api.watsonwork.ibm.com/graphql
Headers: 'Content-Type: application/graphql' , 'x-graphql-view: PUBLIC, FUTURE'
Body:
{
  teamSpaceTemplates(teamId: "myTeamId") {
    items {
      id
    }
  }
}
~~~~

For more information see [Space Templates](../guides/V1_space_template_main.md)