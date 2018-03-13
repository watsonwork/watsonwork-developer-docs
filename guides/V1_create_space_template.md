---
copyright: 'Copyright IBM Corp. 2018'
link: 'create-space-template'
is: 'experimental'
---

# Create a Space Template

A user can create a custom space template with the _createSpaceTemplate_ mutation.

## Schema

### Create Space Template Mutation

At a high level, the _createSpaceTemplate_ mutation looks like this.

```graphql
type MutationRoot {
  ...
  createSpaceTemplate(input: CreateSpaceTemplateInput!): SpaceTemplateMutation
}
```

The _SpaceTemplateMutation_ returned has a single property, the space template created:

```graphql
type SpaceTemplateMutation {
  spaceTemplate: SpaceTemplate
}
```

The input object has three required properties: template _name_ and _description_ strings, and a _spaceStatus_ input object.

The _SpaceStatusInput_ contains a list of acceptable statuses for spaces created using the template. Each _SpaceStatusAcceptableValueInput_ has a _displayName_ value and a boolean flag (defaulting to false) indicating whether this value should be the default status. If no default space status is specified then the first value provided will be taken as the default.

```graphql
type CreateSpaceTemplateInput {
  name: String!
  description: String!
  properties: SpacePropertiesInput
  spaceStatus: SpaceStatusInput!
  requiredApps: SpaceRequiredAppsInput
}

type SpaceStatusInput {
  acceptableValues: [SpaceStatusAcceptableValueInput]!
}

type SpaceStatusAcceptableValueInput {
  displayName: String!
  defaultValue: Boolean
}

```

Custom properties may optionally be added to the template by including a _properties_ field. The _SpacePropertiesInput_ object contains a list of wrapper objects, each containing a single property to be added to the template.

Properties to be added may be of three different types: text, boolean, or list.

```graphql
type SpacePropertiesInput {
  properties: [SpacePropertyWrapperInput]!
}

type SpacePropertyWrapperInput {
  listProperty: SpaceListPropertyInput
  textProperty: SpaceTextPropertyInput
  booleanProperty: SpaceBooleanPropertyInput
}
```

The _SpaceListPropertyInput_ object contains a _displayName_ for the property and a list of the _acceptableValues_. Each _SpaceListPropertyAcceptableValueInput_ has a _displayName_ for the value and a boolean flag (defaulting to false) indicating whether this value should be the default for the property. If no default value is specified then the first entry in the list will be taken as the default.

```graphql
type SpaceListPropertyInput {
  displayName: String!
  acceptableValues: [SpaceListPropertyAcceptableValueInput]!
}

type SpaceListPropertyAcceptableValueInput {
  displayName: String!
  defaultValue: Boolean
}

```

The _SpaceTextPropertyInput_ and _SpaceBooleanPropertyInput_ objects each contain a _displayName_ and _defaultValue_ for the property in question. If not specified, the default value for a text property will be an empty string and for a boolean property will be `false`.

```graphql
type SpaceTextPropertyInput {
  displayName: String!
  defaultValue: String
}

type SpaceBooleanPropertyInput {
  displayName: String!
  defaultValue: Boolean
}
```

Required apps may optionally be added to the template by including a _requiredApps_ field. The _SpaceRequiredAppsInput_ object contains a list of individual app input objects, each of which contains the ID of an app to be added.

```graphql
type SpaceRequiredAppsInput {
  apps: [SpaceRequiredAppInput]!
}

type SpaceRequiredAppInput {
  id: String!
}
```

## Example request

Below is an example request to create a space template, including sample space status values, a custom list property and required apps.

~~~~
Method: POST
URL: https://api.watsonwork.ibm.com/graphql
Headers: 'Content-Type: application/graphql' , 'x-graphql-view: PUBLIC, EXPERIMENTAL'
Body:
{
  mutation {
    createSpaceTemplate(input: {
      name: "Template 1"
      description: "A test template."
      spaceStatus: {
        acceptableValues: [
          {
            displayName: "New"
            defaultValue: true
          },
          {
            displayName: "Close"
          }
        ]
      }
      properties: {
        properties: [
          {
            listProperty: {
              displayName: "Area",
              acceptableValues: [
                {
                  displayName: "Supply",
                  defaultValue: true
                },
                {
                  displayName: "Inventory"
                }
              ]
            }
          }
        ]
      }
      requiredApps: {
        apps: [
          {
            id: "d0c246a0-bced-4bf4-a29d-99cc6ad1ad53"
          },
          {
            id: "e8c0e8ae-49cf-448d-a845-bb453f0bf94a"
          }
        ]
      }
    }) {
      spaceTemplate {
        id
      }
    }
  }
}
~~~~
