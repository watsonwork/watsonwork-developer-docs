---
copyright: 'Copyright IBM Corp. 2017'
link: 'space-roles-admin'
is: 'future'
---
# APIs for administering a space

### Roles in a space
___

A SpaceRole defines the control a set of users has in that space based on their role. For example, the users with the SpaceRole SPACE_OWNER can delete the space. These are the types for the SpaceRole field in graphql.

| SpaceRole   | Description              |
|:------------|:-------------------------|
| SPACE_OWNER | Identifies a space owner |


### Transferring the ownership of a space
___

To transfer the ownership of a space, you need to use a mutation which will remove the SpaceRole "SPACE_OWNER" from one user and add it to another user. You need to specify the target user who will receive the SpaceRole "SPACE_OWNER", this user must already be a member of the space. The user who is making this call, the requestor, must have the SpaceRole "SPACE_OWNER" and will have their SpaceRole "SPACE_OWNER" removed.

#### Making the request

The input type used `SpaceTransferOwnerInput!` It must not be null and have the non null fields `spaceId` and `targetUserId`.

```
mutation{
  transferMySpaceOwnership(input: {spaceId:"spaceid", targetUserId: "id of new owner"}){
    spaceId
    members {
      id
      roles
    }
  }
}
```

#### Mutation properties

| property     | type   | description                                                 |
|:-------------|:-------|:------------------------------------------------------------|
| spaceId      | String | ID for the target space where ownership will be transferred |
| targetUserId | String | ID of the user that will become SPACE_OWNER                 |

#### Response Fields
| field        | type                | description                                                                                                       |
|:-------------|:--------------------|:------------------------------------------------------------------------------------------------------------------|
| spaceId      | String              | ID of the modified space                                                                                          |
| members      | SpaceTransferMember | The members updated from the mutation with userId and updated roles. Updated Request User and Updated Target User |
| member.id    | String              | User Id of one of the updated users                                                                               |
| member.roles | SpaceRole           | The updated role set for the user                                                                                 |

#### Errors

If an invalid space id is sent, a 404 error message will be returned.

If the user making the request is not a member of the space, or does not have owner role, or where the target user is not a member of the space, a 403 error message will be returned.



### Add a role to a user in a space
___

To add a role to a member of a space, you need to use a mutation. You need to specify the target user who will receive the SpaceRole that is specified in the mutation, and this user must already be a member of the space. Note that the requester must have the same SpaceRole as they are attempting to grant. This will grant the user permissions to perform actions associated with the given role within this space.

#### Making the request

The input type used is `SpaceRoleInput!`. It must not be null and have the non-null fields `spaceId`, `memberId` and `spaceRole`.

```
mutation {
  addSpaceMemberRole(input: {spaceId: "spaceid", memberId: "memberId", spaceRole: "accepted role"}) {
    spaceId
    members {
      id
      roles
    }
  }
}
```

#### Mutation properties

| property  | type   | description                                                                               |
|:----------|:-------|:------------------------------------------------------------------------------------------|
| spaceId   | String | ID for the target space where the member specifed is having the specified SpaceRole added |
| memberId  | String | ID of the user that will receive the sent SpaceRole                                       |
| spaceRole | String | The role to be assigned to the target user                                                |

#### Response Fields
| field        | type                | description                                                                              |
|:-------------|:--------------------|:-----------------------------------------------------------------------------------------|
| spaceId      | String              | ID of the modified space                                                                 |
| members      | SpaceTransferMember | The members updated from the mutation with userId and updated roles. Updated Target User |
| member.id    | String              | User Id of one of the updated user                                                       |
| member.roles | SpaceRole           | The updated role set for the user                                                        |

#### Errors

If an invalid space id is sent, a 404 error message will be returned.

If the user making the request is not a member of the space, or does not have the SpaceRole being specified, or where the target user is not a member of the space, a 403 error message will be returned.



### Remove a role from a user in a space

___

To remove a role from a member of a space, you need to use a mutation. You need to specify the target user who will have the SpaceRole that is specified in the mutation removed. This user must already be a member of the space. Note that the requester must have the same SpaceRole as they are attempting to remove. This will revoke a users permissions to perform the actions associated with the given role within this space.

#### Making the request

The input type used is `SpaceRoleInput!`. It must not be null and have the non-null fields `spaceId`, `memberId` and `spaceRole`.

```
mutation {
  removeSpaceMemberRole(input: {spaceId: "spaceid", memberId: "memberId", spaceRole: "removed role"}) {
    spaceId
    members {
      id
      roles
    }
  }
}
```

#### Mutation properties

| property  | type   | description                                                                                  |
|:----------|:-------|:---------------------------------------------------------------------------------------------|
| spaceId   | String | ID for the target space where the member specified is having the specified SpaceRole removed |
| memberId  | String | ID of the user that will have the sent SpaceRole removed                                     |
| spaceRole | String | The role to be removed from the target user                                                  |

#### Response Fields
| field        | type                | description                                                                              |
|:-------------|:--------------------|:-----------------------------------------------------------------------------------------|
| spaceId      | String              | ID of the modified space                                                                 |
| members      | SpaceTransferMember | The members updated from the mutation with userId and updated roles. Updated Target User |
| member.id    | String              | User Id of one of the updated user                                                       |
| member.roles | SpaceRole           | The updated role set for the user                                                        |

#### Errors

If an invalid space id is sent, a 404 error message will be returned.

If the user making the request is not a member of the space, or does not have the SpaceRole being specified, or where the target user is not a member of the space, a 403 error message will be returned.

Users can remove a SpaceRole for other users only if the user making the call has the SpaceRole being specified.. For example a user with the SpaceRole SPACE_OWNER can remove the SpaceRole SPACE_OWNER from another member of the same space.
