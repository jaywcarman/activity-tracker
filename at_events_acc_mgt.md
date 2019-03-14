---

copyright:
  years: 2019
lastupdated: "2019-03-19"

keywords: IBM Cloud, LogDNA, Activity Tracker, account events

subcollection: logdnaat

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}
{:important: .important}
{:note: .note}

# Account management events  
{: #at_events_acc_mgt}

As a security officer, auditor, or manager, you can use the {{site.data.keyword.at_full_notm}} service to track how users and applications interact with the {{site.data.keyword.cloud_notm}} account. 
{:shortdesc}

The {{site.data.keyword.at_full_notm}} service records user-initiated activities that change the state of a service in {{site.data.keyword.cloud_notm}}. For more information, see [About {{site.data.keyword.at_full_notm}}](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-ov#ov).

To get started monitoring your user's actions, see [{{site.data.keyword.at_full_notm}}](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started#getting-started). 



## Events for managing accounts
{: #at_events_acc_mgt_account}

The following table lists the actions that generate an event:

| Action                               | Description |
|--------------------------------------|-------------|
| `billing.account.create`             | An event is generated when you provison an account, after the account ID is asigned to the account. |
| `billing.account.update`             | An event is generated when you update information about the account.  |
| `billing.account.active`              | An event is generated when you verify the account, that is, an event is generated when the account becomes active. |
| `billing.account.subscription.create` | An event is generated when you create a <a href="/docs/account?topic=account-accounts#subscription-account">Subscription account</a>. |
{: caption="Table 1. Actions that generate events" caption-side="top"} 




## Events for managing users
{: #at_events_acc_mgt_users}

The following table lists the actions that generate an event:

| Action                               | Description |
|--------------------------------------|-------------|
| `user-management.user.create`        | An event is generated when you send an invitation to a user to join an account. The account owner is the only user in the account that can perform this action. |
| `user-management.user.active`        | An event is generated when you activate the user in the account. When the user verifies his email address, the event is generated. |
| `user-management.account.user.delete` | An event is generated when you remove a user from the account. The account owner is the only user in the account that can perform this action. |
{: caption="Table 2. Actions that generate events" caption-side="top"} 



## Events for managing organizations
{: #at_events_acc_mgt_org}

The following table lists the actions that generate an event:


| Action                               | Description |
|--------------------------------------|-------------|
|`billing.account.org.create`          | An event is generated when you add an organization to the account. |
{: caption="Table 3. Actions that generate events" caption-side="top"} 



## Where to look for the events
{: #at_events_acc_mgt_ui}

Events are available in the **US-South** region. 

To view these events, you must [provision an instance](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-provision#provision) of the {{site.data.keyword.at_full_notm}} service in the **US-South** region. Then, you must [open the {{site.data.keyword.at_full_notm}} UI](/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-launch#launch_step2). 







