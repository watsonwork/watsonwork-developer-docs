---
copyright: 'Copyright IBM Corp. 2017'
link: 'get-a-list-of-moments'
is: 'published'
---
## Get a list of moments

**NOTE**: This graphql object is currently in `BETA` release and is only available with the following http request header:

      x-graphql-view: BETA


This is a sample GraphQL query to get moments in a space. Be sure to switch "space-id" to the actual id you're curious about.

Additional optional parameters may be included as follows:
- `oldestTimestamp`: The minimum start time of moments.
- `mostRecentTimestamp`: The maximum start time of moments.
- `after`: The first cursor of `PageInfo`, must use together with `first`.
- `first`: The page size of `PageInfo`, could not use together with `last`.
- `before`: The last cursor of `PageInfo`, must use together with `last`.
- `last`: The page size of `PageInfo`, could not use together with `first`.
- `predicted`: Filter to moments which the system predicts are interesting or not for the current user based on their history. Omitting this param will query all moments.

```
query getMoments($spaceId: String!) {
  moments(spaceId: $spaceId) {
    items {
      id
      live
      startTime
      endTime
      keyMessage {
        id
        content
      }
      summaryPhrases(first: 3) {
        label
      }
      participants(first: 10) {
        user {
          id
          displayName
        }
        messageCount
        viaAppUsers {
          displayName
        }
      }
      priority {
        predicted
        support {
          category
          ... on SupportingParticipant {
            person {
              displayName
            }
          }
          ... on SupportingPhrase {
            label
          }
        }
      }
    }
  }
}

```

Get a list of moments in a space, see it in action with our GraphQL tool.

<div class="try-it-now">
      <a href="https://developer.watsonwork.ibm.com/tools/graphql?query=query%20getMoments(%24spaceId%3A%20String!)%20%7B%0Amoments(spaceId%3A%20%24spaceId)%20%7B%0Aitems%20%7B%0Aid%0Alive%0AstartTime%0AendTime%0AkeyMessage%20%7B%0Aid%0Acontent%0A%7D%0AsummaryPhrases(first%3A%203)%20%7B%0Alabel%0A%7D%0Aparticipants(first%3A%2010)%20%7B%0Auser%20%7B%0Aid%0AdisplayName%0A%7D%0AmessageCount%0AviaAppUsers%20%7B%0AdisplayName%0A%7D%0A%7D%0Apriority%20%7B%0Apredicted%0Asupport%20%7B%0Acategory%0A...%20on%20SupportingParticipant%20%7B%0Aperson%20%7B%0AdisplayName%0A%7D%0A%7D%0A...%20on%20SupportingPhrase%20%7B%0Alabel%0A%7D%0A%7D%0A%7D%0A%7D%0A%7D%0A%7D" target="_blank">Try it now</a>
</div>
