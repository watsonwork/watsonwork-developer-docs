---
copyright: 'Copyright IBM Corp. 2018'
link: 'update-meeting-settings'
is: 'experimental'
---

# Update a meeting

## Concepts

The _updateMeetingSettings_ mutation allows the API caller to configure options on the meeting.  The mutation accepts a Space ID (spaceId), and an allowPublic boolean as arguments, and makes the request on behalf of the caller, updating the meeting within the specified space.  The result will reflect the whether the call was accepted for processing by the service.

## Schema

### Update Meeting Settings Mutation



```graphql
type MutationRoot {
  ...
  updateMeetingSettings(input: UpdateMeetingSettingsInput!): MeetingSettingsMutationOutput
}

type UpdateMeetingSettingsInput {
  spaceId: ID!
  allowPublic: Boolean!
}

type MeetingSettingsMutationOutput {
  accepted: Boolean!
}
```
## Field definitions

# UpdateMeetingSettingsInput
|Name|Description|Schema|
|---|---|---|---|
|**spaceId**|Space ID of the space for which the meeting should be updated|**String** <br>_required_|
|**allowPublic**|Whether or not non-space members can join meetings started in the space|**Boolean** <br>_required_|

# MeetingSettingsMutationOutput
|Name|Description|Schema|
|---|---|---|---|
|**accepted**|Whether the request to update the meeting was accepted for processing|**Boolean** <br>_required_|


## Example Request

~~~~
Method: POST
URL: https://api.watsonwork.ibm.com/graphql
Headers: 'Content-Type: application/graphql' , 'x-graphql-view: PUBLIC, EXPERIMENTAL'
Body:
{
  mutation {
    updateMeetingSettings(input: {spaceId : "5ad0fabfe4b078066d690a24", allowPublic: true}) {
      accepted
    }
  }
}
~~~~
## Example Result

~~~~
{
  "data": {
    "updateMeetingSettings": {
      "accepted": "true"
    }
  }
}
~~~~

Try it out with our GraphQL tool - <a href="https://developer.watsonwork.ibm.com/tools/graphql?apiType=experimental&query=mutation%20updateMeetingSettings%20{%20%20updateMeetingSettings(input: {spaceId:%20%22space-id%22,%20allowPublic:%20true})%20{%20%20%20%20accepted%20%20}}" target="_blank">Update meeting settings</a>
