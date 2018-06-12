---
copyright: 'Copyright IBM Corp. 2017'
link: 'create-a-space'
is: 'published'
---
## Create a space

Spaces are where the collaboration magic happens. Let's take a look at how a sample GraphQL mutation is used to create a space.

Starting small, the absolute minimum mutation to create a space and get the ID would be:

```
mutation createSpace {
  createSpace(input: { title: "Space title",  members: [""]}){
    space {
      id
    }
  }
}
```

<div class="tip">
  <img src="../images/note_pencil.png" />
  <p><strong>Note:</strong> Only users can create spaces. Need your App to create a space? No problem! Checkout out <a href="https://developer.watsonwork.ibm.com/docs/apps/prepare-your-app-to-run">Prepare your app to run</a> to learn how to authorize your App to act on behalf of a user.</p>
</div>

See it in action with our GraphQL tool and create a space. <a href="https://developer.watsonwork.ibm.com/tools/graphql?query=mutation%20createSpace%20%7B%0A%20%20createSpace(input%3A%20%7Btitle%3A%20%22Space%20title%22%2C%20members%3A%20%5B%22user1-id%22%2C%20%22user2-id%22%5D%7D)%20%7B%0A%20%20%20%20space%20%7B%0A%20%20%20%20%20%20id%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D%0A" target="_blank">Try it now</a>

If you need more info we've got you covered. Get as much additional information as you want by:

```
mutation createSpace {
  createSpace(input: { title: "Space title",  members: ["user1-id", "user2-id"]}){
    memberIdsChanged
    space {
      id
      title
      description
      membersUpdated
      members {
        items {
          email
          displayName
        }
      }
      conversation{
        messages{
          items {
            content
          }
        }
      }
    }
  }
}
```

See it in action with our GraphQL tool and create a space. <a href="https://developer.watsonwork.ibm.com/tools/graphql?query=mutation%20createSpace%20%7B%0A%20%20createSpace(input%3A%20%7Btitle%3A%20%22Space%20title%22%2C%20members%3A%20%5B%22user1-id%22%2C%20%22user2-id%22%5D%7D)%20%7B%0A%20%20%20%20memberIdsChanged%0A%20%20%20%20space%20%7B%0A%20%20%20%20%20%20id%0A%20%20%20%20%20%20title%0A%20%20%20%20%20%20description%0A%20%20%20%20%20%20membersUpdated%0A%20%20%20%20%20%20members%20%7B%0A%20%20%20%20%20%20%20%20items%20%7B%0A%20%20%20%20%20%20%20%20%20%20email%0A%20%20%20%20%20%20%20%20%20%20displayName%0A%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20conversation%20%7B%0A%20%20%20%20%20%20%20%20messages%20%7B%0A%20%20%20%20%20%20%20%20%20%20items%20%7B%0A%20%20%20%20%20%20%20%20%20%20%20%20content%0A%20%20%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D%0A" target="_blank">Try it now</a>
