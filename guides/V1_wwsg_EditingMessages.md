---
copyright: 'Copyright IBM Corp. 2018'
link: 'edit-message-overview'
is: 'experimental'
---
## Edit Message Overview

Watson Work Services provides an **updateMessage** API for callers to change the contents of a **message**.  This mutation will replace the current content of a given message defined by its message id, and the new content.

Note: Only the author of a message can update its content.  Updating the content of messages not created by the calling user will receive a 403 Forbidden response.

### External API

 * GraphQL mutation for editing a message
    * **updateMessage** [Change the content of a message](https://github.com/watsonwork/watsonwork-developer-docs/blob/master/guides/V1_UpdateMessage.md)
    <br>
 * Outbound webhooks [Event for edited message](https://github.com/watsonwork/watsonwork-developer-docs/blob/master/guides/V1_wwsg_Webhooks.md)
    * **message-edited**
<br><br>


