---
copyright: 'Copyright IBM Corp. 2017, 2018'
link: 'conversation'
is: 'published'
---
# Conversation

A conversation is where people come together and send and receive messages - the conversation also is where
apps can provide interaction with the people in the conversation. It's the main collaboration area.

Watson Work Services represents a Conversation with this object.

| property      | type          | description  |
| ------------- |:------------- |:-----|
| id          | ID      | The ID of the Conversation. The ID scalar type represents a unique identifier, often used to refetch an object or as key for a cache. The ID type appears in a JSON response as a String; however, it is not intended to be human-readable. When expected as an input type, any string (such as "4") or integer (such as 4) input value will be accepted as an ID.|
| created     | Date        | The date that the space for this conversation was created at|
| createdBy   | Person    | The person who created the space for this conversation |
| updated     | Date    | The date that the space for this conversation  was updated at|
| updatedBy   | Person | The person who updated the space for this conversation  |
| messages(oldestTimestamp: Long, mostRecentTimestamp: Long, annotationType: String, before: String, after: String, first: Int, last: Int, includeSoftDeleted: Boolean) | MessageCollection | The messages of this conversation provided as a MessageCollection. |
