---
copyright: 'Copyright IBM Corp. 2018'
link: 'extended-action-fulfillment'
is: 'alpha'
---

# Extended Action Fulfillment

This document describes an extension to [Action Fulfillment Cards](https://github.com/watsonwork/watsonwork-developer-docs/blob/master/guides/V1_Action_Fulfillment.md) which allows you to create richer user interfaces. A new card type called a JSON card, is being developed which will support the creation of a richer User Experience. A JSON card has `title` and `cardJson` properties. The `title` is the primary text that is displayed in the card. The `cardJson` is a JSON representation of the card content.

Here's an example of the new JSON card:

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
            type: JSON,
            jsonCardInput: {
              title: "Sample Title",
              cardJson: {
                type: "Container",
                children: [
                  {
                    type: "TextInput",
                    props: {
                      id: "Name",
                      labelText: "Enter Name: ",
                    }
                  },
                  {
                    type: "Button",
                    props: {
                      labelText: "Save",
                    }
                  }
                ]
              }
            }
          }
        }
      ]
      }) {
      successful
    }
  }
```

### JSON Card Schema
The JSON Card definition describes a hierarchy of React elements which will be created and used to populate the Card.

```
{
  "definitions": {},
  "$schema": "http://json-schema.org/draft-06/schema#",
  "$id": "http://developer.watsonwork.ibm.com/card.json",
  "type": "object",
  "properties": {
    "type": {
      "$id": "/properties/type",
      "type": "string",
      "title": "type",
      "description": "React component tag name."
    },
    "props": {
      "$id": "/properties/props",
      "type": "array",
      "title": "props",
      "description": "React component properties."
    },
    "id": {
      "$id": "/properties/children",
      "type": "array",
      "title": "children",
      "description": "React component children."
    }
  }
}

```
