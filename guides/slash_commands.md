---
copyright: 'Copyright IBM Corp. 2017'
link: 'slash-commands'
is: 'beta'
---

# Commands

## Concepts

Commands enable users to privately interact with apps through explicitly triggering actions. Within any given space, a user will be able to view the list of commands that have been registered by the apps in that space, and explicitly trigger these actions. The action, and any information the user passes along with the action, will then be sent to the app that had registered the action. The app can then respond privately to the user.

#### In Workspace

In Watson Workspace, these commands will surface as _slash commands_. Anytime a user types `/` in a space, the user will be presented with a list of commands that have been registered by the apps in that space. If the user selects one of the commands, the command will then highlight in the input field and allow the user to add additional information before sending the action to the app. Once the user sends the command, the private dialog window will appear and allow the app to respond privately to the user. Other users in the space will not be notified of any actions being sent or responded to, unless the app decides to post a message back to the space.

## Working with Commands

#### Register your command
To register a command for your app, navigate to your app's dashboard under https://developer.watsonwork.ibm.com.
  * **Note:** While we are in _BETA_ for this feature, you will need to add the URL parameter `?actionTriggers=true`.

From the app's dashboard, select the **Add an Action** menu option on the left menu. This section lets you define actions that your app has, and associate these actions with a command.

To register a new command, select the **Add an action** button. When the new action dialog appears, provide the following information to register your action:

 | Field | Description | Required |
 | --- | --- | --- |
 | **Name** | A name for your action. **Note:** This is **not** the slash command string, but rather just a display name for the actions in the app's dashboard. | Yes |
 | **Description** | A description for the action. | No |
 | **Callback URL** | The URL where the action should be sent to. This will automatically create a webhook for you with this URL. | No |
 | **Allow self signed certificate** | This enables you to provide a Callback URL that has a self-signed certificate, rather than a real one for development purposes. | No |

 Once you have provided these values, select the **Command** button to continue configuration of your slash command. This button will direct you to provide information about the command in particular:

 | Field | Description | Required |
 | --- | --- | --- |
 | **Command String** | This is the value that will be surfaced as the slash command in Workspace. | Yes |
 | **Hint** | This value will surface as a hint for the command. This is where you would put in any parameter hints that your command may require. | No |

 Click **Add** to save your command changes, and then **Create** to finalize the creation of your action.

 Your action is now registered with the Watson Work Services platform, and _almost_ ready to use! You will need to copy the **Webhook secret** that is returned from creating the action so that you can update your running application to use this secret. See [Webhook References](../references/V1_OutboundCallback.yml) for more details on how to configure your webhook. Once you've configured, select the **Enable** button on your action to enable your webhook.

 Now when you add your app to a space, the commands you've registered will surface for users! In Workspace, this means the users will be able to type `/` and see your newly added command.

 #### Respond to a command
 Now that we've registered our commands, we need our app to respond if a user triggers the command. The process for responding to commands is similar to the process for responding to actions that are triggered during the [Action Fulfillment](../guides/V1_Action_Fulfillment.md) workflow.

 When a user triggers an action ( for example, in Workspace if a user selects a slash command and presses enter ), the app will receive an `actionSelected` annotation.

   **Action Selected annotation**

   Request body sample:

   ```javascript
   {
     spaceName: 'Sample Space Name',
     annotationType: 'actionSelected',
     annotationPayload: '<PAYLOAD_BELOW>',
     messageId: '',
     spaceId: '58934f00e4b0f86a34bbd085',
     userName: 'Sample End User',
     type: 'message-annotation-added',
     userId: '83152e37-0d9f-4bbb-9d5f-024e75a97600'
   }
   ```

   The `annotationPayload` is a string that needs to be parsed. Below are the parsed contents:

   ```javascript
   {
     type:'actionSelected',
     annotationId: '',
     version:'1.0',
     created: '',
     createdBy: '',
     updated: '',
     updatedBy: '',
     tokenClientId: '',
     conversationId:'58934f00e4b0f86a34bbd085',
     targetDialogId:'590888dce4b0a1b856e3169f-0',
     referralMessageId:'',
     actionId: '/command parameter1 paramter2',
     targetAppId:'83152e37-0d9f-4bbb-9d5f-024e75a97713'
   }
   ```

   * `conversationId` is the id of the space that the action is within
   * `actionId` is the slash command that was sent by the user
   * `targetAppId` is the appId that the triggered action belongs to.
   * `targetDialogId` is a string indicating the particular private dialog instance

