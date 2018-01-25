---
copyright: 'Copyright IBM Corp. 2017'
link: 'troubleshooting-apps'
is: 'published'
---
## Troubleshooting Apps

An App, its fields and its registered outbound webhooks need to fulfill certain requirements. When creating or editing an App Watson Work Services will respond with an error, if the requirements are not met. Error messages will be shown.

The tables below summarize the most important errors including further details and potential error causes.


Errors regarding values for certain App fields:

| error message | error tag/error detail tag | details|
|------|:-------------|:-------------|
| The App name cannot be blank | `APP_NAME_BLANK` | The App name shall not be empty and shall not only contain space characters. |
| The App name is already in use, try a different name | `APP_NAME_CONFLICT` | App names are required to be unique, this is done so that users can understand and differentiate amongst Apps. |
| Invalid URI syntax | `APP_URI_INVALID` | An App field which expects an URI/URL (Configuration URL, Terms of Service URL or OAuth2 Redirect URI) does not met the URI syntax. |
| Invalid URI syntax: protocol must be 'https' | `APP_URI_NO_SCHEME` or `APP_URI_WRONG_SCHEME` | Only 'https' is allowed for an App field which expects an URI/URL (Configuration URL, Terms of Service URL or OAuth2 Redirect URI). |


Errors regarding the webhook URL of an outbound webhook:

| error message | error tag/error detail tag | details|
|------|:-------------|:-------------|
| Invalid webhook URL: URL formed incorrectly. | `OBW_WEBHOOK_URL_INVALID` | The given webhook URL could not be interpreted as an URL. |
| Invalid webhook URL: protocol must be 'https'. | `OBW_WEBHOOK_URL_WITHOUT_HTTPS` | Only 'https' is allowed for a webhook URL. |
| Invalid webhook URL: URL contains [length] characters but must contain at least 12 characters. | `OBW_WEBHOOK_URL_LENGTH` | The given webhook URL is too short. |
| Invalid webhook URL: URL contains [length] characters but must not contain more than 2000 characters. | `OBW_WEBHOOK_URL_LENGTH` | The given webhook URL is too long. |
| Invalid webhook URL: URL must not contain IP address. | `OBW_WEBHOOK_URL_MISSING_HOSTNAME` | IP addresses are not allowed in webhook URLs. |
| Invalid webhook URL: URL must not resolve to local address and cannot contain 'localhost'. | `OBW_WEBHOOK_URL_FOR_LOCAL_ADDRESS` | The webhook URL can not be a local address and is not allowed to have 'localhost' as its host name. |
| Invalid webhook URL: The host name cannot be resolved. | `OBW_WEBHOOK_URL_HOSTNAME_UNKNOWN` | The host name in the given webhook URL could not be resolved. |
| Invalid webhook URL: URL resolves to ... | `OBW_WEBHOOK_URL_RESOLVES_TO_BAD_IPADDRESS` | The given webhook URL resolves to an address which is not allowed to be used as general end point. See description of field 'callbackUrl' in [Webhooks API Reference](../references/V1_OutboundCallback.yml) for further details. |


