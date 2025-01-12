---

copyright:
  years: 2019, 2021
lastupdated: "2021-08-09"

keywords: IBM Cloud, Activity Tracker, streaming

subcollection: activity-tracker

---

{{site.data.keyword.attribute-definition-list}}

# Configuring conditional streaming
{: #streaming-conditional}

In an {{site.data.keyword.at_full}} instance, you can configure streaming exclusion rules through the UI to filter what data is streamed.
{: shortdesc}

This information applies only if you use an {{site.data.keyword.at_short}} [hosted event search offering](/docs/activity-tracker?topic=activity-tracker-service_plan).
{: important}

You must have manager access for {{site.data.keyword.at_short}} to define exclusion rules.  See [Configure streaming](/docs/activity-tracker?topic=activity-tracker-streaming#streaming-1) for more information on roles required for streaming.
{: note}

Complete the following steps to define an exclusion rule:

1. [Launch the {{site.data.keyword.at_full_notm}} web UI](/docs/services/activity-tracker?topic=activity-tracker-launch).

2. Select the **Settings** icon ![Configuration icon](images/admin.png "Admin icon"). Then select **Streaming** &gt; **Exclusion Rules**. 

3. Select **Add Rule**. The **Create Rule** section opens.

4. Enter a name for the rule in the section **What is this rule for?**.

5. Enter the exclusion criteria by adding a query. For more information on how to build a query, see [Select the set of events to display through a view by applying a search query](/docs/activity-tracker?topic=activity-tracker-views#views_step2).

6. Click **Save**.







