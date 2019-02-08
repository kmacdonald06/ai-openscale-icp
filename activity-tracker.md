---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-04"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Activity Tracker events
{: #at-events}

When you have {{site.data.keyword.aios_short}} provisioned as a service in your {{site.data.keyword.Bluemix_notm}} account, you can see the following events in the [{{site.data.keyword.Bluemix_notm}} Activity Tracker](https://{DomainName}/docs/services/cloud-activity-tracker/activity_tracker_ov.html#activity_tracker_ov).

## Events for public APIs
{: #at-pubapi}

| Action | Description |
| -- | -- |
| aiopenscale.metrics.create | Store metric in the {{site.data.keyword.aios_short}} instance |
| aiopenscale.payload.create | Log payload in the {{site.data.keyword.aios_short}} instance |

## Events for private APIs
{: #at-priapi}

| Action | Description |
| -- | -- |
| aiopenscale.datamart.configure | Configure the {{site.data.keyword.aios_short}} instance |
| aiopenscale.datamart.delete | Delete the {{site.data.keyword.aios_short}} instance |
| aiopenscale.binding.create | Add service binding to the {{site.data.keyword.aios_short}} instance |
| aiopenscale.binding.delete | Delete service binding from the {{site.data.keyword.aios_short}} instance |
| aiopenscale.subscription.create | Add subscription to the {{site.data.keyword.aios_short}} instance |
| aiopenscale.subscription.delete | Delete subscription from the {{site.data.keyword.aios_short}} instance |
