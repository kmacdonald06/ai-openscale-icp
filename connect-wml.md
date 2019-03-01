---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-01"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# Specifying a Watson Machine Learning service instance
{: #cwml-wml}

Your first step in the {{site.data.keyword.aios_short}} tool is to specify a Watson Machine Learning (WML) instance. Your WML instance is where you store your AI models and deployments.
{: shortdesc}

## Prerequisites
{: #cwml-prereq}

You should have provisioned a WML instance in the same {{site.data.keyword.cloud_notm}} account where the {{site.data.keyword.aios_short}} service instance is present. If you have provisioned a WML instance in some other account, then you will not be able to configure that instance with {{site.data.keyword.aios_short}}.

## Connect your Watson Machine Learning service instance
{: #cwml-config}

{{site.data.keyword.aios_short}} connects to AI models and deployments in a WML instance.

1.  From the home page of the {{site.data.keyword.aios_short}} tool, click **Begin**.

    ![Home page](images/gs-config-start.png)

1.  Select the Watson Machine Learning tile and click **Next**.

    ![Tile selection](images/connect-wml.png)

1.  {{site.data.keyword.aios_short}} checks your {{site.data.keyword.cloud_notm}} account to locate any existing WML instances. You can then select an instance from the **Watson Machine Learning service** drop-down menu.

    ![Select WML service](images/gs-set-wml.png)

1.  (Optional) You also have the option to **Select a different location**, to specify a machine learning location outside of your {{site.data.keyword.cloud_notm}} account. Provide credentials for your location as valid JSON:

    ![Set WML instance](images/gs-get-wml.png)

    Click **Next**.

1.  {{site.data.keyword.aios_short}} checks your selected Machine Learning instance to locate a list of deployments stored in that instance. From the list of deployments, select which ones you will monitor.

    ![Select deployments](images/gs-config-deploy.png)

1.  Click **Next**.
1.  Click **Save**.

### Next steps
{: #connect-next}

{{site.data.keyword.aios_short}} is now ready for you to [specify your database](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-cdb-connect).
