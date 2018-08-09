---
copyright: 'Copyright IBM Corp. 2018'
link: 'delete-space-template'
is: 'beta'
---

# Delete a Space Template

A user can delete a custom space template with the _deleteSpaceTemplate_ mutation.

## Schema

### Delete Space Template Mutation

```graphql
type MutationRoot {
  ...
  deleteSpaceTemplate(input: DeleteSpaceTemplateInput!): DeleteSpaceTemplateMutation
}
```

The _DeleteSpaceTemplateMutation_ returned has a single property, a boolean value indicating whether or not the delete operation was _successful_:

```graphql
type DeleteSpaceTemplateMutation {
  successful: Boolean!
}
```

The _DeleteSpaceTemplateInput_ likewise has only a single, required property, the _id_ of the space template to be deleted:

```graphql
type DeleteSpaceTemplateInput {
  id: String!
}
```

## Example request

~~~~
Method: POST
URL: https://api.watsonwork.ibm.com/graphql
Headers: 'Content-Type: application/graphql' , 'x-graphql-view: PUBLIC, BETA'
Body:
{
  mutation {
    deleteSpaceTemplate(input: {id: "my-custom-template-id"}) {
      successful
    }
  }
}
~~~~