The `actionSelected` annotation sends along the command that a user had entered, in the `actionId` field, as well as information about the space that the command was entered in and the `targetDialogId` for the private space to respond to.

Once this event is received, the app can respond back with a **targeted message** to the user who had triggered the command.

**Create Targeted Message**
~~~~
Method: POST
URL: https://api.watsonwork.ibm.com/graphql
Headers: 'Content-Type: application/graphql' , 'x-graphql-view: PUBLIC, BETA'
~~~~

```
  mutation {
    createTargetedMessage(input: {
      conversationId: "58934f00e4b0f86a34bbd085"
      targetUserId: "83152e37-0d9f-4bbb-9d5f-024e75a97600"
      targetDialogId: "SAMPLE_ACTION_1234"
      annotations: [],
      attachments: []
      }) {
      successful
    }
  }
```

The `targetDialogId` and the `targetUserId` are obtained from the actionSelected webhook event received by the app. These are sent back in the createTargetedMessage graphql call so that they display for that user and in the correct dialog. The annotations should be an array of generic annotations with buttons property.

The generic annotation can be added through GraphQL for these targeted messages. In addition to the title and text field, generic annotations within a targeted message can contain buttons with a title, id and style. The title is the text that is displayed to the user. The button identifier (id) is used as the actionId of a Webhook event that is sent back to your app. The current styles are _PRIMARY_ (purple button) AND _SECONDARY_ (gray button).

Here's an example with a generic annotation:

```
  mutation {
    createTargetedMessage(input: {
      conversationId: "58934f00e4b0f86a34bbd085"
      targetUserId: "83152e37-0d9f-4bbb-9d5f-024e75a97600"
      targetDialogId: "SAMPLE_ACTION_1234"
      annotations: [
      {
        genericAnnotation: {
          title: "Sample Title",
          text: "Sample Body"
          buttons: [
            {
              postbackButton: {
                title: "Sample Button",
                id: "Sample_Button",
                style: PRIMARY
              }
            }
          ]
        }
      }
      ]
      }) {
      successful
    }
  }
```

Attachments can be added through GraphQL for targeted messages as well. If your app sends both attachments and annotations, only attachments will be rendered in the User Experience. Cards are a type of an Attachment. Information card is a type of Card Attachment. Information card has title, subtitle, text, date, and can also contain buttons. The title is the primary text that is displayed in card. The subtitle is secondary text in the card. The date is a unix-timestamp displayed as human readable date in the card. Buttons have text, payload, and style. The button payload is used as the actionId of a Webhook event that is sent back to your app. The current styles are _PRIMARY_ (purple button) AND _SECONDARY_ (gray button).

Here's an example with attachments:

```
  mutation {
    createTargetedMessage(input: {
      conversationId: "58934f00e4b0f86a34bbd085"
      targetUserId: "83152e37-0d9f-4bbb-9d5f-024e75a97600"
      targetDialogId: "SAMPLE_ACTION_1234"
      attachments: [
      {
          type: CARD,
          cardInput: {
              type: INFORMATION,
              informationCardInput: {
                  title: "Sample Title",
                  subtitle: "Sample Subtitle",
                  text: "Sample Text",
                  date: "1500573338000",
                  buttons: [
                      {
                          text: "Sample Button Text",
                          payload: "Sample Button Payload",
                          style: PRIMARY
                      }
                  ]
              }
          }
      }
      ]
      }) {
      successful
    }
  }
```
