---
copyright: 'Copyright IBM Corp. 2018'
link: 'share-space-template'
is: 'experimental'
---

# Share a Space Template

A user can share one of their custom space templates with the _shareSpaceTemplate_ mutation.

## Schema

### Share Space Template Mutation
At a high-level the mutation looks like this:

```graphql
MutationRoot {
  shareSpaceTemplate(input: ShareSpaceTemplateInput!): ShareSpaceTemplateMutation!
}

type ShareSpaceTemplateInput {
  id: ID!
  target: ShareTarget!
}

enum ShareTarget {
  OPEN
}
```

The input has two required arguments, id and target. The id is the id of the template to be shared. The target denotes who the template is to be shared with. The only target currently available is OPEN, which means the template, once shared, is available to anyone who knows the template id and has permission to access openly shared templates. Once shared a template cannot be unshared.

In order to share a template you should be the creator of the template and all required apps in the template should already be shared
(see [Share an app](guides/V1_ShareAnApp.md) for additional information).


```graphql
type ShareSpaceTemplateMutation {
  successful: Boolean!
}
```

The mutation returns successful if the share operation succeeds.

## Example request

Below is an example request to share a space template.

~~~~
Method: POST
URL: https://api.watsonwork.ibm.com/graphql
Headers: 'Content-Type: application/graphql' , 'x-graphql-view: PUBLIC, EXPERIMENTAL'
Body:
mutation {
  shareSpaceTemplate(input: {id: "34c74efa-62eb-4475-afd0-e36b6bf0f515", target: OPEN}) {
    successful
  }
}
~~~~

## Workspace Share URL

Once shared, templates can be accessed in Workspace via a share URL.

The format of the workspace URL is
```
https://workspace.ibm.com/space/template/<templateId>
```
And to go directly into the create space flow is
```
https://workspace.ibm.com/space/create?template=<templateId>
```
