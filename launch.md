---

copyright:
  years: 2019
lastupdated: "2019-03-19"

keywords: IBM Cloud, LogDNA, Activity Tracker, web UI, browser

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

# Navigating to the web UI
{: #launch}

After you provision an instance of the {{site.data.keyword.at_full_notm}} service in the {{site.data.keyword.cloud_notm}}, you can view, monitor, and manage events through the {{site.data.keyword.at_full_notm}} web UI.
{:shortdesc}


## Step 1. Granting IAM policies to a user to view data 
{: #step1}

**Note:** You must be an administrator of the {{site.data.keyword.at_full_notm}} service, an administrator of an {{site.data.keyword.at_full_notm}} instance, or have account IAM permissions to grant other users policies.

The following table lists the minimum policy that a user must have to be able to launch the web UI, and view data:

| Service                              | Role                      | Permission granted       |
|--------------------------------------|---------------------------|---------------------|
| `{{site.data.keyword.at_full_notm}}` | Platform role: Viewer     | Allows the user to view the list of service instances in the Observability dashboard. |
{: caption="Table 1. IAM policies" caption-side="top"} 




## Step 2. Launching the web UI through the {{site.data.keyword.cloud_notm}} UI
{: #launch_step2}

You launch the web UI within the context of an {{site.data.keyword.at_full_notm}} instance, from the {{site.data.keyword.cloud_notm}} UI. 

Complete the following steps to launch the web UI:

1. Log in to your {{site.data.keyword.cloud_notm}} account.

    Click [{{site.data.keyword.cloud_notm}} dashboard ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/login){:new_window} to launch the {{site.data.keyword.cloud_notm}} dashboard.

	After you log in with your user ID and password, the {{site.data.keyword.cloud_notm}} dashboard opens.

2. In the navigation menu, select **Observability**. 

3. Select **Activity Tracker**. 

    The list of instances that are available on {{site.data.keyword.cloud_notm}} is displayed.

4. Select one instance. Then, click **View LogDNA**.

The Web UI opens.


## Getting the web UI URL from the {{site.data.keyword.cloud_notm}}
{: #launch_get}

To get the web UI URL, complete the following steps from a terminal:

1. Set the resource group where the {{site.data.keyword.at_full_notm}} instance is provisioned.

    ```
    export logdna_rg_name=<Resource_Group_Name_Where_LogDNA_Instance_Is_Created>
    ```
    {: codeblock}

2. Set the {{site.data.keyword.at_full_notm}} instance name.

    ```
    export logdna_instance_name=<Your_LogDNA_Instance_Name>
    ```
    {: codeblock}

3. Set the endpoint.

    ```
    export rc_endpoint=resource-controller.cloud.ibm.com
    ```
    {: codeblock}

4. Set the IAM token.

    ```
    export iam_token=$(ibmcloud iam oauth-tokens | grep IAM | grep -oP  "eyJ.*")
    ```
    {: codeblock}

    **Note:** If you are working on a MacOS terminal, the command is as follows: `export iam_token=$(ibmcloud iam oauth-tokens | grep IAM | grep -o  "eyJ.*")`

5. Set the resource group ID.

    ```
    export resource_group_id=$(ibmcloud resource groups | grep "^$logdna_rg_name" | awk '{print $2}')
    ```
    {: codeblock}

6. Set the web UI URL in a variable.

    ```
    export dashboard_url=$(curl -H "Accept: application/json" -H "Authorization: Bearer $iam_token" "https://$rc_endpoint/v1/resource_instances?resource_group_id=$resource_group_id&type=service_instance" | jq ".resources[] | select(.name==\"$logdna_instance_name\") | .dashboard_url")
    ```
    {: codeblock}

7. Get the web UI URL.

    ```
    echo $dashboard_url
    ```
    {: codeblock}

    
