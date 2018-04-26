---
copyright: 'Copyright IBM Corp. 2018'
link: 'create-space-from-template'
is: 'experimental'
---

# Create a Space from a Template

When you add `EXPERIMENTAL` to the `x-graphql-view` header, a number of additional properties are exposed in the _CreateSpaceInput_ object.

```graphql
input CreateSpaceInput {
...
  templateId: String
  propertyValues: [SpacePropertyValueInput]
}
```

If you set as _templateId_ the id of a template to which you have access, the space created will inherit the properties and apps configured as part of that template.

Values for the custom properties may be assigned using the _propertyValues_ field, which takes a list of _SpacePropertyValueInput_ objects.

```graphql
input SpacePropertyValueInput {
  propertyId: String!
  propertyValueId: String!
}
```

The _propertyId_ of the object identifies the property whose value is to be set and the _propertyValueId_ identifies the value to be assigned.
- In the case of a text property the _propertyValueId_ should simply be the string value you want to assign to the property.
- In the case of a boolean property the _propertyValueId_ should be one of the the upper-case strings "TRUE" or "FALSE".
- In the case of a list property the _propertyValueId_ should be the id of one of the acceptable values specified for the property.

Space properties may similarly be updated by adding a _propertyValues_ field as above to the input object passed to the _updateSpace_ mutation. Only those properties which you actually want to update need be included in this case. Properties for which no new values are specified will retain the values previously assigned.

When a space is created from a template it will be assigned the default status value defined in the template. The status of the space may subsequently be updated by adding a _statusValue_ field to the input object passed to the _updateSpace_ mutation. This field takes a _SpaceStatusValueInput_ object with a single _statusValueId_ property.

```graphql
input SpaceStatusValueInput {
  statusValueId: String!
}
```

The _statusValueId_ should be the id of one of the acceptable status values defined in the template.

Try creating and updating a space from a template in <a href="https://developer.watsonwork.ibm.com/tools/graphql?apiType=experimental" target="_blank">our GraphQL Explorer</a>.
