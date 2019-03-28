---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-28"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:important: .important}
{:note: .note}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# Navigating the dashboard
{: #iov-insights}

You can track all the deployments you are monitoring through the {{site.data.keyword.aios_short}} dashboard. The dashboard is your main view into {{site.data.keyword.aios_short}}.

  ![Insight tabs](images/insight-tabs.png)

{: shortdesc}

## Insights
{: #iov-dash-tab}

The Insights tab ( ![Insight dashboard](images/insight-dash-tab.png) ) provides a high-level view of your deployment monitoring.

  ![Insight dashboard](images/insight-dashboard.png)

- ***Deployments Monitored*** - In this example, a total of 10 deployments are being monitored. Eight of the ten deployments are shown as individual tiles below.

- ***Accuracy Alerts*** - A total of 3 Accuracy alerts are represented in the tiles below by purple shading. In this example, the `Driver Performance`, `Market Analytics`, and `Pricing Risk` deployments show Accuracy values of `60%`, `65%`, and `79%`, respectively.

- ***Fairness Alerts*** - There are a total of 6 Fairness alerts, represented in the tiles below by both purple shading, and by a small `BIAS` tag. In this example, the `Driver Performance`, `Market Analytics`, `Regulatory Compliance`, `Fraud Detection`, `Premium Optimization`, and `Damage Cost Estimator` deployments show Fairness values of `59%`, `68%`, `62%`, `64%`, `79%`, and `63%`, respectively.

Each tile provides a summary of monitoring activity for that deployment. Note that the `Call Center Routing` deployment tile shows no issues, indicating a fairly stable, accurate model.

Select any of the individual deployment tiles to view more details about that deployment. See [Monitoring Fairness, Average Requests per Minute, and Accuracy](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-itc-timechart).

## Configuration
{: #iov-config-tab}

The Configuration tab ( ![Config tab](images/insight-config-tab.png) ) opens a Configuration Summary for the selected deployment.

  ![Config summary](images/insight-config-summary.png)

From here, you can directly edit the configuration settings for your deployment monitor.

## Transactions
{: #iov-transact-tab}

The Transactions tab ( ![Transactions tab](images/insight-transact-tab.png) ) lets you search a specific transaction ID to explain a particular deployment transaction. For more information, see [Monitoring explainability](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-ie-ov).

## Help tab
{: #iov-help-tab}

The Help tab ( ![Transactions tab](images/insight-help-tab.png) ) provides additional information to assist you in using {{site.data.keyword.aios_short}}.
