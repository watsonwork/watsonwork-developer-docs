---
copyright: 'Copyright IBM Corp. 2017'
link: 'space'
is: 'published'
---
# Space

In Watson Work Services a space is the place where people come together to collaborate.
It represents the container for the people who are collaborating, and it contains the resources people
use to engage in collaboration - for example a space holds the conversation, which is where people exchange messages.

Watson Work Services represents a Space with this object.

| property      | type          | description  |
| ------------- |:------------- |:-----|
| id          | ID      | The unique ID for this space. The ID scalar type represents a unique identifier, often used to refetch an object or as key for a cache. The ID type appears in a JSON response as a String; however, it is not intended to be human-readable. When expected as an input type, any string (such as "4") or integer (such as 4) input value will be accepted as an ID.|
| created     | Date        | Date this space  was created |
| createdBy   | Person    | Person who created this space |
| updated     | Date    | Date this space  was updated |
| updatedBy   | Person | Person who updated this space  |
| title      | String        | The title of the space |
| description         | String        | The description of the space |
| members(before: String, after: String, first: Int, last: Int) | PersonCollection | The members of this space provided as a PersonCollection
| membersUpdated | Date | The date the membership was updated |
| conversation |Conversation | The conversation object for this space |
