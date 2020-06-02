---

copyright:
  years: 2016, 2019
lastupdated: "2019-04-23"

keywords: annotator clinical data, clinical data, annotation

subcollection: wh-acd
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:table: .aria-labeledby="caption"}

<!-- Name your file `at-events.md` and include it in the Reference nav group in your toc file. -->

# {{site.data.keyword.cloudaccesstrailshort}} events
{: #at_events}

Use the {{site.data.keyword.cloudaccesstrailfull}} service to track how users and applications interact with the {{site.data.keyword.wh-acd_short}} service.
{: shortdesc}

The {{site.data.keyword.cloudaccesstrailfull_notm}} service records user-initiated activities that change the state of a service in {{site.data.keyword.Bluemix_notm}}. For more information, see the [{{site.data.keyword.cloudaccesstrailshort}}](https://cloud.ibm.com/docs/services/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started).

<!-- You can create different sections to group events by area. -->

## List of events
{: #events}

<!-- Make sure you introduce the table with a detailed description that immediately precedes it. For example, see https://cloud.ibm.com/docs/services/cloud-activity-tracker/services?topic=cloud-activity-tracker-cf. -->
The {{site.data.keyword.wh-acd_short}} detects medical entities and relationships in unstructured text. The detection event can be executed with either a pre-defined flow id or a dynamic flow without the flow id. The detection event is called **wh-acd.analyze.evaluate** in the following table. 

{{site.data.keyword.IBM_notm}} is responseible for backups and high availability of the activity events for the {{site.data.keyword.wh-acd_short}} service in each supported region. The retention period for both successful or failed detection events is **two-weeks**. The consumers may open a service now ticket to retrieve additional information regarding a specific call as long as the call is made within a **two week** period. The **service now** ticket includes the request id for the dynamic flow scenario, and includes the pre-defined flow id and the request id for the pre-defined flow scenario.
{:important}


An management event is generated when profiles, flows, or cartridges are created, read, update or deleted. In addition, an event is also generated when all tenant data is deleted. The following table is a list of actions that generate events.






| Action | Description |
|:-----------------|:-----------------|
| wh-acd.analyze.evaluate | Detect medical entities in unstructured text. | 
| wh-acd.profile.create | Create a profile. |
| wh-acd.profile.read   | Read   a profile. |
| wh-acd.profile.update | Update a profile. |
| wh-acd.profile.delete | Delete a profile. |
| wh-acd.flow.create | Create a flow. |
| wh-acd.flow.read   | Read   a flow. | 
| wh-acd.flow.update | Update a flow. |
| wh-acd.flow.delete | Delete a flow. |
| wh-acd.cartridges.create | Create a cartridge. | 
| wh-acd.cartridges.read   | Read   a cartridge. | 
| wh-acd.cartridges.update | Update a cartridge. |
| wh-acd.cartridge.deploy | Deploy a cartridge. |
| wh-acd.alluserdata.delete | Delete a tenant's data. |
{: caption="Table 1. Actions that generate events" caption-side="top"}

## Where to view the events
{: #ui}

{{site.data.keyword.cloudaccesstrailshort}} events are available in the {{site.data.keyword.cloudaccesstrailshort}} **account domain** that is available in the {{site.data.keyword.Bluemix_notm}} region where the events are generated.
