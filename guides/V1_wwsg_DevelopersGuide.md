---
copyright: 'Copyright IBM Corp. 2017'
link: 'developers-guide'
is: 'published'
---
# Developer’s Guide to Watson Work Services

## Understanding Watson Work Services APIs

In Watson Work Services you will interact with our APIs over the HTTP protocol.
- For events you want to be notified about, you can simply subscribe to **Webhooks** which will in turn call your HTTP endpoint for each event.
- For data you want to create or retrieve you can leverage our **REST** or **GraphQL** APIs. We support a traditional REST model when appropriate, otherwise, we expose the majority of our data model through a GraphQL API.

**Note on calling our APIs**

In addition to our published APIs we also allow you to try out ones we categorize as **beta**, **experimental** and **future**.
You can learn more about what these mean by reading [Engaging with Us](../V1_EngagingWithUs.md).


In order to have access to APIs beyond the published ones, you must pass specific values in a header, as

```
x-graphql-view: PUBLIC, BETA, EXPERIMENTAL, FUTURE
```

So either pass none (as currently the default), or pass any combination of the above so long as you always have `PUBLIC` present (e.g., `x-graphql-view: PUBLIC, BETA`).

Once you do that, you can make use of those additional APIs we’re working on.
