---
copyright: 'Copyright IBM Corp. 2017'
link: 'files-guide'
is: 'experimental'
---


# Files in IBM Watson Work Services

**Note: OBSOLETE. Need to update to GraphQL variant.  This documentation and underlying APIs and structures ARE subject to change**

## Concepts

- Files can exist in a number of external repositories with various degrees of integration capabilities
- IBM Watson Work Services _provides_ a default Files repository which we will refer to as **Files** in this document
- Files are related to the rest of the object model in Watson Work Services by virtue of two connecting points:
  - a reference to them as part of markdown in a conversation message
  - an annotation of type `File` to a conversation message
- Typically a conversation message contains both, a reference in its content markdown and an annotation
- Uploading a file is simple, just use the REST endpoint described [here](https://developer.watsonwork.ibm.com/docs/api-reference/files)
- Downloading files require that either you already have the URL which is:
  - given back to you as a result of an upload operation
  - derived from a File reference obtained by using GraphQL queries into the Watson Work Services data model
  - derived from a File reference provided in real time via webhook callback due to Watson Work Services model change

## Using GraphQL to inspect model

### Conversation message content

Use a GraphQL query to obtain the message(s) content properties and parse it looking for markdown with format:

`<$file|FILE_REFID|FILE_NAME|WIDTHxHEIGHT>`

Where:
`FILE_REFID` is the actual File Reference Id which is needed to obtain a download URL
`FILE_NAME` is the intended file name
`WIDTH` and `HEIGHT`specify the size of the image in case the file content is of type: `image/jpeg`

Example:
`<$file|ibm0@default@578cf829e4b0c3e87919a2b1@file-bf17cbc5-a5ec-4ecf-940a-b8be4822e49e|Social-9.jpg|1024x768>`


### Conversation message annotations

Use a GraphQL query to obtain the message(s) annotations of either type `generic` or type `file`

#### generic annotations

Similar to the above message created, but instead obtain the message content from the event element called `text`

#### file annotations

The file annotation is identified with an annotation `type` of `file` and will contain the FILE_REFID identified above in the element `fileid` of the annotation payload

As a reference, here is the File annotation payload which is JSON in stringified format:

`"{\"type\":\"file\",\"annotationId\":\"5a8cbcede4b0de791d72efef\",\"type\":\"file\",\"version\":\"1.0\",\"created\":1519172845653,\"createdBy\":\"toscana-service-storage-client-id\",\"updated\":1519172845653,\"updatedBy\":\"toscana-service-storage-client-id\",\"tokenClientId\":\"toscana-service-storage-client-id\",\"fileId\":\"ibm0@default@578cf829e4b0c3e87919a2b1@file-bf17cbc5-a5ec-4ecf-940a-b8be4822e49e\",\"name\":\"Social-9.jpg\",\"size\":139512,\"contentType\":\"image/jpeg\",\"width\":1024,\"height\":768,\"messageRefId\":null}"`

Here is the same information in JSON format:

```
{
  "type": "file",
  "annotationId": "5a8cbcede4b0de791d72efef",
  "type": "file",
  "version": "1.0",
  "created": 1519172845653,
  "createdBy": "toscana-service-storage-client-id",
  "updated": 1519172845653,
  "updatedBy": "toscana-service-storage-client-id",
  "tokenClientId": "toscana-service-storage-client-id",
  "fileId": "ibm0@default@578cf829e4b0c3e87919a2b1@file-bf17cbc5-a5ec-4ecf-940a-b8be4822e49e",
  "name": "Social-9.jpg",
  "size": 139512,
  "contentType": "image/jpeg",
  "width": 1024,
  "height": 768,
  "messageRefId": null
}
```

## Using Webhook events

### Message Created

Obtain the message content element from the event data and refer to above information in the inspecting the model section as it is essentially the same approach.

### Annotation Added

#### Generic Annotation

Obtain the value of `text` element from the annotation payload and refer to the information above in the inspecting the model section

#### File Annotation

Obtain the value of `fileid` element of the annotation payload and refer to the information above in the inspecting the model section

## Deriving a File download URL from a Watson Work Services File reference

This is a three step process:
1. download metadata about the file and decide which method to use to obtain a download URL
2. use either redirect or non-redirect URL to obtain a download URL which will expire in 10 minutes and which should not be considered a permanent URL
3. download the file contents using download URL obtained from step 2

#### Step 1.  Download File Metadata

`https://api.watsonwork.ibm.com/files/api/v1/files/file/<id>`

Where `<id>` is the File identifier obtained via model inspection or webhook notification described earlier

Example:
https://api.watsonwork.ibm.com/files/api/v1/files/file/ibm0@default@578cf829e4b0c3e87919a2b1@file-bf17cbc5-a5ec-4ecf-940a-b8be4822e49e

This yields a JSON structure as follows:

```
{
  "entries": [
    {
      "id": "ibm0@default@578cf829e4b0c3e87919a2b1@file-bf17cbc5-a5ec-4ecf-940a-b8be4822e49e",
      "name": "Social-9.jpg",
      "size": 139512,
      "urls": {
        "metadata": "https://api.watsonwork.ibm.com/files/api/v1/files/file/ibm0@default@578cf829e4b0c3e87919a2b1@file-bf17cbc5-a5ec-4ecf-940a-b8be4822e49e",
        "noredirect_download": "https://api.watsonwork.ibm.com/files/api/v1/files/file/ibm0@default@578cf829e4b0c3e87919a2b1@file-bf17cbc5-a5ec-4ecf-940a-b8be4822e49e/content/noredirect/Social-9.jpg",
        "redirect_download": "https://api.watsonwork.ibm.com/files/api/v1/files/file/ibm0@default@578cf829e4b0c3e87919a2b1@file-bf17cbc5-a5ec-4ecf-940a-b8be4822e49e/content/redirect/Social-9.jpg"
      },
      "created": 1519172842000,
      "createdBy": "97a45340-8f0a-1028-803c-db07163b51b2",
      "contentType": "image/jpeg",
      "scanStatus": "PASS",
      "lastScan": 1519172841111
    }
  ],
  "total_count": 1
}
```

#### Step 2. Decide which method to use to obtain Download URL:

- `noredirect_download` is a URL which will return http status 204 with header `X-Content-Location` an actual URL to the download location which will be valid for only 10 minutes per the `Expires` param on the URL
- `redirect_download` is a URL which will return http status 302 with header `Location` an actual URL to the download location which will be valid for only 10 minutes per the `Expires` param on the URL

#### Step 3. Use Download URL

Note that the download URLs obtained in either `X-Content-Location` or `Location` ** are not to be considered stable and can change ** and for this reason it is a moot point to even describe the URL format in documentation


