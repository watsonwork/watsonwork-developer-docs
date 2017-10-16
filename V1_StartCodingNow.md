---
copyright: 'Copyright IBM Corp. 2017'
link: start-coding-now
is: 'published'
---

### Start coding now!

So let's get started and create an app.  When you create an app you are effectively registering your app in our environment so it can take action using Watson Work Services.   Your new app is automatically assigned an **App ID**, a unique number that Watson Work Services uses to identify your app and an **App secret**, used to authenticate your App so that it can work in our environment.

1. Click **Apps** in the main navigation at the top of this page, or click [this link](https://developer.watsonwork.ibm.com/apps) to take you to Your Apps page.
2. Click **Create new app** to register a new app and obtain its App ID and an App Secret. 
3. Give your app a name and description and click **Create**.  Save both, the App ID and the App Secret. Your app uses these to obtain an access token which is needed every time you need to connect to the API. If you lose your App Secret, you can go back to your app registration page in and generate a new one.

Once you have your ID and secret, use this simple Node.js code fragment to make your first Watson Work Services API call and make sure your App ID and App Secret work. If this is a brand new app, you can use it as a stub to start coding.  The code is very simple, but illustrates the means to obtain an access token to use in making subsequent API calls.

1. Install [node.js](https://nodejs.org/en/) version 6 or later.
2. Test your Node.js installation at the command line. Enter `node --version`.
3. Copy the following code and save it into a text file with a .js extension.

```
const request = require('request');

// API to authorize application and generate access token.
const WWS_OAUTH_URL = "https://api.watsonwork.ibm.com/oauth/token";

// API to issue graphQL requests.
const WWS_GRAPHQL_URL = "https://api.watsonwork.ibm.com/graphql";


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
  if (response.statusCode == 200) {

    const authenticationResponse = JSON.parse(body);
    console.log ("Authentication successful\n");
    console.log ("App Id: " + authenticationOptions.auth.user);
    console.log ("App Secret: " + authenticationOptions.auth.pass + "\n");
    console.log ("access_token:\n\n" + authenticationResponse.access_token + "\n");
    console.log ("token_type: " + authenticationResponse.token_type);
    console.log ("expires_in: " + authenticationResponse.expires_in);
    console.log ("\n");

    const GraphQLOptions = {
        "url": `${WWS_GRAPHQL_URL}`,
        "headers": {
            "Content-Type": "application/graphql",
            "jwt": ""
        },
        "method": "POST",
        "body": "query me_app { me { displayName, createdBy { displayName, email } } }"
    };

    GraphQLOptions.headers.jwt = authenticationResponse.access_token;

    console.log ("Issuing API to get more App details...\n");


    request(GraphQLOptions, function(err, response, graphqlbody) {

      if (!err && response.statusCode === 200) {
          const me = JSON.parse(graphqlbody).data.me;

          console.log ("App Name:" + me.displayName);
          console.log ("App Creator Name:" + me.createdBy.displayName);
          console.log ("App Creator Email:" + me.createdBy.email);

      } else {
          console.log("ERROR: Can't retrieve " + GraphQLOptions.body + " status:" + response.statusCode);
          return;
      }
    });

  } else {
    console.log("Error authenticating with\nApp:" + authenticationOptions.auth.user + "\nSecret:" + authenticationOptions.auth.pass + "\n\n" + response.body + "\n\n" + JSON.stringify(authenticationOptions));
  }
});


```

4. Open a command line and change to the directory where you saved your file.  Set two environment variables to the app id and secret.  Enter `export APP_ID=<yourAppId>` on a Mac or `set APP_ID=<yourAppId` on a PC.  Do the same for `APP_SECRET`
5. Install the Node `request` library. Enter `npm install request`.
6. Using the name of the file that you saved the above code enter: `node <your file name>.js` to execute the code.

The app returns an access token based on the provided id and secret and additional data on the token including its lifetime in seconds (how long it will be valid.)  You'll use this token to access the Watson Work Services APIs. You're ready to start building.
