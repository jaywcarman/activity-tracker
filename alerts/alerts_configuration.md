---

copyright:
  years: 2019, 2021
lastupdated: "2021-08-09"

keywords: IBM Cloud, Activity Tracker, alerts, events

subcollection: activity-tracker

---

{{site.data.keyword.attribute-definition-list}}

# Generating alerts on {{site.data.keyword.cloud_notm}} configuration changes
{: #alerts_configuration}

In {{site.data.keyword.at_full}}, you can create alerts to notify on configuration changes on the {{site.data.keyword.cloud_notm}} account. For example, you can generate notifications that report when services are created, modified, and deleted. These alerts can be limited to specific resources, or can apply to any services offered within the {{site.data.keyword.cloud_notm}}.
{: shortdesc}

This information applies only if you use an {{site.data.keyword.at_full}} [hosted event search offering](/docs/activity-tracker?topic=activity-tracker-service_plan).
{: important}

## Configuring alerts using the console
{: #alerts_configuration_ui}

The following will generate an alert when a service instance is created, deleted, or updated.  These events are recorded in the Frankfurt region, regardless of the region of the service instance.

If you already have an instance in the Frankfurt region, you should use that existing instance.
{: note}

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.

	After you log in with your user ID and password, the {{site.data.keyword.cloud_notm}} UI opens.

2. [Launch the {{site.data.keyword.at_short}} instance UI](/docs/activity-tracker?topic=activity-tracker-launch). The *Everything* view opens.

3. [Define the rule that determines the scope of the data that you want to monitor](/docs/activity-tracker?topic=activity-tracker-views#views_step2).

    In the search bar, enter a query such as `instance.create OR instance.delete OR instance.update`.  The view will now only display events when an instance is created, deleted, or updated.  

    Check that you can see in the view events that report creation, deletion or change of a service instance.

    Filtering on different configuration changes is also possible.  You can filter events that are related to a specific service type.  For example, you can filter on all {{site.data.keyword.keymanagementservicelong_notm}} instances by specifying `kms.instance`.  
    
    To filter when keys are created or deleted in the {{site.data.keyword.keymanagementservicelong_notm}} service, you can specify `kms.secrets.create OR kms.secrets.delete`.
    
    See the events that are generated by the services to determine what configuration changes you want to be alerted.
    {: tip}

    [Save the rule](/docs/activity-tracker?topic=activity-tracker-view_logs#view_logs_step7).  

4. [Configure the alert](/docs/activity-tracker?topic=activity-tracker-alerts#alerts_create). Select 1 or more notification channels. Valid channels are email, Slack, PagerDuty, webHook, and {{site.data.keyword.mon_short}}. Select the type of alert, and define the condition that determines when the alert is triggered. For more information, see [Working with alerts](/docs/activity-tracker?topic=activity-tracker-alerts).

For the query `instance.create OR instance.delete OR instance.update`, the alert will trigger when a service instance is created, deleted, or updated in any region in your account.  If you choose an email notification channel,  will be sent to the designated email address.



## Configuring alerts by using the API
{: #alerts_configuration_api}

You can configure alerts in {{site.data.keyword.at_short}} by using the Configuration REST API. 

- You can use the `POST` method to create an alert.
- You can use the `PUT` method to modify an existing alert. You can use the DELETE method to delete a view and associated alerts.
- You can use the `DELETE` method to delete an alert.

For more information, see [Managing views and alerts programmatically](/docs/activity-tracker?topic=activity-tracker-config-api).

For example, the following sample will create an email alert of type presence that sends a notification when 1 event reporting thr creation, deletion, or change of a service instance occurs in the account:

```text
curl https://api.eu-de.logging.cloud.ibm.com/v1/config/view \
        -H 'content-type: application/json' \
        -H 'servicekey: <SERVICE_KEY>' \
        -d '{
        "name": "Configuration Changes",
        "query": "instance.create OR instance.delete OR instance.update",
        "category": [],
        "channels": [{
            "integration": "email",
            "immediate": false,
            "terminal": true,
            "triggerlimit": 1,
            "triggerinterval": "30",
            "operator": "presence",
            "emails": ["user@mycompany.com"]
        }]}'
```
{: codeblock}


You will create a view as well as an alert, even when using the API.
{: note}


## Sample queries to notify on account configuration changes
{: #alerts_configuration_queries}

### Notify when services are created, modified, and deleted
{: #alerts_configuration_queries_1}

The following table outlines queries that you can use to alert on configuraton changes that report when services are created, modified, and deleted:

| Notify on | Query | UI Source | API hosts |
|-----------|-------|-----------|-----------|
| Create a service instance | `instance.create` | N/A | N/A | 
| Create a service instance for service type | `instance.create` | You can choose a specific service in the source filter section of the UI.   \n   \n For example, to notify when a Key Protect service instance is created, choose `kms` as the source. | You can specify the service in the hosts patameter.   \n   \n For example, to notify when a Key Protect service instance is created, add `\"hosts\": \"kms\"` | 
| Delete a service instance | `instance.delete` | N/A | N/A | 
| Delete a service instance for service type | `instance.delete` | You can choose a specific service in the source filter section of the UI.   \n   \n For example, to notify when a Key Protect service instance is deleted, choose `kms` as the source. | You can specify the service in the hosts patameter.   \n   \n For example, to notify when a Key Protect service instance is deleted, add `\"hosts\": \"kms\"` | 
| Modify a service instance | `instance.update` | N/A | N/A | 
| Modify a service instance for service type | `instance.update` | You can choose a specific service in the source filter section of the UI.   \n   \n For example, to notify when a Key Protect service instance is changed, choose `kms` as the source. | You can specify the service in the hosts patameter.   \n   \n For example, to notify when a Key Protect service instance is changed, add `\"hosts\": \"kms\"` | 
| Create, delete or modify any service instance | `instance.create OR instance.delete OR instance.update` | N/A | N/A | 
{: caption="Table 1. Query samples when services are created, modified, and deleted" caption-side="top"} 

### Notify when account settings are modified
{: #alerts_configuration_queries_2}

The following table outlines queries that you can use to alert on configuraton changes that report when account settings are modified:

| Notify when | Query |
|-----------|-----------|
| An administrator enforces policies for entities to create platform API keys| `action:iam-identity.accountsettings.update AND requestData.request_body.old_restrict_create_platform_apikey:UNRESTRICTED AND requestData.request_body.new_restrict_create_platform_apikey:RESTRICTED` |
| An administrator allows creation of platform API keys without a policy in place| `action:iam-identity.accountsettings.update AND requestData.request_body.old_restrict_create_platform_apikey:RESTRICTED AND requestData.request_body.new_restrict_create_platform_apikey:UNRESTRICTED` |
| An administrator enforces policies for entities to create service IDs| `action:iam-identity.accountsettings.update AND requestData.request_body.old_restrict_create_service_id:UNRESTRICTED AND requestData.request_body.new_restrict_create_service_id:RESTRICTED` |
| An administrator allows creation of service IDs without a policy in place| `action:iam-identity.accountsettings.update AND requestData.request_body.old_restrict_create_service_id:RESTRICTED AND requestData.request_body.new_restrict_create_service_id:UNRESTRICTED` |
| An administrator sets an expiration timeout for sessions | `action:iam-identity.accountsettings.update AND requestData.request_body.old_session_expiration_in_seconds:NOT_SET AND requestData.request_body.new_session_expiration_in_seconds:<SECONDS>`  |
| An administrator sets the default expiration timeout for sessions | `action:iam-identity.accountsettings.update AND requestData.request_body.old_session_invalidation_in_seconds:<SECONDS> AND requestData.request_body.new_session_expiration_in_seconds:NOT_SET` |
| An administrator sets an expiration timeout for sessions | `action:iam-identity.accountsettings.update AND requestData.request_body.old_session_expiration_in_seconds:NOT_SET AND requestData.request_body.new_session_invalidation_in_seconds:<SECONDS>`  |
| An administrator sets the default expiration timeout for sessions | `action:iam-identity.accountsettings.update AND requestData.request_body.old_session_invalidation_in_seconds:<SECONDS> AND requestData.request_body.new_session_invalidation_in_seconds:NOT_SET` |
| An administrator sets an expiration timeout for sessions | `action:iam-identity.accountsettings.update AND requestData.request_body.old_session_expiration_in_seconds:NOT_SET AND requestData.request_body.new_session_invalidation_in_seconds:<SECONDS>`  |
| An administrator sets the default expiration timeout for sessions | `action:iam-identity.accountsettings.update AND requestData.request_body.old_session_invalidation_in_seconds:<SECONDS> AND requestData.request_body.new_session_invalidation_in_seconds:NOT_SET` |
| An administrator restricts user list visibility in the account | `action:iam-identity.accountsettings.update AND requestData.team_directory_enabled:true`  |
| An administrator allows users to see the list of users in the account | `action:iam-identity.accountsettings.update AND requestData.team_directory_enabled:false`  |
| An administrator restricts access to resources in the account | `action:iam-identity.accountsettings.update AND requestData.public_access_enabled:true`  |
| An administrator allows public access to resources in the account | `action:iam-identity.accountsettings.update AND requestData.public_access_enabled:false`  |
| An administrator changes the MFA setting in the account. Valid MFA setting values are: NONE, TOTP, TOTP4ALL, LEVEL1, LEVEL2, LEVEL3 | `action:iam-identity.accountsettings.update AND new_mfa_traits:<MFA_SETTING>` |
{: caption="Table 2. Query samples when account settings are modified" caption-side="top"} 


