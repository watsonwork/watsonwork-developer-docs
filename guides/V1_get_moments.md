---
copyright: 'Copyright IBM Corp. 2017'
link: 'get-a-list-of-moments'
is: 'beta'
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

Try it out with our GraphQL tool - <a href="https://developer.watsonwork.ibm.com/tools/graphql?query=query%20getMoments(%24spaceId%3A%20String!)%20%7B%0A%20%20moments(spaceId%3A%20%24spaceId)%20%7B%0A%20%20%20%20items%20%7B%0A%20%20%20%20%20%20id%0A%20%20%20%20%20%20live%0A%20%20%20%20%20%20startTime%0A%20%20%20%20%20%20endTime%0A%20%20%20%20%20%20keyMessage%20%7B%0A%20%20%20%20%20%20%20%20id%0A%20%20%20%20%20%20%20%20content%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20summaryPhrases(first%3A%203)%20%7B%0A%20%20%20%20%20%20%20%20label%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20participants(first%3A%2010)%20%7B%0A%20%20%20%20%20%20%20%20user%20%7B%0A%20%20%20%20%20%20%20%20%20%20id%0A%20%20%20%20%20%20%20%20%20%20displayName%0A%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20messageCount%0A%20%20%20%20%20%20%20%20viaAppUsers%20%7B%0A%20%20%20%20%20%20%20%20%20%20displayName%0A%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20priority%20%7B%0A%20%20%20%20%20%20%20%20predicted%0A%20%20%20%20%20%20%20%20support%20%7B%0A%20%20%20%20%20%20%20%20%20%20category%0A%20%20%20%20%20%20%20%20%20%20...%20on%20SupportingParticipant%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20person%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20displayName%0A%20%20%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%20%20...%20on%20SupportingPhrase%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20label%0A%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D%0A&operationName=getMoments" target="_blank">Get a list of moments</a>
