---
copyright: 'Copyright IBM Corp. 2018'
link: 'moment'
is: 'beta'
---
# Moment

**NOTE**: This graphql object is currently in `BETA` release and is only available with the following http request header:

      x-graphql-view: BETA

or with <a href="https://developer.watsonwork.ibm.com/tools/graphql?apiType=beta" target="_blank" >apiType=beta on the graphical GraphQL tool URL</a>.


Watson Work Services analyzes messages in each space to identify **moments**.

Each moment includes a summary of a group of messages. The summary includes summary phrases, participants, and other information extracted from messages.

Observers can catch up and understand the significance of activity that has transpired since their last visit, or use moments to get a glimpse into an ongoing discussion without reading all the messages.

Moments are automatically created as a conversation progresses.

The [Conversation](./guides/V1_conversation_main.md) object also references the collection of moments for that conversation, so in addition to dedicated queries for moments by their ID or by a space ID, you can query for moments in many places where you query for messages in conversations.

| property      | type          | description  |
| ------------- |:------------- |:-----|
| id | ID | The unique ID for this moment. The ID scalar type represents a unique identifier, often used to refetch an object or as key for a cache. The ID type appears in a JSON response as a String; however, it is not intended to be human-readable. |
| live | Boolean | The status whether this moment is still under updating |
| startTime | Date | Date and time this moment started |
| endTime | Date | Date and time this moment ended |
| keyMessage | Message | A messages which is most representative of the discussion in the moment |
| summaryPhrases | [SummaryPhrase] | The key phrases of the summary for this moment |
| participants | [Participant] | The participants of this moment |
| mentioned | [Mentioned] | Mentions of people in this moment |
| messages | MessageCollection | Filterable messages in this moment |
| space | Space | The space where the moment occurred |

## SummaryPhrase
### SummaryPhrase interface
| property      | type          | description  |
| ------------- |:------------- |:-----|
| label | String | The display string of this phrase |
| score | Float | The confidence of this phrase, if applicable |

### Keyword (implements SummaryPhrase)

The keyword interface is used to distinguish a keyword summary phrase, but currently adds no unique properties of its own.

### Entity (implements SummaryPhrase)
| property      | type          | description  |
| ------------- |:------------- |:-----|
| count | Int | The count of this entity phrase in the moment |


## Participant
| property      | type          | description  |
| ------------- |:------------- |:-----|
| user | Person | The user information of this participant |
| messageCount | Int | The total message count of this participant in this moment |
| viaAppUsers | AppUser | The extra user info from App participant, should be null for normal user |

### AppUser

If present, the AppUser represents information sent to Watson Work through the [actor fields when the message was created](./guides/V1_wwsg_Spaces.md).

| property      | type          | description  |
| ------------- |:------------- |:-----|
| displayName | String | The display name of this 3rd party App user |
| photoUrl | String | The photo url of this App user |
| url | String | The url of this App user |
