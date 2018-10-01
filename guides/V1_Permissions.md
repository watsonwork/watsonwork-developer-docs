---
copyright: 'Copyright IBM Corp. 2017'
link: 'permissions'
is: 'beta'
---

# Permissions

API calls to Watson Workspace are authenticated by requiring an identity to be included as part of the call.  Identities are granted permissions which control what they can do.  This is true regardless of whether the API call is made from the command line with a tool like curl, or from the Watson Workspace UI in a browser or a mobile client.

Permissions are represented as a set of strings which can be empty, e.g. for logging in, or have one ore more entries.  For example the API endpoint for [inbound webhooks](../references/V1_InboundWebhooks.yml) that lets you create a new message in a space is guarded by the permission `message_create`.  That means, that if you call this API endpoint but don’t have the `message_create` permission, an error would be the result: 403, Forbidden.

## Granting Permissions
Permissions are granted in several different ways:
 - when a user account is created
 - when an app is created
 - when a user or an app is added to a space
 - when an app acts on behalf of a user

Apps have a base set of permissions that allows them to perform some actions that are not related to spaces, for example accessing their own profiles. However, all the access that an app is given in a space, has to be explicitly granted to the app when it is added to a space. Users can have different permissions based on their subscriptions, roles and so forth. When an app is granted access to act on behalf of a user, the user’s permissions are limited to the ones that are approved by the user to be used by apps.

When you, as a developer, register an app with Watson Work Services, you define what permissions are required by your app.  When a user adds the app to a space, the list of permissions is displayed in human readable form and the user can either proceed and grant these permissions or stop the process and not add the app.

You have similar control over the set of permissions that your app will be granted when it acts on behalf of a user, for example when the app posts messages in the name of the user.  During the OAuth authentication process, the permissions are displayed to the user, again in human readable form and again the user can either proceed or abort the process.

These two sets of permissions are associated with your app when you register it with Watson Work Services.

# Permissions for Apps

**Valid permissions for Apps (`permissionTemplate`)**

| description                            | permission name   |
| ---                                    | ---               |
| Contribute messages to a conversation  | `message_create`  |
| Access to messages in a conversation   | `message_read`    |
| Access transcript of a conversation    | `transcript_read` |
| Access to membership in a space        | `membership_list` |
| Download files from a space            | `file_download`   |
| Upload files to a space                | `file_upload`     |
| Manage spaces (membership, title, etc) | `space_change`    |
| Read space details                     | `space_read`      |


**Valid permissions for Apps acting on behalf of a user (`scopeTemplate`)**

Includes all permissions for Apps from the table above.

| description                            | permission name   |
| ---                                    | ---               |
| Contribute messages to a conversation  | `message_create`  |
| Access to messages in a conversation   | `message_read`    |
| Access transcript of a conversation    | `transcript_read` |
| Access to membership in a space        | `membership_list` |
| Download files from a space            | `file_download`   |
| Upload files to a space                | `file_upload`     |
| Manage spaces (membership, title, etc) | `space_change`    |
| Read space details                     | `space_read`      |
| List spaces (that I am a member off)   | `space_list`      |
| Create spaces                          | `space_create`    |
| Read user profile                      | `profile_read`    |
| Update user profile                    | `profile_update`  |
| Read user settings                     | `settings_read`   |
| Update user settings                   | `settings_update` |
