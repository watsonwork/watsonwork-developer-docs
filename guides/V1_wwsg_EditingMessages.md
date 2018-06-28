---
copyright: 'Copyright IBM Corp. 2018'
link: 'edit-message-overview'
is: 'experimental'
---
## Edit Message Overview

Watson Work Services provides an **updateMessage** API for callers to change the contents of a **message**.  This mutation will replace the current content of a given message defined by its message id, and the new content.

![Image](https://github.com/watsonwork/watsonwork-developer-docs/blob/master/images/editMessage.png)

Notes:


 - Only the author of a message can update its content.  Updating the content of messages not created by the calling user will receive a **403 Forbidden** response.

 - Existing annotations will be stripped from an updated message.  Apps are expected to regenerate any annotation using the new content.  Mention annotations are automatically regenerated based on the new content.  These annotations will be sent as `message-annotation-added` events.

 - Apps calling the updateMessage mutation using the app's identity will be rejected with a **400 Bad Request** response, but when the app is running on behalf of a user, it will be allowed to update the user's messages as that user.

 - An app can not update a message created via generic annotation or by using generic annotations.



### External API

 * GraphQL mutation for editing a message
    * **updateMessage** [Change the content of a message](https://github.com/watsonwork/watsonwork-developer-docs/blob/master/guides/V1_UpdateMessage.md)
    
    
 * Outbound webhooks [Event for edited message](https://github.com/watsonwork/watsonwork-developer-docs/blob/master/guides/V1_wwsg_Webhooks.md)
    * **message-edited**




