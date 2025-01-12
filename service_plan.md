---

copyright:
  years: 2019, 2021
lastupdated: "2021-08-09"

keywords: IBM Cloud, Activity Tracker, service plan, price
subcollection: activity-tracker

---

{{site.data.keyword.attribute-definition-list}}


# Service plans
{: #service_plan}

Different pricing plans are available that you can choose for an {{site.data.keyword.at_full_notm}} instance. Each plan defines the number of days that data is retained for search, the number of users allowed to manage the data, and the features that are enabled.
{: shortdesc}

This information applies only if you use an {{site.data.keyword.at_full}} [hosted event search offering](/docs/activity-tracker?topic=activity-tracker-service_plan).
{: important}


| Plan                          | Number of days that data is available for seach | Number of users per plan | Plan ID |
|-------------------------------|-------------------------------------------------|--------------------------|---------|
| `HIPAA 30 day Event Search`   | 30                                              | 25                       | 254d26dc-3ef5-4006-912c-954186a0d033 |
| `30 day Event Search`         | 30                                              | Unlimitted               | e914263e-8b62-475e-8206-938e3a31ad26 |
| `14 day Event Search`         | 14                                              | Unlimitted               | b7f77c86-adde-4e32-8a1b-daba35b1d4fa |
| `7 day Event Search`          | 7                                               | Unlimitted               | 9aae7491-5cb6-43eb-9b7a-3e0456c781f0 |
| `Lite`   `[*]`                | Data is not available for search                | 1                        | 6efc5a58-4289-4632-867f-5a25e817bfe9 |
{: caption="Table 1. List of service plans" caption-side="top"} 

`[*]` In the lite plan, the log line is not formatted.
{: important}

{{site.data.keyword.at_full_notm}} offers a `Lite` plan that you can use to view your events as they pass through the system. You can view events by using event tailing. You can also design filters to prepare for upgrading to a longer retention period plan. This plan has a 0-day retention period.


## Features by plan
{: #svcplan_features}

The following tables outline the different features that are included in each service plan:

| Feature                              | `HIPAA 30 day Event Search` plan | `30 day Event Search` plan | `14 day Event Search` plan    | `7 day Event Search` plan     | `Lite` plan | 
|--------------------------------------|-------------------------|-------------------------------|-----------------------------|--------------|----------|
| `Live streaming tail`                | ![Checkmark icon](images/checkmark-icon.svg) | ![Checkmark icon](images/checkmark-icon.svg) | ![Checkmark icon](images/checkmark-icon.svg) |![Checkmark icon](images/checkmark-icon.svg) |![Checkmark icon](images/checkmark-icon.svg)|
| `Events are stored and searchable`                | ![Checkmark icon](images/checkmark-icon.svg) | ![Checkmark icon](images/checkmark-icon.svg) | ![Checkmark icon](images/checkmark-icon.svg) |![Checkmark icon](images/checkmark-icon.svg) | |
| `Archiving of events`                             | ![Checkmark icon](images/checkmark-icon.svg) | ![Checkmark icon](images/checkmark-icon.svg) | ![Checkmark icon](images/checkmark-icon.svg) |![Checkmark icon](images/checkmark-icon.svg) | |
| `Multi-channel Alerting`                      | ![Checkmark icon](images/checkmark-icon.svg)  | ![Checkmark icon](images/checkmark-icon.svg) | ![Checkmark icon](images/checkmark-icon.svg) |![Checkmark icon](images/checkmark-icon.svg) | |
| `Exporting events`                              | ![Checkmark icon](images/checkmark-icon.svg) | ![Checkmark icon](images/checkmark-icon.svg) | ![Checkmark icon](images/checkmark-icon.svg) |![Checkmark icon](images/checkmark-icon.svg) | |
| `Definig custom parsing templates`              | ![Checkmark icon](images/checkmark-icon.svg) | ![Checkmark icon](images/checkmark-icon.svg) | ![Checkmark icon](images/checkmark-icon.svg) |![Checkmark icon](images/checkmark-icon.svg) | |
| `Configuring exclusion rules from the UI`   | ![Checkmark icon](images/checkmark-icon.svg) | ![Checkmark icon](images/checkmark-icon.svg) | ![Checkmark icon](images/checkmark-icon.svg) |![Checkmark icon](images/checkmark-icon.svg) | |
| `Creating views`               | ![Checkmark icon](images/checkmark-icon.svg) | ![Checkmark icon](images/checkmark-icon.svg) | ![Checkmark icon](images/checkmark-icon.svg) |![Checkmark icon](images/checkmark-icon.svg) | |
| `Creating dashboards`               | ![Checkmark icon](images/checkmark-icon.svg) | ![Checkmark icon](images/checkmark-icon.svg) | ![Checkmark icon](images/checkmark-icon.svg) |![Checkmark icon](images/checkmark-icon.svg) | |
| `Creating screens`               | ![Checkmark icon](images/checkmark-icon.svg) | ![Checkmark icon](images/checkmark-icon.svg) | ![Checkmark icon](images/checkmark-icon.svg) |![Checkmark icon](images/checkmark-icon.svg) | |
| `Analyzing logs in different contexts`       | ![Checkmark icon](images/checkmark-icon.svg) | ![Checkmark icon](images/checkmark-icon.svg) | ![Checkmark icon](images/checkmark-icon.svg) |![Checkmark icon](images/checkmark-icon.svg) | |
{: caption="Table 2. List of features available that are available for each service plan" caption-side="top"} 


