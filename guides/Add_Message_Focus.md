---
copyright: 'Copyright IBM Corp. 2017'
link: 'add-a-message-focus'
is: 'beta'
---
# Add a message focus
Your App can add a message focus to any message that it has access to by either configuring your app with Watson Conversation or by leveraging the GraphQL `addMessageFocus` mutation.

The `addMessageFocus` GraphQL mutation enables an app to construct and attach a message-focus annotation to a particular message.

Take a look at the`addMessageFocus` GraphQL mutation.

```graphql
  mutation {
    addMessageFocus(input: {
      messageId: "58934f00e4b0f86a34bbd073"
      messageFocus: {
        phrase: "What are the top opportunities?"
        lens: "Opportunity"
        category: "Inquiry"
        actions: [ "ListTopOpportunities" ]
        confidence: 0.99
        payload: "payload_string"
        start: 0
        end: 31
        version: 1
        hidden: false
      }
    }){
    message {
      id
      annotations
    }
  }
  }
```
<br/>

| Property | Description |
| --- | --- |
| messageId | The id for the message that will get annotated with the `message-focus` annotation. |
| phrase | The part of the message that is considered to be a focus, based on the 3rd party app's processing. |
| lens | The custom lens that was determined from the phrase. For example, `Opportunity`. <br/><br/>Note: This lens will surface in moments unless `hidden` is set to false. |
| category | [Optional] A further refinement for the detected lens. <br/><br/>Example: If the lens is `Opportunity`, the categories could be `Inquiry`, `Sale`, etc.  |
| actions | [Optional] A list of actions that can be taken on the phrase, based on the detected lens. This will result in the phrase getting highlighted for the user to initiate the action. <br /><br/>See [Action Fulfillment](https://developer.watsonwork.ibm.com/docs/tutorials/action-fulfillment) tutorial for more details.  |
| confidence | [Optional] A confidence score for the lens classification. |
| payload | [Optional] Any app-specific information that may need to be persisted and transferred back to the app when interacting with message-focus annotations. |
| start | [Optional] The starting index for where the phrase surfaces in the original message text. This will be used if an `action` is defined and a highlight is required.  |
| end | [Optional] The ending index for where the phrase surfaces in the original message text. |
| version | [Optional] The app-specific version for the particular `message-focus` annotation. |
| hidden | [Optional] A true or false flag to determine if the lens should surface in the Moments view.  |

Once this mutation is posted, a `message-focus` annotation will be attached to the message. This will result in the usual events being sent out for new annotations, and will also result in the clients displaying any actions, if they exist, on the `message-focus`.
