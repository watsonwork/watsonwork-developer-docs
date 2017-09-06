---
copyright: 'Copyright IBM Corp. 2017'
link: 'people'
is: 'published'
---
# People

Well, this is pretty obvious.  You and I are people.  Collaborative tools like Watson Workspace are all about enabling people to work together to achieve something awesome.  

A person has a photo, a name, and email address.  They can be mentioned and direct messaged, they send messages and share files.  They can be added and removed from a space.  You can tell if they are online or offline.

The Person object is defined as follows.

| property      | type          | description  |
| ------------- |:------------- |:-----|
| id          | ID      | The unique id for the Person. Note, the ID scalar type represents a unique identifier, often used to refetch an object or as key for a cache. The ID type appears in a JSON response as a String; however, it is not intended to be human-readable. When expected as an input type, any string (such as "4") or integer (such as 4) input value will be accepted as an ID.|
| created     | Date        | Date the Person object was created |
| createdBy   | Person    | Person who created the Person object - Person who added this person to Watson Work Services |
| updated     | Date    | Date the Person was last updated |
| updatedBy   | Person | Person who last updated the Person object |
| displayName   | String        | Name of the user as it displays in the user experience |
| extId         | String        | External id for the user, this is a unique identifier |
| email         | String        | The primary email address for the user |
| emailAddresses | [String]     | The array of additional email addresses for the user |
| photoUrl    | String        | The URL for the photo of the user, intended for display in the user experience |
| customerId  | String        | The organization for the user |
| presence  | PresenceStatus        | The user's current status, either 'online' or 'offline' |
| ibmUniqueID | String | Unique internal record identifier assigned when a user first obtains an IBMid (registered users only). Note that this id can be used to connect a Workspace user account to IBMid based accounts in other systems. |


Here's a breakdown of the APIs for each capability of the Person object.

| | REST APIs | Webhook APIs | GraphQL APIs |
|-------------------------|:------|:-----|:-----|
|Get user information     |||√|
|Get a list of users      |||√|
|Get my user details      |||√|
|Update space membership  |||√|
