---
copyright: 'Copyright IBM Corp. 2017'
link: start-coding-now
is: 'published'
---

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

```

To run the file, open a command line.

1. Change to the directory where you saved your file.
2. Install the request library. Enter `npm install request`.
3. Enter `export APP_ID=<your_app_id>`
4. Enter `export APP_SECRET=<your_app_secret>`
5. Enter `$node FILENAME.js`.

The app returns an access token and some metadata at the command line, which you'll use later to access the Watson Work Services API. You're ready to start building.
