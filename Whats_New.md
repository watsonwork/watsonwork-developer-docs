---
copyright: 'Copyright IBM Corp. 2017'
is: 'published'
link: 'whats-new'
---
## What's New

Keep up to date on what's new in IBM Watson Work Services. We'll list the latest news here, stay tuned!

| Date          | What's new       |
| ------------- |:-------------|
| 06.Jun.2018   | Added section with GraphQL [pagination](./guides/V1_pagination.md) example. |
| 27.Mar.2018   | Added `space-updated` and `space-deleted` webhook events. |
| 26.Mar.2018   | Updated [Focus](./guides/V1_wwsg_ActionIdentification.md), [Focus Annotation](guides/V2_Annotation_Message_Action_Identification.md), and [Focus API](./references/V1_Focus.yml) to reflect the classes produced by the latest implementation of Focus identification. After examining the usefulness of various categories for collaboration scenarios, a smaller set of categories with better precision is now used. See also [How AI can help enterprise workers automatically triage conversations](https://www.ibm.com/blogs/research/2018/01/ai-enterprise-workers-triage-convos/) for more information on the latest approach used for Focus identification. |
| 27.Feb.2018   | Added guide for [Publish in the Catalog](./guides/V1_PublishInTheCatalog.md) and also the [App review checklist](./guides/V1_AppReviewChecklist.md). |
| 15.Feb.2018   | Simplifications made to [Information Extraction](./guides/V1_Annotation_Message_Information_Extraction.md) based on the Watson Natural Language Understanding API |
| 07.Feb.2018   | Marked the property __emailAddresses: [String]__ on the [Person](https://developer.watsonwork.ibm.com/docs/people/) object **DEPRECATED** |
| 05.Dec.2017   | Added diagrams for collaboration flow, Watson's contributions and Watson understanding the conversation |
| 25.Sep.2017   | Added the Survey for **you** to help us make this developer experience great, please check it out on the main page or click [Take the Survey](https://www.surveygizmo.com/s3/3792857/IBM-Watson-Work-Services-Feedback) now. |
| 05.Sep.2017   | Added tutorial for slash commands which are now in `Beta` |
| 05.Sep.2017   | Moved documentation to github.com.  Exposed a number of documents not yet in web based developer experience to engage early with developers via github issues and PRs |
| 24.July.2017  | Introduced new concept of adding attachments in targeted messages via GraphQL. Attachments are rendered in the User Experience as Cards. Attachments are still `BETA` features. We are still actively developing them. |
| 08.May.2017   | Introduced new concept of `Beta` APIs. <br/><br>The developer documentation section will now include some APIs that we are still actively developing, but are stable and ready for initial evaluation. These API signatures may slightly change, though the underlying functionality will be released. The documentation will have a <sup class="badge badge-beta">BETA</sup> label for any API that is considered `beta`. |
|               | Added new tutorial showcasing new beta APIs for action identification and private interaction with users in the [Action Fulfillment](https://developer.watsonwork.ibm.com/docs/tutorials/action-fulfillment) tutorial. |
|               | The GraphQL explorer has been moved into the https://developer.watsonwork.ibm.com. The link in the developer docs section and in the navigation bar will now point to [GraphQL Explorer](https://developer.watsonwork.ibm.com/tools/graphql) |
| 24.Mar.2017   | In the Focus annotations, **start** and **end** indexes now represent the location of the phrase on the original message's content, including markdown. The **phrase** field still corresponds to the plaintext equivalent (disregarding markdown). Bumped the **focusVersion** from *4* to *5*. |
| 20.Mar.2017   | Updated Focus API to use Watson Conversation. Focus category 'Send' is now 'Share', category 'Open' is now 'View'. Added two new Focus fields lensId and applicationId. Renamed Focus field 'version' to 'focusVersion'. |
| 14.Mar.2017   | Added new section to [Share an App](./guides/V1_ShareAnApp.md) |
| 28.Feb.2017   | Renamed Focus annotation **type** from *cognitive-aip-nlc* to *message-focus* |
| 20.Feb.2017   | Improving, updating and adding function for App registration. |
|               | Added **Make it Cognitive** section to Apps registration page. You can connect your App to a Watson Conversation Workspace. [Learn more about Watson Conversation here](https://www.ibm.com/watson/developercloud/conversation.html)|
|               | Added **Terms of Service** setting for you to add a URL for your App users. |
|               | Added **Share your App** Button/URL so you can start sharing your App with others. |
|               | Your App can now be submitted for consideration to appear in the IBM Watson Workspace catalog of Apps accessed via the settings page for each space. |
|               | Added capability for an App's registration to optionally specify that additional App specific configuration is needed via a URL link that will be presented to its users after the App is added to their space. |
| 7.Feb.2017    | Welcome to the What's new page! |
