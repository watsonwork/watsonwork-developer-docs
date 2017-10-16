---
copyright: 'Copyright IBM Corp. 2017'
link: 'make-your-app-cognitive'
is: 'published'
---
## Make your App cognitive

The Make it Cognitive section of your App's dashboard allows you to associate an instance (workspace) of [Watson Conversation](https://www.ibm.com/watson/developercloud/conversation.html) with your application. When you App is installed to a space, new messages will be sent to your Watson Conversation instance by Watson Work Services using the credentials you've provided in the Make it Cognitive section of the App's dashboard.

In your App's dashboard, you provide a Watson Conversation ID. This ID is found in [Watson Conversation](https://www.ibmwatsonconversation.com) by clicking View Details from the menu on your Watson Conversation Workspace.

You also provide credentials in your App dashboard. Find the credentials in the [Bluemix service](https://console.ng.bluemix.net/services/) by clicking on your Watson Conversation service instance and then clicking on the Service Credentials tab. You may create dedicated credentials here for use by Watson Work Services.

Watson Work Services annotates messages with [Focuses](../guides/V1_wwsg_ActionIdentification.md) based on the intents from your instance of Watson Conversation.

The user interface for [Moments](../guides/V1_wwsg_MomentIdentification.md) in Watson Workspace will display all focuses, including those identified by Apps installed in the space.

Lens names are derived from your intent names.

Use of your App, by you or others, may incur charges to the account associated with the Watson Conversation instance and credentials provided.
