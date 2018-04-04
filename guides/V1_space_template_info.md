---
copyright: 'Copyright IBM Corp. 2018'
link: 'space-template-info'
is: 'experimental'
---

# Space Template Info

You can add _templateInfo_ to your _space_ request in order to fetch information about the template associated with the space.

_templateInfo_ is a property of a _Space_ object which is exposed when you add `EXPERIMENTAL` to the `x-graphql-view` header.

```graphql
type Space {
...
  templateInfo: SpaceTemplateInfo
}
```

The _SpaceTemplateInfo_ object comprises a subset of the fields in the _SpaceTemplate_ type.

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

Try adding _templateInfo_ to a _space_ query in <a href="https://developer.watsonwork.ibm.com/tools/graphql?apiType=experimental" target="_blank">our GraphQL Explorer</a>.
