---

copyright:
  years: 2019, 2021
lastupdated: "2021-09-30"

keywords: IBM Cloud, Activity Tracker, streaming, API

subcollection: activity-tracker

---

{{site.data.keyword.attribute-definition-list}}

# Managing streaming by using the API
{: #streaming-manage-api}


{{site.data.keyword.at_full}} provides an API that you can use to configure streaming for an {{site.data.keyword.at_full_notm}} instance.
{: shortdesc}

This information applies only if you use an {{site.data.keyword.at_full}} [hosted event search offering](/docs/activity-tracker?topic=activity-tracker-service_plan).
{: important}

See [Configure streaming](/docs/activity-tracker?topic=activity-tracker-streaming#streaming-1) for more information on roles required for streaming.
{: note}

## Get details of the streaming configuration
{: #streaming-api-get-conf}

Use [this method](https://{DomainName}/apidocs/activity-tracker#get-v1-config-stream){: external} to get the details about an existing streaming configuration.

```text
curl --request GET https://api.eu-gb.logging.cloud.ibm.com/v1/config/stream  
 -H "content-type: application/json"  
 -H "servicekey: <SERVICE_KEY>"  
```
{: pre}

The response will be similar to the following:

```text
{"status":"active","brokers":["kafka-0.mh-svc1-0000.eu-de.containers.appdomain.cloud:9093","kafka-1.mh-sv2.eu-de.containers.appdomain.cloud:9093","kafka-2.mh-sv3.eu-de.containers.appdomain.cloud:9093"],"topic":"at-london-topic","user":"token"}
```
{: codeblock}


## Delete the streaming configuration
{: #streaming-api-delete-conf}

Use [this method](https://{DomainName}/apidocs/activity-tracker#delete-v1-config-stream){: external} to delete an existing streaming configuration.

```text
curl --request DELETE https://api.eu-gb.logging.cloud.ibm.com/v1/config/stream  
 -H "content-type: application/json"  
 -H "servicekey: <SERVICE_KEY>"
```
{: pre}

The response will be similar to the following if the configuration is successfully deleted:

```text
{"deleted":true}
```
{: codeblock}

If an incorrect service key was specified, a response similar to the following will be returned: 

```text
{"error":"Service Key Validation Error: Invalid or deactivated servicekey","status":"error","code":"NotAuthorized"}
```
{: codeblock}

## Configure streaming
{: #streaming-api-conf}

Use [this method](https://{DomainName}/apidocs/activity-tracker#post-v1-config-stream){: external} to create a streaming configuration.

```text
curl --request POST https://api.eu-gb.logging.cloud.ibm.com/v1/config/stream  
 -H "content-type: application/json"  
 -H "servicekey: <SERVICE_KEY>"  
 -d '{"brokers":["<BROKERS>"],"topic":"topic","user":"token","password":"<COS_SERVICE_CREDENTIAL_API_KEY>"}'
 ```
 {: pre}

The response will be similar to the following if the configuration is successfully configured:

 ```text
 {"status":"active","brokers":["kafka-0.mh-svc1-0000.eu-de.containers.appdomain.cloud:9093","kafka-1.mh-sv2.eu-de.containers.appdomain.cloud:9093","kafka-2.mh-sv3.eu-de.containers.appdomain.cloud:9093"],"topic":"at-london-topic","user":"token"}
 ```
 {: codeblock}

## Update the streaming configuration
{: #streaming-api-update-conf}

Use [this method](https://{DomainName}/apidocs/activity-tracker#put-v1-config-stream){: external} to update a streaming configuration.

```text
curl --request PUT https://api.eu-gb.logging.cloud.ibm.com/v1/config/stream  
 -H "content-type: application/json"  
 -H "servicekey: <SERVICE_KEY>"  
 -d '{"brokers":["<BROKERS>"],"topic":"topic","user":"token","password":"<COS_SERVICE_CREDENTIAL_API_KEY>"}' 
```
{: pre}

The response will be similar to the following if the configuration is successfully updated:

 ```text
{"status":"active","brokers":["kafka-0.mh-svc1-0000.eu-de.containers.appdomain.cloud:9093","kafka-1.mh-sv2.eu-de.containers.appdomain.cloud:9093","kafka-2.mh-sv3.eu-de.containers.appdomain.cloud:9093"],"topic":"at-london-topic","user":"token"}
 ```
 {: codeblock}

If streaming is not configured, the following will be returned when trying to do an update:

```text
{"error":"Streaming configuration does not exist","code":"NotFound","status":"error"}
```
{: codeblock}

## Check the status of a streaming configuration
{: #streaming-api-conf-status}

To check if streaming is enabled or disabled, you can use either the GET or PUT methods.

When streaming is not enabled, the following is returned when running the [GET method](#streaming-api-get-conf): 

```text
{"error":"Not found","code":"NotFound","status":"error"}
```
{: codeblock}

When streaming is not enabled, the following is returned when running the [PUT method](#streaming-api-update-conf): 

```text
{"error":"Streaming configuration does not exist","code":"NotFound","status":"error"}
```
{: codeblock}

## List streaming exclusion rules
{: #streaming-api-list-rules}

Use [this method](https://{DomainName}/apidocs/activity-tracker#get-v1-config-stream-exclusions){: external} to list existing streaming exclusion rules.

```text
curl --request GET https://api.eu-gb.logging.cloud.ibm.com/v1/config/stream/exclusions  
 -H "content-type: application/json"  
 -H "servicekey: <SERVICE_KEY>"
 ```
 {: pre}

The response will be similar to the following:

 ```text
 [{"hosts":[],"apps":[],"title":"Exclude Rule 1","query":"host:iam-am (action read)","active":true,"id":"xxxxxxxxxx"}]
 ```
 {: codeblock}

## Get details about a streaming exclusion rule 
{: #streaming-api-get-rules}

Use [this method](https://{DomainName}/apidocs/activity-tracker#get-v1-config-stream-exclusions-rule-id){: external} to get details of an existing streaming exclusion rule.

```text
curl --request GET https://api.eu-gb.logging.cloud.ibm.com/v1/config/stream/exclusions/{ruleId}  
 -H "content-type: application/json"  
 -H "servicekey: <SERVICE_KEY>"  

```
{: pre}

The response will be similar to the following:

```text
{"hosts":[],"apps":[],"title":"Exclude Rule 1","query":"host:iam-am (action read)","active":true,"id":"xxxxxxxxxx"}
```
{: codeblock}

## Create a streaming exclusion rule
{: #streaming-api-add-rules}

Use [this method](https://{DomainName}/apidocs/activity-tracker#post-v1-config-stream-exclusions){: external} to create a streaming exclusion rule.

```text
curl --request POST https://api.eu-gb.logging.cloud.ibm.com/v1/config/stream/exclusions  
 -H "content-type: application/json"  
 -H "servicekey: <SERVICE_KEY>"  
 -d '{"title": "Exclude Example", "query": "example", "active": true}' 

```
{: pre}

The response will be similar to the following:

```text
{"hosts":[],"apps":[],"title":"Exclude Rule 1","query":"host:iam-am (action read)","active":true,"id":"xxxxxxxxxx"}
```
{: codeblock}

## Delete a streaming exclusion rule
{: #streaming-api-delete-rules}

Use [this method](https://{DomainName}/apidocs/activity-tracker#delete-v1-config-stream-exclusions-rule-id){: external} to delete an existing  streaming exclusion rule.

```text
curl --request DELETE https://api.eu-gb.logging.cloud.ibm.com/v1/config/stream/exclusions/{ruleId}  
 -H "content-type: application/json"  
 -H "servicekey: <SERVICE_KEY>"  
```
{: pre}

The response will be similar to the following:

```text
{"deleted":true}
```
{: codeblock}

## Update a streaming exclusion rule
{: #streaming-api-update-rules}

Use [this method](https://{DomainName}/apidocs/activity-tracker#patch-v1-config-stream-exclusions-rule-id){: external} to update an existing streaming exclusion rule.

```text
curl --request PATCH https://api.eu-gb.logging.cloud.ibm.com/v1/config/stream/exclusions/{ruleId}  
 -H "content-type: application/json"  
 -H "servicekey: <SERVICE_KEY>"  
 -d '{"title": "Exclude Example Update", "query": "example", "active": false}' 
```
{: pre}

```text
{"hosts":[],"apps":[],"title":"Exclude Example Update","query":"example","active":false,"id":"xxxxxxxxxx"}
```
{: codeblock}

