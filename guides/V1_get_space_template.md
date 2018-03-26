---
copyright: 'Copyright IBM Corp. 2018'
link: 'get-space-template'
is: 'experimental'
---

# Get Space Template

A user can fetch details of a space template by passing its id to the _spaceTemplate_ query, provided the user either created
the template or is subscribed to the offering with which the template is associated.

## Schema

### Fetch A Space Template

```graphql
type QueryRoot {
  ...
  spaceTemplate(id: ID!): SpaceTemplate
}
```

## Example request

~~~~
Method: POST
URL: https://api.watsonwork.ibm.com/graphql
Headers: 'Content-Type: application/graphql' , 'x-graphql-view: PUBLIC, EXPERIMENTAL'
Body:
{
  spaceTemplate(id: "template-id") {
    name
    requiredApps {
      items {
        id
      }
    }
    properties {
      items {
        id
        type
        displayName
        ... on SpaceListProperty {
          defaultValue
          acceptableValues {
            id
            displayName
          }
        }
        ... on SpaceTextProperty {
          defaultValue
        }
        ... on SpaceBooleanProperty {
          defaultStringValue
        }
      }
    }
    spaceStatus {
      defaultValue
      acceptableValues {
        id
        displayName
      }
    }
  }
}
~~~~

Sample output for the above request:
```json
{
  "data": {
    "spaceTemplate": {
      "name": "Template 1",
      "requiredApps": {
        "items": [
          {
            "id": "d0c246a0-bced-4bf4-a29d-99cc6ad1ad53"
          }
        ]
      },
      "properties": {
        "items": [
          {
            "id": "area-property",
            "type": "LIST",
            "displayName": "Area",
            "defaultValue": "other-bundle",
            "acceptableValues": [
              {
                "id": "supply-bundle",
                "displayName": "Supply"
              },
              {
                "id": "inventory-bundle",
                "displayName": "Inventory"
              },
              {
                "id": "other-bundle",
                "displayName": "Other"
              }
            ]
          },
          {
            "id": "public-property",
            "type": "BOOLEAN",
            "displayName": "Public",
            "defaultStringValue": "TRUE"
          },
          {
            "id": "summary-property",
            "type": "TEXT",
            "displayName": "Summary",
            "defaultValue": ""
          }
        ]
      },
      "spaceStatus": {
        "defaultValue": "new-bundle",
        "acceptableValues": [
          {
            "id": "new-bundle",
            "displayName": "New"
          },
          {
            "id": "close-bundle",
            "displayName": "Close"
          }
        ]
      }
    }
  }
}
```

For more information see [Space Templates](../guides/V1_space_template_main.md)
