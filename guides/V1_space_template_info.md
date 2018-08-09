---
copyright: 'Copyright IBM Corp. 2018'
link: 'space-template-info'
is: 'beta'
---

# Space Template Info

A number of additional properties of a _Space_ object are exposed when you add `BETA` to the `x-graphql-view` header.

```graphql
type Space {
...
  templateInfo: SpaceTemplateInfo
  statusValueId: String
  propertyValueIds: [SavedPropertyIds]
}
```

You can add _templateInfo_ to your _space_ request in order to fetch information about the template associated with the space.

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

The information returned by _templateInfo_ can be used to interpret _statusValueId_ and _propertyValueIds_.

_statusValueId_ represents the current status value assigned to the space in the form of an ID. The _displayName_ associated with that ID can be obtained by looking at the _acceptableValues_ for the _spaceStatus_ as listed under _templateInfo_.

```graphql
type SpaceStatus {
...
  acceptableValues: [SpaceStatusAcceptableValue]
}

type SpaceStatusAcceptableValue {
...
  id: ID!
  displayName: String!
}
```

_propertyValueIds_ lists the IDs of the properties of the space and the values currently assigned to each.

```graphql
type SavedPropertyIds {
  propertyId: String
  propertyValueId: String
}
```

The _displayName_ associated with each property ID can be obtained by looking at the collection of _properties_ listed under _templateInfo_.

```graphql
type SpacePropertyCollection {
  items: [SpaceProperty]!
}

interface SpaceProperty {
...
  id: ID!
  displayName: String!
}
```

In the case of text and boolean properties, the _propertyValueId_ displayed will be a straightforwardly readable value. In the case of list properties, the value will be an ID; the display name associated with the ID can be obtained by looking at the _acceptableValues_ for the property under _templateInfo_.

```graphql
type SpaceListProperty implements SpaceProperty {
...
  acceptableValues: [SpaceListPropertyAcceptableValue]!
}

type SpaceListPropertyAcceptableValue {
...
  id: ID!
  displayName: String!
}
```

Try adding these fields to a _space_ query in <a href="https://developer.watsonwork.ibm.com/tools/graphql?apiType=experimental" target="_blank">our GraphQL Explorer</a>.