Errors regarding the verification of the webhook URL of an outbound webhook.
The following errors occur when a webhook is enabled or when the App is being updated (or it's outbound webhook is being updated). These changes will trigger the verification of the webhook URL.
Also see [Webhooks API Reference](../references/V1_OutboundCallback.yml) for further details on the verification call.  

| error message | error tag/error detail tag | details|
|------|:-------------|-------------|
| Verification of outbound webhook endpoint failed. Self signed certificate is not allowed. | `OBW_VERIFICATION_CERTIFICATE_SELF_SIGNED_NOT_ALLOWED` | The webhook end point is using a self-signed certificate. A self-signed certificate is not allowed unless it had been explicitly allowed by checking the **Allow Self-signed certificate** in the Listen to events section of your App. |
| Verification of outbound webhook endpoint failed. 'CertPathValidatorException' occurred while certificate validation. | `OBW_VERIFICATION_CERTIFICATE_UNAUTHORIZED` | The certificate used by the webhook end point could not be validated. |
| Verification of outbound webhook endpoint failed. Certificate is expired. | `OBW_VERIFICATION_CERTIFICATE_EXPIRED` | The certificate used by the webhook end point has expired. |
| Verification of outbound webhook endpoint failed. Certificate is not yet valid. | `OBW_VERIFICATION_CERTIFICATE_NOT_YET` | The certificate used by the webhook end point is not yet valid. |
| 'Verification of outbound webhook endpoint failed. Certificate has been revoked. | `OBW_VERIFICATION_CERTIFICATE_REVOKED` | The certificate used by the webhook end point has been revoked. |
| Verification of outbound webhook endpoint failed. Host name does not match the certificate subject provided by the peer. | `OBW_VERIFICATION_CERTIFICATE_MISMATCH` | The host name of the certificate used by the webhook end point does not match the certificate subject provided by the peer. |
| Verification of outbound webhook endpoint failed. Connection failed because of a bad gateway. | `OBW_VERIFICATION_CONNNECTION_BAD_GATEWAY` | Connection to the webhook end point could not be setup, because of a bad gateway HTTP error. |
| Verification of outbound webhook endpoint failed. Connection was refused. | `OBW_VERIFICATION_CONNNECTION_REFUSED` | Connection to the webhook end point could not be setup, because the webhook end point refuses it. |
| Verification of outbound webhook endpoint failed. Connection timed out. | `OBW_VERIFICATION_CONNNECTION_TIMEOUT` | Connection to the webhook end point could not be setup, because the connection timed out. |
| Verification of outbound webhook endpoint failed. The handshake failed because of non-matching TLS version. | `OBW_VERIFICATION_HANDSHAKE_BAD_TLS` | The handshake for the connection to the webhook end point failed, because the webhook end point does not support TLSv1.2 - see description of field 'callbackUrl' in [Webhooks API Reference](../references/V1_OutboundCallback.yml) for further details. |
| Verification of outbound webhook endpoint failed. The handshake failed for unknown reason, possibly because of non-matching TLS ciphers. | `OBW_VERIFICATION_HANDSHAKE_ERROR` | The handshake for the connection to the webhook end point failed. One reason for this failure is that the webhook end point does not support one of the required TLS ciphers - see description of field 'callbackUrl' in [Webhooks API Reference](../references/V1_OutboundCallback.yml) for further details. |
| Verification of outbound webhook endpoint failed. HTTP status response code is not 200. | `OBW_VERIFICATION_RESPONSE_STATUSCODE` | The webhook end point does not respond with HTTP status code 200 on the verification call. |
| Verification of outbound webhook endpoint failed. Response has no body. | `OBW_VERIFICATION_RESPONSE_HAS_NO_BODY` | The response of the webhook end point on the verification call does not contain a body. |
| Verification of outbound webhook endpoint failed. Cannot parse response body. | `OBW_VERIFICATION_RESPONSE_WRONG_FORMAT` | The response body of the webhook end point on the verification call does match the expected format and can not be parsed. |
| Verification of outbound webhook endpoint failed. Response does not contain verification challenge. | `OBW_VERIFICATION_RESPONSE_NO_CHALLENGE` | The response body of the webhook end point on the verification call does not contain the expected verification challenge. |
| Verification of outbound webhook endpoint failed. Response field is not identical to challenge. | `OBW_VERIFICATION_RESPONSE_WRONG_CHALLENGE` | The response body of the webhook end point on the verification call does not contain the expected verification challenge. |
| Verification of outbound webhook endpoint failed. Response has no 'X-OUTBOUND-TOKEN' header. | `OBW_VERIFICATION_RESPONSE_NO_HMAC` | The response header of the webhook end point on the verification call does not contain the expected header field 'X-OUTBOUND-TOKEN'. |
| Verification of outbound webhook endpoint failed. Value of response header 'X-OUTBOUND-TOKEN' is not correct. | `OBW_VERIFICATION_RESPONSE_WRONG_HMAC` | The response header of the webhook end point on the verification call does not contain the expected value for header field 'X-OUTBOUND-TOKEN'. |
