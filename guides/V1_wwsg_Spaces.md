---
copyright: 'Copyright IBM Corp. 2017'
link: 'send-a-message-into-a-conversation'
is: 'published'
---
# Send a message into a conversation

Watson Work Services provides a **space** object as a context for people to interact with its **conversation** object and post / send **messages** to it.

When an app posts a message, it can provide the message formatting and additional properties through the use of an  **Annotation** object.  Think of the annotation as an attachment to the message.  The app must use the "generic" annotation type to express the content and format that should be posted / sent to the conversation.

You can read the API reference here, [Spaces API Reference](../references/V1_Spaces.yml), to learn more about the "generic" annotation properties.

Some of these properties allow you to change the aesthetics of a message. For example, you can add _color_ to make your message stand out. Or, you can provide ways to decorate the text string with _markdown_. Optionally, you can include information about **who** the app is representing as sending the message by adding the _actor_ object to your message.

### Message color

For color, select a hexadecimal RGB color value. This will appear as an indicator to decorate your message.

### Style with markdown

Your text message and title can be decorated using a set of markdown.


| Style | Supported Markdown |
| --- | --- |
| **bold** | \*bold\* |
| __italic__ | \_italic\_ |
| [link](https://developer.watsonwork.ibm.com/docs) | \[link\](https://example.com) |
| code | \`code\` |
| code block | \`\`\`<br />code block<br />\`\`\` |

### Add an actor

In addition to decoration, you can include an actor as part of your message. Keep in mind this is an optional property for your message. An actor represents the person or entity that is responsible for the message.  This is used typically to represent people who are not necessarily users in Watson Work Services but who are being "proxied" to participate in a conversation via an app. The name property is a string that represents the actor’s name.

### Example

The following represents the body sent to Watson Work Services by an app to represent a message sent by a user named Frank Adams who is outside the realm of Watson Work Services users.  See details in [Spaces API Reference](../references/V1_Spaces.yml)

```
{
  "type": "appMessage",
  "version": "1",

  "annotations":  [
    {

      "type": "generic",
      "version": "1",

      "color": "#36a64f",
      "title": "Hello world",
      "text": "Hello from a Watson Work Services app",

      "actor": {
        "name": "Frank Adams"
      }

    }
	]
}
```
