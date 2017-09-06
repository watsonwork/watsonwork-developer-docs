---
copyright: 'Copyright IBM Corp. 2017'
link: get-started
is: 'published'
---
### Welcome to Watson Work Services

Hi!  Thanks for checking out Watson Work Services.  You've come to the right place if you want to build apps that take advantage of conversational + cognitive services, powered by Watson.   With Watson Work Services, you can build capabilities to customize your team's use of Watson Workspace, and create apps that will integrate with Watson Workspace for anyone to add to their spaces, and you can also develop apps for other business tools.  

These services are built for extensibility.  They are meant to extend your experience with Watson Workspace and your everyday tools - making it easier for you and others to get work done.

In Watson Workspace, users get work done in a space, a virtual workspace.  They can converse, share files, work with other tools and more.  There are cognitive capabilities such as moments and action fulfillment built in.   As an app developer, there is a lot you can do to enhance that experience and other similar conversational experiences.  

So let's get started building an app with Watson Work Services.

### What can you build?

The Watson Work Services platform can support apps in Watson Workspace, or you can make them available on their own. That's great, but what's that mean? You can build apps that can:

- Send interactive [messages into a space](guides/V1_wwsg_Spaces.md)

- Listen & respond to events automatically via [outbound webhooks](guides/V1_wwsg_Webhooks.md)

- Allow users to initiate actions using [conversational text](guides/V1_Action_Fulfillment.md)

You can also make apps that use cognitive capabilities to understand users' conversations and interactions. Your app can suggest actions, recognize sentiment, or provide expertise. And, they can be trained to understand business dialect associated with specific domains or industries. For example, a sales team has different terminology than a medical team. Here are a few we've come up with, we can't wait to see what you do!

<table border="0">
 <tr height="64">
  <td><img src="../images/GitHub-Mark-32px64w.png" style="height:32px;text-align:center;" /></td>
  <td><a href="https://github.com/watsonwork">IBM Watson Work Sample Apps</a>, see Watson Work Services in action.</td>
 </tr>
 <tr height="64">
  <td><img src="../images/IBMWatsonWorkspaceIcon64w.png" style="height:32px;text-align:center;" /></td>
  <td><a href="https://workspace.ibm.com/#">IBM Watson Workspace</a>, working for you and your team to get work done.</td>
 </tr>
 <tr height="64">
  <td><img src="../images/DiscoverIcon64w.png" style="height:32px;text-align:center;" /></td>
  <td><a href="http://www.rocketsoftware.com/products/rocket-discover">Rocket Discover</a>, self-service data discovery for business users and executives.</td>
 </tr>
 <tr height="64">
  <td><img src="../images/redbooth-color-342x87.png" style="width:64px;text-align:center;" /></td>
  <td><a href="http://redbooth.com">Redbooth</a>, easy-to-use online task and project management software for busy teams.</td>
 </tr>
 <tr height="64">
  <td><img src="../images/Sapho_logo.png" style="width:64px;text-align:center;" /></td>
  <td><a href="https://www.sapho.com/">Sapho</a>, the future of work. Delivered today.</td>
 </tr>
 <tr height="64">
  <td><img src="../images/opentopic-Logo.png" style="width:64px;text-align:center;" /></td>
  <td><a href="http://opentopic.com/ibm-workspaces/">Opentopic</a>, personalize your digital marketing campaigns using cognitive technology.
 </td>
 </tr>
 </table>

- Make it easy for users to catch up by summarizing the conversation with [Moments](guides/V1_wwsg_MomentIdentification.md)

- Analyze and extract key information such as keywords, sentiment, dates, and more with [Information Extraction annotations](guides/V1_Annotation_Message_Information_Extraction.md)

- Identify [focuses](guides/V1_wwsg_ActionIdentification.md) (key phrases) within the conversation and suggest actions users can take inline with [Action Fulfillment](guides/V1_Action_Fulfillment.md).

### Start coding now!

So let's get started and create an app.  When you create an app you are effectively registering your app in our environment so it can take action using Watson Work Services.   Your new app is automatically assigned an **App ID**, a unique number that Watson Work Services uses to identify your app and an **App secret**, used to authenticate your App so that it can work in our environment.

