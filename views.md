---

copyright:
  years: 2019, 2021
lastupdated: "2021-08-09"

keywords: IBM Cloud,Activity Tracker, search, filter, events

subcollection: activity-tracker

---

{{site.data.keyword.attribute-definition-list}}


# Searching events by using queries
{: #views}

Through the {{site.data.keyword.at_full_notm}} web UI, you can apply search and filtering criteria to define the set of events that are displayed through a custom view.
{: shortdesc}

This information applies only if you use an {{site.data.keyword.at_full}} [hosted event search offering](/docs/activity-tracker?topic=activity-tracker-service_plan).
{: important}

## Prerequisites
{: #views_prereqs}

Before you start, check that your user ID has permissions to launch the web UI and view events. The following table lists the minimum roles that a user must have to be able to launch the {{site.data.keyword.at_full_notm}} web UI, and view, search, and filter events:

| Role                      | Permission granted            |
|---------------------------|-------------------------------|  
| Platform role: `Viewer`     | Allows the user to view the list of service instances in the Observability dashboard. |
| Service role: `Reader`      | Allows the user to launch the web UI and view events in the web UI.  |
{: caption="Table 1. IAM roles" caption-side="top"} 

For more information on how to configure policies for a user, see [Granting user permissions to a user or service ID](/docs/services/activity-tracker?topic=activity-tracker-iam_view_events#iam_view_events).



## Step 1. Go to the web UI and select a view
{: #views_step1}

Complete the following steps:

1. [Go to the web UI](/docs/services/activity-tracker?topic=activity-tracker-launch#launch).
2. Click the **Views** icon ![Views icon](images/views.png "Views icon").
3. Select **Everything** or a view. 


## Step 2. Select the set of events to display through a view by applying a search query
{: #views_step2}

To search for specific events, you can apply a search query. 

* You can do simple searches (single term string search), compound search (multiple search terms and operators), field searches if the log line can be parsed, and others.
* AND and OR operators are case-sensitive and must be capitalized.
* Use `FieldName:==FieldValue` to search for a specific field value.
* Use `FieldName:Value` to search for field values that start with that value. 

You can only search events for the number of days that is specified through the instance's service plan.
{: important}


Complete the following steps:
1. Enter a search query. 
2. Press **Enter**. 

As you apply a query, notice that the name of the view changes to **Unsaved View**.


### Query for events that are generated by a service
{: #views_step2_1}

To filter out events for a specific service, you need to enter the following query:

```text
_platform:==SERVICENAME
```
{: codeblock}

Where `SERVICENAME` is the name of the service in the {{site.data.keyword.cloud_notm}}.

The following table lists core services:

| Events that are generated by               | Value                         | Sample query                     |
|--------------------------------------------|-------------------------------|----------------------------------|
| [IAM Access Management service](/docs/services/activity-tracker?topic=activity-tracker-at_events_iam#at_events_iam_policies)  | `iam-am`  | `_platform:==iam-am`    |
| [IAM Identity service](/docs/services/activity-tracker?topic=activity-tracker-at_events_iam#at_events_iam_login)   | `iam-identity`    | `_platform:==iam-identity`  |
| [IAM Access Groups service](/docs/services/activity-tracker?topic=activity-tracker-at_events_iam#at_events_iam_access)   | `iam-groups`  | `_platform:==iam-groups`     |
| [Resource controller service](/docs/services/activity-tracker?topic=activity-tracker-cloud_services#platform_core_integrated)   | `BSS`  | `_platform:==BSS`  |            
{: caption="Table 2. Query by service name" caption-side="top"}



### Query for sets of events that are generated by a service
{: #views_step2_2}

When a service generates different types of events, you can enter the following query:

```text
_platform:==SERVICENAME [(action TYPEOFACTION)] 
```
{: codeblock}

Where 

* `SERVICENAME` is the name of the service in the {{site.data.keyword.cloud_notm}}
* `TYPEOFACTION` is a compound query where you can use AND and OR operators, and also use `-` to exclude data. Notice that the `AND` and `OR` operators are case-sensitive and must be capitalized.


The following table show examples of how to query for a group of events that is generated by a service:

| Events that are generated by               | Type of events     | Sample query                     |
|--------------------------------------------|--------------------|---------------------------------|
| `IAM Identity service`                     | [Login events](/docs/services/activity-tracker?topic=activity-tracker-at_events_iam#at_events_iam_login) | `_platform:==iam-identity (action login)`  |
| `IAM Identity service`                     | [API key events](/docs/services/activity-tracker?topic=activity-tracker-at_events_iam#at_events_iam_apikeys) | `_platform:==iam-identity (action user-apikey) -(action login)`  |
| `IAM Identity service`                     | [Account service ID events](/docs/services/activity-tracker?topic=activity-tracker-at_events_iam#at_events_iam_serviceids) | `_platform:==iam-identity (action account-serviceid)`  |
| `Resource controller`                      | [Provisioning and managing service instances](/docs/services/activity-tracker?topic=activity-tracker-at_events_rc#rc_provision) | `_platform:==BSS (action instance)`  | 
| `Resource controller`                      | [Managing users in the account](/docs/services/activity-tracker?topic=activity-tracker-at_events_acc_mgt#at_events_acc_mgt_users)   |  `_platform:==BSS (action user-management.user)`  |                   |
{: caption="Table 3. Samples of more complex queries" caption-side="top"}


### Query for events that have a specific action
{: #views_step2_3}

Each event has an **action** field that informs about the action that triggered the event. You can enter the following query to search for all events that have the same action:

```text
action ACTIONVALUE
```
{: codeblock}

Where `ACTIONVALUE` is the value of the action field or part of the value.

The following table show examples of queries for different actions:

| Action                 | Sample query                     |
|------------------------|----------------------------------|
| Provision a service    | `action instance.create`         |
| Remove an instance     | `action instance.delete`         |
| Add a user             | `action user-management.user.create` |
{: caption="Table 4. Samples of queries by action type" caption-side="top"}

### Query for events with a specific reason code
{: #views_step2_4}

You can enter the following query to search for events with a specific reason code:

```text
reason.reasonCode:VALUE
```
{: codeblock}

Where *VALUE* represents the reason code value.

For example, to filter events with reason code 500, you can enter the following query:

```text
reason.reasonCode:500
```
{: codeblock}

### Query for events whose action fails
{: #views_step2_5}

When an action requested fails, the field **outcome** is set to **failure**. You can enter the following query to search for these type of events:

```text
outcome:failure
```
{: codeblock}


### Query by event criticallity
{: #views_step2_6}

Each event has a **severity** field that defines the level of threat an action may have on the Cloud. 

Valid values are *normal*, *warning*, and *critical*. 
* **Normal** is set for routine actions in the Cloud. For example, starting an instance, or refreshing a token. 
* **Warning** is set for actions where a Cloud resource is updated or its metadata is modified. For example, updating the version of a worker node, renaming a certificate, or renaming a service instance. 
* **Critical** is set for actions that affect security in the Cloud. For example, changing credentials of a user, deleting data, unauthorized access to work with a Cloud resource.

You can enter the following query to search for these type of events:

```text
severity:VALUE
```
{: codeblock}

Where `VALUE` can be set to *normal*, *warning*, or *critical*

For example, to query for critical events, you can run the following query:

```text
severity:critical
```
{: codeblock}



## Step 3. Create a custom view
{: #views_step3}

After you apply the search query to the **Everything** view or to an existing custom view, complete the following steps to save the outcome as a custom view:

1. In the web UI, click **Unsaved View**.
2. Select **Save as new view / alert**. The *Create new view* page opens.
3. Enter a name for the view in the *Name* field.
4. Optionally, add a category. Enter a name and then click **Add this as new view category**.
5. Optionally, attach an alert. A new section is displayed for you to configure the alert.
6. Click **Save View**



## Step 4. Customize how event lines are displayed through a view
{: #views_step4}

There are different options to customize how you see data in a view:
* You can modify the properties of a view., You can rename a view, add or modify its description, and apply a specific line format.
* You can change the `log format` in the *USER PREFERENCES* section.
* You can apply a line template from the *Tools* section. Notice that this overrides any other line configuration. If you select **Persist these settings**, all views in the UI will show data per the line format that is specified in this section.
* You can apply color to terms or strings by setting **Highlight Terms** in the **Tools** section.



### Change the line format through the view properties page
{: #views_step4_1}

Complete the following steps to modify the format of an event line in a single view:

1. In your view, select **Edit View Properties**. The *Edit View Properties* page opens.

2. Enter a custom line format in the **Custom %LINE Template** section. The default is set to `{{line}}`.

    For more information about the line template guidelines, see [Guidelines](/docs/services/activity-tracker?topic=activity-tracker-views#views_line).

3. Click **Save properties**.



### Change the line format through the user preferences section
{: #views_step4_2}

In the **USER PREFERENCES** section, you can modify the order of the data fields that are displayed per line.

Complete the following steps to modify the format of an event line:

1. In the web UI, click the **Configuration** icon ![Configuration icon](images/admin.png "Admin icon").
2. Select **USER PREFERENCES**. A new window opens.
3. Select **Log Format**.
4. Modify the *Line Format* section to match your requirements. Drag boxes.


### Change the line format through the line template in the tools section
{: #views_step4_3}

Complete the following steps to modify the format of an event line:

1. In the view, click the **Tools** icon ![Tools icon](images/tool.png "Tools icon").
2. In the **Line Template** field, enter your custom line format. For more information about the line template guidelines, see [Guidelines](/docs/services/activity-tracker?topic=activity-tracker-views#views_line).
3. Optionally, click **Persist these settings** to apply the line format to all views.



### Highlight terms
{: #view_events_step4_4}

Complete the following steps to highlight terms in a view:

1. In the view, click the **Tools** icon ![Tools icon](images/tool.png "Tools icon").
2. In the **Line Template** field, enter a word or string in the **Highlight Terms** section.
3. Optionally, click **Persist these settings** to apply these setting to all views.





## Guidelines defining line templates
{: #views_line}

Consider the following guidelines that you must apply when you define a line template:
* Use mustache style `{{field.name}}` or bash style `${field.name}` variables to construct your template. 
* Use `{{line}}` or `$@` to reference the original line. 
* All other characters or strings are interpreted as text literal. 


For example, you can define a line template as `{{initiator.id}} -- {{action}} -- {{message}}` to see these fields for each event in a view.


## Change the name and description of a custom view
{: #views_step5}

You can rename a view. You can add or modify the description of a view.


Complete the following steps:

1. In your view, select **Edit View Properties**. The *Edit View Properties* page opens.

    You can rename the view, add or modify the description of the view, and apply a custom line format.

2. Enter a new name in the **Rename View** section to rename the view.

3. Enter or modify the description in the **Description** section.

4. Click **Save properties**.


