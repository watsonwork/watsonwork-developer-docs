---
copyright: 'Copyright IBM Corp. 2018'
link: 'reactions-overview'
is: 'published'
---
## Reactions Overview

Watson Work Services provides a set of **reaction** APIs for callers to interact with **messages**, adding and removing reactions associated with a message.

Reaction APIs allow for the association of "reactions" to objects such as "messages". A "reaction" is represented simply by a String. The Workspace application utilizes a particular set of emojis to represent the reactions. This separation of emoji from reactions allow for future implementations and for other clients to choose different set of emojis or their own custom set of Strings.

![Image](https://github.com/watsonwork/watsonwork-developer-docs/blob/master/images/reaction.png)

Reactions are a quick way to respond to someone's message.  The caller can select any reaction (string/emoji) of their preference, and associate it with a message.  The message object will optionally retrieve all the reactions to a message, returning each **reaction** (string/emoji), the current number (**count**) of reactors for each of those reactions and if the caller has already reacted or not (**viewerHasReacted**).  Separately, the caller can get a paginated list of users who reacted with a specific reaction.

### External APIs

 * GraphQL mutation for adding reaction
    * **addReaction** [Add a reaction to a message](https://github.com/watsonwork/watsonwork-developer-docs/blob/master/guides/V1_Add_Reaction.md)
    <br>
 * GraphQL mutation for removing reaction
    * **removeReaction** [Remove a reaction to a message](https://github.com/watsonwork/watsonwork-developer-docs/blob/master/guides/V1_Remove_Reaction.md)
    <br>
 * GraphQL query for users reacting with a reaction
    * **reactingUsers** [Get users who reacted to a message](https://github.com/watsonwork/watsonwork-developer-docs/blob/master/guides/V1_Reacting_Users.md)
    <br>
 * Outbound webhooks [Events for reactions](https://github.com/watsonwork/watsonwork-developer-docs/blob/master/guides/V1_wwsg_Webhooks.md)
    * **reaction-added**
    * **reaction-removed**
    <br>
 * GraphQL query for getting reaction along with messages
    * [Optional inclusion of reactions with message retrieval](https://github.com/watsonwork/watsonwork-developer-docs/blob/master/guides/V1_message_main.md)
<br><br>


