---
copyright: 'Copyright IBM Corp. 2017'
link: engaging-with-us
is: 'published'
---

## Engaging with us

We are continually adding value and want to include you as early as possible in our development process so we can include
your input and feedback. Some features are stable (in that they will not change), others are in progress of being built which we call **beta**
and others are things we want to try and discover what would work best, we call **experimental**. Additionally, when we are about to
introduce something new and want to get feedback on the concepts and understanding before we expose APIs, so that your
feedback can inform and guide the future API, we will call these **future**. Also, **future** may, (but not always), include the ability for you to
play with an API, through one of our tools (like the GraphQL Explorer), so you can have some experience with it and give us
feedback to help inform and improve things.

APIs that are going to be going out of service will be called **deprecated**, which means that while this is still available
for developers to use, it will be removed and calls to this API will no longer work. They will be kept on to provide backward
compatibility, and to provide time for developers to update affected code.

You will see these various categories called out on those specific APIs. All other, undecorated API references are
considered published and are fully supported.

To provide more transparency in how we’re working and what we’re building, we will surface our content in markdown files in
the GitHub repo - [github.com/watsonwork/watsonwork-developer-docs](https://github.com/watsonwork/watsonwork-developer-docs) so that you can engage with us through GitHub to inform
and provide feedback to help make and design great APIs.

In providing feedback let us know what sort of feedback you’re giving us, such as;

- something wrong or incorrect
- something confusing with the documentation or results experienced with an API
- in the cases where we’ve published something that is **experimental**, **beta**, or **future**, please provide a comment or reaction to what we’re saying
- provide suggestions to things we may have left out that you believe we should include
- and really any other thoughts you want to share with us

To provide feedback, if it’s on an existing document or the API related to it, please create a fork and make your own changes and comments and create a Pull Request to draw our attention. If you want to comment in general or give us general feedback not directly related to documentation files, please create an issue. Also, create issues if you have suggestions for us in terms of Tutorials or code examples you’d like to see.

### How we make our developer experience

We build our developer experience [developer.watsonwork.ibm.com](https://developer.watsonwork.ibm.com) through the use of the files we
keep in the GitHub repository mentioned above. When we build, we only bring in those files that are marked as **published**, **beta**
or **deprecated**, and do not add those marked as **future** or **experimental**.

Note: you can see and experience these things in our [GraphQL Explorer](https://developer.watsonwork.ibm.com/tools/graphql). When you use the explorer by default you’ll see only the currently published APIs we support. If you want to also see things like **beta**,**experimental** or **future** you need to update the URL.

To see **beta** use this URL [https://developer.watsonwork.ibm.com/tools/graphql?apiType=beta](https://developer.watsonwork.ibm.com/tools/graphql?apiType=beta)

To see **experimental** use this URL [https://developer.watsonwork.ibm.com/tools/graphql?apiType=experimental](https://developer.watsonwork.ibm.com/tools/graphql?apiType=experimental)

To see **future** use this URL [https://developer.watsonwork.ibm.com/tools/graphql?apiType=future](https://developer.watsonwork.ibm.com/tools/graphql?apiType=future)

To see all three of these, just use this URL [https://developer.watsonwork.ibm.com/tools/graphql?apiType=beta,experimental,future](https://developer.watsonwork.ibm.com/tools/graphql?apiType=beta,experimental,future) ...and you can mix and match to pick the ones you want to see.



**Folder Structure**

Root:
- [Navigation Menu](https://github.com/watsonwork/watsonwork-developer-docs/blob/master/NavigationMenu.md) where we keep the structure of the entire experience.
- general getting started information, direction and also a list of what’s new as we add it to the experience [What’s New](https://github.com/watsonwork/watsonwork-developer-docs/blob/master/Whats_New.md)

Guides:
- all the developer guide and get started content

References:
- this is for ALL API references, in .yml format

Images:
- any image that is used in any of the md files go here

**Note on calling our APIs**

In addition to our published APIs we also allow you to try out ones we categorize as **beta**, **experimental** and **future**.

In order to have access to APIs beyond the published ones, you must pass specific values in a header, as

```
x-graphql-view: PUBLIC, BETA, EXPERIMENTAL, FUTURE
```

So either pass none (as currently the default), or pass any combination of the above so long as you always have `PUBLIC` present (e.g., `x-graphql-view: PUBLIC, BETA`).

Once you do that, you can make use of those additional APIs we’re working on.

