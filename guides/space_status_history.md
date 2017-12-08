---
copyright: 'Copyright IBM Corp. 2017'
link: 'space-status-history'
is: 'experimental'
---

# Space Status History

## Concepts

The _statusHistory_ field provides a list containing information about status changes 
in a space. The most recent value for each space status option is stored, ie. when a value is selected multiple times the old values are overwritten. 
For a new space initially the statusHistory will be empty. 
A statusHistory entry will be created when a user selects a new status value in the space.

The statusHistory data is eventually consistent and not synchronized with a status update.

## Schema

### Space Status History Fetcher

```grapqhl
query  {
  space(id: "space-id") {
    statusHistory {
      id
      updated
      updatedBy {
        id
      }
    }
  }
}
```

## Example Request

~~~~
Method: POST
URL: https://api.watsonwork.ibm.com/graphql
Headers: 'Content-Type: application/graphql' , 'x-graphql-view: PUBLIC, EXPERIMENTAL'
Body:
query  {
  space(id: "space-id") {
    statusHistory {
      id
      updated
      updatedBy {
        id
      }
    }
  }
}
~~~~


