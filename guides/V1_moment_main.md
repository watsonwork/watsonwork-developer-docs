---
copyright: 'Copyright IBM Corp. 2017'
link: 'moment'
is: 'beta'
---
# Moment

**NOTE**: This graphql object is currently in `BETA` release and is only available with the following http request header:

      x-graphql-view: BETA

Watson Work Services analyzes messages in each space to identify **moments**.

Each moment includes a summary of a group of messages. The summary includes key phrases, participants, and other information extracted from messages.

Observers can catch up and understand the significance of activity that has transpired since their last visit, or use moments to get a glimpse into an ongoing discussion without reading all the messages.

Moments are automatically created as the chat in each space progresses. A moment is presented with this object.

| property      | type          | description  |
| ------------- |:------------- |:-----|
| id | ID | The unique ID for this moment. The ID scalar type represents a unique identifier, often used to refetch an object or as key for a cache. The ID type appears in a JSON response as a String; however, it is not intended to be human-readable. |
| live | Boolean | The status whether this moment is still under updating |
| startTime | Date | Date this moment is started |
| endTime | Date | Date this moment is ended |
| keyMessage | Message | The message which is identified as the most representative one in this moment |
| summaryPhrases | [SummaryPhrase] | The key phrases of the summary for this moment |
| participants | [Participant] | The participants of this moment |
| priority | UserPriorityStatus | Conveys information about the priority of this moment for this user |
| mentioned | [Mentioned] | Mentions in this moment |
| messages | MessageCollection | Messages in this moment |
| space | Space | The space where the moment is in |

### SummaryPhrase
###### SummaryPhrase interface
| property      | type          | description  |
| ------------- |:------------- |:-----|
| label | String | The display string of this phrase |
| score | Float | The confidence of this phrase |

###### Keyword (implements SummaryPhrase)

###### Entity (implements SummaryPhrase)
| property      | type          | description  |
| ------------- |:------------- |:-----|
| count | Int | The count of this entity phrase in the moment |


### Participant
| property      | type          | description  |
| ------------- |:------------- |:-----|
| user | Person | The user info of this participant |
| messageCount | Int | The total message count of this participant in this moment |
| viaAppUsers | AppUser | The extra user info from App participant, should be null for normal user |

###### AppUser
| property      | type          | description  |
| ------------- |:------------- |:-----|
| displayName | String | The display name of this 3rd party App user |
| photoUrl | String | The photo url of this App user |
| url | String | The url of this App user |


### UserPriorityStatus
| property      | type          | description  |
| ------------- |:------------- |:-----|
| predicted | Boolean | Whether this moment is a priority. The predicted field may be null if a prediction is not yet available. |
| support | [SupportingFeature] | Features which support the prediction made in this UserPriorityStatus. If a priority is predicted, each SupportingFeature is a personalized reason the system predicted the moment as a priority for the current user. If a priority is not predicted, each SupportingFeature is a personalized reason the system predicted the moment was not a priority. The SupportingFeatures may be null if not enough is known about the user to make a prediction. |

###### SupportingFeature
An abstract representation of something which supports a priority prediction. Implementing classes represent specific types of features.

| property      | type          | description  |
| ------------- |:------------- |:-----|
| category | PriorityFeatureType | The category of the support |

###### PriorityFeatureType
An enum of the category of the support.

| value | description |
|:------|:------ |
| USER_MARK | category for SupportingUserMark |
| PARTICIPANT | category for SupportingParticipant |
| PHRASE | category for SupportingPhrase |

###### SupportingUserMark (implements SupportingFeature)
Indicates the user has explicitly marked the item as a priority.

###### SupportingParticipant (implements SupportingFeature)
References a person that was meaningful to the priority prediction.

| property      | type          | description  |
| ------------- |:------------- |:-----|
| person | Person | The referenced person |

###### SupportingPhrase (implements SupportingFeature)
References a phrase that was meaningful to the priority prediction.

| property      | type          | description  |
| ------------- |:------------- |:-----|
| label | String | The referenced phrase |
