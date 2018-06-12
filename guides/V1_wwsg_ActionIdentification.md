---
copyright: 'Copyright IBM Corp. 2017'
link: 'focus'
is: 'published'
---
## Focus

When it comes to Focuses, there are two concepts you need to understand.  A `lens`, which is a way a user interprets or understands a message, and a `focus`, which helps the user understand what to pay attention to in that message.  In other words, lenses help the user focus on different parts of the conversation.  

Watson Work Services has three lenses - `ActionRequest`, `Question`, and `Commitment`.  These lenses identify focuses that are either an action, a question or a commitment. `Focuses`, identified with the `ActionRequest` lens, can be further refined by action-related categories.  

When Watson Work Services identifies a `focus`, an annotation is added to the message where the focus was found.

#### Lenses and Categories
###### ActionRequest
The `ActionRequest` lens is used when there is an explicit or implied request to do something.

The following _categories_ are available
* `Schedule` : Schedule an event or create an invite.
* `Share` : Share or send content such as documents or links. Send a message or email (or otherwise contact or reach out to) another person.

###### Question
The `Question` lens is used to identify text where a user is asking a question and where they expect an answer.

###### Commitment
The `Commitment` lens is similar to the `ActionRequest` lens but identifies text where a user is committing to take an action.
