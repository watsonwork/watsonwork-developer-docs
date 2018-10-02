---
copyright: 'Copyright IBM Corp. 2017'
link: 'focus-annotation'
is: 'published'
---
## Focus Annotation
Let’s break down the annotation structure for a `focus`.  For each message, the text is broken into sentences, and an annotation is created for every identified `focus` within a sentence.  The category is an optional field which further refines the `lens`.

This is an annotation containing a `focus` identified by the `Commitment` lens.
````json
{
  "type":"message-focus",
  "lens":"Commitment",
  "focusVersion":2,
  "annotationId":"580fa6b2e4b0fad7dded220d",
  "created":1477420722906,
  "createdBy":"toscana-aip-nlc-consumer-client-id",
  "start":48,
  "end":82,
  "phrase":"We will put back next week likely.",
  "confidence":0.6648085353262561,
  "extractedInfo":{
    "entities":[],
    "keywords":[],
    "dates":[
      {
        "date":"2016-10-30T00:00:00.000",
        "text":"next week"
      }
    ]
  }
}
````

This is an annotation containing a `focus` identified by the Question lens.
````json
{
  "type":"message-focus",
  "lens":"Question",
  "focusVersion":2,
  "annotationId":"58112d5ee4b0aeaa85d597ae",
  "created":1477520734799,
  "createdBy":"toscana-aip-nlc-consumer-client-id",
  "start":0,
  "end":36,
  "phrase":"William - how is that issue you have?",
  "confidence":0.9495088951743085,
  "extractedInfo":{
    "entities":[
      {
        "count":1,
        "relevance":0.33,
        "text":"William",
        "type":"Person"
      }
    ],
    "keywords":[
      {
        "relevance":0.953778,
        "text":"blank page bug"
      },
      {
        "relevance":0.394388,
        "text":"William"
      }
    ],
    "dates":[]
  }
}
````

The focus annotation is the structure added as an annotation to a message when a `focus` is found in that message. The definition of the focus annotation references several other structures detailed below.

See also [Annotation](../guides/V1_annotations.md) for information on common annotation fields.

| property      | type          | description  |
| ------------- |:------------- |:------------ |
| type          | String        | For a focus annotation, the type will be _message-focus_. |
| lens          | String        | One of _ActionRequest_, _Question_, and _Commitment_. Watson Work may add lenses at any time, and clients should not depend upon only receiving this set of lenses. |
| category      | String        | Only ActionRequest currently uses _categories_. These categories are _Schedule_ and _Share_. Watson Work Services may add categories at any time, and clients should not depend upon only receiving this set of categories.
| focusVersion  | String        | The schema version for this focus |
| start         | Number        | An inclusive index for the focus’s start location in the message’s original content (including markdown). In some cases, start and end may be omitted, in which case clients should consider the entire message as the focus. |
| end           | Number        | An exclusive index for the focus’s end location in the message’s original content (including markdown). In some cases, start and end may be omitted, in which case clients should consider the entire message as the focus. |
| phrase        | String        | The plaintext of the passage identified as the focus and classified as the given lens/category (disregarding markdown). In some cases, phrase may be omitted, in which case clients may consider the entire message as the focus or, where feasible, consider the start and end indexes to understand the area within the message designated as the focus. |
| confidence    | Number        | A decimal value between 0 and 1 denoting how confident the service is in assigning the specified class to the phrase |
| extractedInfo | FocusExtractedInfo | Information extracted from the focus |

### FocusExtractedInfo

`FocusExtractedInfo` contains extracted information which is relevant to the `focus`.

| property      | type          | description  |
| ------------- |:------------- |:------------ |
| entities      | [FocusEntity] | An array of entities found in the focus |
| keywords      | [FocusKeyword]| An array of keywords found in the focus |
| dates         | [FocusDate]   | An array of dates found in the focus |

### FocusEntity

| property      | type          | description  |
| ------------- |:------------- |:------------ |
| count         | String        | The number of occurrences of the entity in the focus |
| relevance     | Number        | The entity’s relevance to the focus |
| text          | String        | The text referencing the entity |
| type          | String        | A category or type of the entity, such as Person or Organization. |

### FocusKeyword

| property      | type          | description  |
| ------------- |:------------- |:------------ |
| relevance     | String        | The keyword’s relevance to the focus |
| text          | String        | The text of the keyword |

### FocusDate

| property      | type          | description  |
| ------------- |:------------- |:------------ |
| date          | String        | A string representation of the Date using ISO 8601 |
| text          | String        | The text containing the date reference |
