---
copyright: 'Copyright IBM Corp. 2017'
link: 'api-reference'
is: 'published'
---

# API Reference

**Note on calling our APIs**

In addition to our published APIs we also allow you to try out ones we categorize as **beta**, **experimental** and **future**.
You can learn more about what these mean by reading [Engaging with Us](../V1_EngagingWithUs.md).


In order to have access to APIs beyond the published ones, you must pass specific values in a header, as

```
x-graphql-view: PUBLIC, BETA, EXPERIMENTAL, FUTURE
```

So either pass none (as currently the default), or pass any combination of the above so long as you always have `PUBLIC` present (e.g., `x-graphql-view: PUBLIC, BETA`). 

Once you do that, you can make use of those additional APIs we’re working on.
