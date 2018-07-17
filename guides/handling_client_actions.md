## Handling Client Actions

Watson Work Services allows your App to provide for actions issued from a Watson Work Services client (for example, Watson Workspace). Here your App will be invoked directly from the client app and can provide a user experience to guide a user through the fulfillment of that action. This is accomplished by using Client Action Handlers.

### Client Action Handlers

Client Action Handlers allow your App to deliver a user experience to a Watson Work Services 
client. You will need to register a call back URL that the client can invoke for specified actions 
so that the client can recognize and enable your action for users. Once a user invokes your 
action through the client, your App can access context. 

Here’s the flow for client action handlers:

![Client Action Handlers flow](../images/action_handler.jpg)

Currently you can register a Client Action Handler to deal with configuration of your App, and 
this supports two configuration use cases. For a user in a space, your App can provide 
configuration called "space configuration". Also, your app can provide configuration for a 
team, so that a team administrator can set the appropriate configuration for your app for their 
entire team, called "team configuration". 

### Space Configuration 



### Team Configuration 




