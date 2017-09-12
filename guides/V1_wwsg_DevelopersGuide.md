---
copyright: 'Copyright IBM Corp. 2017'
link: 'developers-guide'
is: 'published'
---
# Developer's Guide to Watson Work Services

## Understanding Watson Work Services APIs

In Watson Work Services you will interact with our APIs over the HTTP protocol.
- For events you want to be notified about, you can simply subscribe to **Webhooks** which will in turn call your HTTP endpoint for each event.
- For data you want to create or retrieve you can leverage our **REST** or **GraphQL** APIs. We support a traditional REST model when appropriate, otherwise, we expose the majority of our data model through a GraphQL API.