To create your app start in apps dashboard.  (Include pictures of the UI)
1. Click **Apps** in the main navigation at the top of this page, or click this link to the Your Apps page.
2. Click **Create new app** to create an App ID and an App Secret. Save them both. Your app uses these every time you connect to the API. If you lose your App Secret, you won't have an opportunity to retrieve it.
3. Give your app a name and description and click **Create**.

Once you have your ID and secret, use this simple node.js app to make your first Watson Work Services API call and make sure your App ID and App Secret work. If this is a brand new app, you can use it as a stub to start coding.
1. Install [node.js](https://nodejs.org/en/) version 6 or later.
2. Test your node.js installation at the command line. Enter node --version.
3. Copy the following code and paste it in a text file. Save it as a .js file and create a folder to contain it.

```
const request = require('request');

// API to authorize application and generate access token.
const WWS_OAUTH_URL = "https://api.watsonwork.ibm.com/oauth/token";

// App ID retrieved from registration process.
const APP_ID = process.env.APP_ID;

// App secret retrieved from registration process.
const APP_SECRET = process.env.APP_SECRET;

// Build request options for authentication.
const authenticationOptions = {
    "method": "POST",
    "url": WWS_OAUTH_URL,
    "auth": {
      "user": APP_ID,
      "pass": APP_SECRET
    },
    "form": {
      "grant_type": "client_credentials"
    }
  };

if (!APP_ID || !APP_SECRET) {
  console.log("Please provide the app id and app secret as environment variables.");
  process.exit(1);
}

// Authorize application.
request(authenticationOptions, function(err, response, body){

  // If successful authentication, a 200 response code is returned
  if(response.statusCode == 200){
    console.log ("Authentication successful\n");
    console.log ("App Id: " + authenticationOptions.auth.user);
    console.log ("App Secret: " + authenticationOptions.auth.pass + "\n");
    console.log ("access_token:\n\n" + JSON.parse(body).access_token + "\n");
    console.log ("token_type: " + JSON.parse(body).token_type);
    console.log ("expires_in: " + JSON.parse(body).expires_in);
    console.log ("\n");
  } else {
    console.log("Error authenticating with\nApp: " + authenticationOptions.auth.user + "\nSecret: " + authenticationOptions.auth.pass + "\n\n");
  }
});

}
```

To run the file, open a command line.

1. Change to the directory where you saved your file.
2. Install the request library. Enter `npm install request`.
3. Enter `export APP_ID=<your_app_id>`
4. Enter `export APP_SECRET=<your_app_secret>`
5. Enter `$node FILENAME.js`.

The app returns an access token and some metadata at the command line, which you'll use later to access the Watson Work Services API. You're ready to start building.

### Next steps

Great!  You're off and running!  

First, check out the rest of the developer documentation to learn how to make your app sing. Since you'll be using GraphQL we've prepared a [quick intro](guides/V1_wwsg_DevelopersGuide.md) so you can learn how to make the magic happen. If you still need a kickstart with building your first app check out this [tutorial](guides/V1_Action_Fulfillment.md). We also have [sample apps on Github](https://github.com/watsonwork) that can help you understand what you can do with Watson Work Services. If you need more help, let us know and talk to other developers in our [forums](https://help.workspace.ibm.com/hc/en-us/community/topics/201192468-Developers).

You can start building your app on [IBM Bluemix](https://console.ng.bluemix.net/), which is a platform and other services that can host your app. Create a free account and get started!

You can make basic changes to your app, like changing the name, description, or deleting it in your app's dashboard. Click **Apps** in the main navigation at the top of this page, or click this link to the your [Apps page](https://developer.watsonwork.ibm.com/apps) to find your app and modify it. You can also supercharge it with these fantastic features.

- [Make your app cognitive](guides/V1_cognitive_app.md) to associate an instance of Watson Conversation.
- [Make your app configurable](guides/V1_MakeAppsConfigurable.md) to allow users to customize or configure preferences for your app.
- [Listen to events](guides/V1_wwsg_Webhooks.md) in a space by adding a Webhook to your app.
- [Share your app](guides/V1_ShareAnApp.md) with friends and colleagues by generating the HTML for a share button.
