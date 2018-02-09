# GraphQL with JSON


<a name="overview"></a>
## Overview

### Version information
*Version* : 1.0.0


### URI scheme
*Host* : api.watsonwork.ibm.com  
*Schemes* : HTTPS




<a name="paths"></a>
## Paths

<a name="graphql-post"></a>
### This endpoint allows to execute a GraphQL query
```
POST /graphql
```


#### Description
This endpoint allows to execute a GraphQL query


#### Parameters

|Type|Name|Description|Schema|Default|
|---|---|---|---|---|
|**Header**|**Authorization**  <br>*required*|Authorization header, in form of `Bearer {access_token}` where `{access_token}` is a JWT token|string||
|**Header**|**X-RequestId**  <br>*optional*|Optional header to be able to replay requests in an idempotent way|string||
|**Query**|**operationName**  <br>*optional*|The name of the operation.|string||
|**Query**|**query**  <br>*optional*|The query to be executed. The query is mandatory, but it can be as a url parameter or in the body.|string||
|**Query**|**variables**  <br>*optional*|The variables to be used with the query.|< string > array||
|**Body**|**body**  <br>*optional*||[GraphQLParams](#graphqlparams)||


#### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|Response of the execution of the GraphQL query|[GraphQLResponse](#graphqlresponse)|
|**400**|Additional information on a field in the GraphQL query that failed to be resolved|[HttpError](#httperror)|


#### Consumes

* `application/json`


#### Produces

* `application/json`


<a name="graphql-get"></a>
### GraphiQL schema exploration tool
```
GET /graphql
```


#### Description
GraphiQL tool that allows to navigate the GraphQL schema, command completion to build GraphQL queries and query execution


#### Parameters

|Type|Name|Description|Schema|Default|
|---|---|---|---|---|
|**Query**|**query**  <br>*optional*|The query to be executed|string||


#### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|GraphiQL HTML Tool|No Content|


#### Produces

* `text/html`




<a name="definitions"></a>
## Definitions

<a name="graphqlerror"></a>
### GraphQLError
Additional information on a field in the GraphQL query that failed to be resolved


|Name|Description|Schema|
|---|---|---|
|**field**  <br>*optional*||[field](#graphqlerror-field)|
|**message**  <br>*optional*|Message explaining why did the field failed to be resolved|string|

<a name="graphqlerror-field"></a>
**field**

|Name|Description|Schema|
|---|---|---|
|**name**  <br>*optional*|Name of the field that produced the error|string|
|**type**  <br>*optional*|Type of error|string|


<a name="graphqlparams"></a>
### GraphQLParams

|Name|Description|Schema|
|---|---|---|
|**data**  <br>*required*||[GraphQLQuery](#graphqlquery)|
|**operationName**  <br>*optional*|Defines the name of the operation|string|
|**variables**  <br>*optional*||[GraphQLVariables](#graphqlvariables)|


<a name="graphqlquery"></a>
### GraphQLQuery
GraphQL Query to be executed

*Type* : object


<a name="graphqlresponse"></a>
### GraphQLResponse
Response of the execution of the GraphQL query


|Name|Description|Schema|
|---|---|---|
|**data**  <br>*optional*||object|
|**errors**  <br>*optional*||< [GraphQLError](#graphqlerror) > array|


<a name="graphqlvariables"></a>
### GraphQLVariables
Key-value map of variables to be used in a GraphQL query

*Type* : object


<a name="httperror"></a>
### HttpError
Additional information for an error when a GraphQL query could not be processed


|Name|Description|Schema|
|---|---|---|
|**message**  <br>*optional*|Description of the error|string|
|**status**  <br>*optional*|HTTP Status Code of the error|integer|





