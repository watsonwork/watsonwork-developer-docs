---
copyright: 'Copyright IBM Corp. 2017'
link: 'search'
is: 'future'
---

# Search

Watson Work Services offers the ability to search for people, spaces, space members and space content (i.e., messages). The
objects returned by the respective search types are as detailed below.

## Person

| property             | type           | description                                                                                                                                |
|----------------------|:---------------|:-------------------------------------------------------------------------------------------------------------------------------------------|
| displayName          | String         | Display name of the person, intended for use in a user experience                                                                          |
| extId                | String         | External id for the person. This is a unique identifier.                                                                                   |
| email                | String         | The primary email address for this person                                                                                                  |
| photoUrl             | String         | The URL for the photo of the person, intended for use to visually represent user in a user experience                                      |
| customerId           | String         | The organization for this person                                                                                                           |
| created              | Date           | Date this person object was created                                                                                                        |
| updated              | Date           | Date this person object was last updated                                                                                                   |
| presence             | PresenceStatus | User’s presence status.  One of 'online' or 'offline'                                                                                      |
| type                 | String         | Either `"user"` or `"app"`                                                                                                                     |
| directMessageSpaceId | ID             | In the case of a person with whom you have an existing direct message conversation, the id of your direct messaging space with that person |

## Space Member

| property             | type           | description                                                                                                                                |
|----------------------|:---------------|:-------------------------------------------------------------------------------------------------------------------------------------------|
| displayName          | String         | Display name of the person, intended for use in a user experience                                                                          |
| extId                | String         | External id for the person. This is a unique identifier.                                                                                   |
| email                | String         | The primary email address for this person                                                                                                  |
| photoUrl             | String         | The URL for the photo of the person, intended for use to visually represent user in a user experience                                      |
| customerId           | String         | The organization for this person                                                                                                           |
| created              | Date           | Date this person object was created                                                                                                        |
| updated              | Date           | Date this person object was last updated                                                                                                   |
| presence             | PresenceStatus | User’s presence status.  One of 'online' or 'offline'                                                                                      |
| type                 | String         | Either `"user"` or `"app"`                                                                                                                     |
| roles | List<Role>             | The roles the user has in the target space |
| permissions | List<String>             | The permissions the user has in this space |

## Space

| property                                                      | type             | description                                                                                                                                                                                                                                                                                                                                                          |
|---------------------------------------------------------------|:-----------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| title                                                         | String           | The title of the space                                                                                                                                                                                                                                                                                                                                               |
| created                                                       | Date             | Date this space  was created                                                                                                                                                                                                                                                                                                                                         |
| updated                                                       | Date             | Date this space was updated                                                                                                                                                                                                                                                                                                                                          |
| id                                                            | ID               | The unique ID for this space. The ID scalar type represents a unique identifier, often used to refetch an object or as key for a cache. The ID type appears in a JSON response as a String; however, it is not intended to be human-readable. When expected as an input type, any string (such as "4") or integer (such as 4) input value will be accepted as an ID. |
| members(before: String, after: String, first: Int, last: Int) | PersonCollection | The members of this space provided as a PersonCollection                                                                                                                                                                                                                                                                                                             |
| membersUpdated                                                | Date             | The date the membership was updated                                                                                                                                                                                                                                                                                                                                  |
| conversation                                                  | Conversation     | The conversation object for this space                                                                                                                                                                                                                                                                                                                               |
| createdBy                                                     | Person           | The person who created this space                                                                                                                                                                                                                                                                                                                                    |
| updatedBy                                                     | Person           | The person who updated this space                                                                                                                                                                                                                                                                                                                                    |

## MessageSearchResult

| property   | type         | description                                               |
|------------|:-------------|:----------------------------------------------------------|
| message    | Message      | A conversation message                                    |
| highlights | \[Highlight] | Highlighted snippets of content matching the search query |
| space      | Space        | The space in which the message was posted                 |

### Message

| property    | type      | description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|-------------|:----------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| content     | String    | The body of the message                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| contentType | String    | Mime type of the message content                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| annotations | \[String] | A set of optional objects/attachments that are added to a message, called annotations. Each annotation represents meta data that are related to the message. An annotation is represented by a structured format, which can be viewed as a template. There are different annotation types. Some are used to store results of cognitive analysis of a message, for example. An annotation can be added at message create time or later, as an update.  Apps are currently limited to create only one type of annotation called `generic` |
| created     | Date      | Date this message  was created                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| updated     | Date      | Date this message  was updated                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| id          | ID        | The ID of the message. The ID scalar type represents a unique identifier, often used to refetch an object or as key for a cache. The ID type appears in a JSON response as a String; however, it is not intended to be human-readable. When expected as an input type, any string (such as "4") or integer (such as 4) input value will be accepted as an ID.                                                                                                                                                                           |
| createdBy   | Person    | The person who created this message                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| updatedBy   | Person    | The person who updated this message                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |

### Highlight

| property    | type      | description                               |
|-------------|:----------|:------------------------------------------|
| field       | String    | The field containing the matching content |
| highlighted | \[String] | Highlighted snippets of matching content  |
