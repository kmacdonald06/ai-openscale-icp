---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-05"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Tutorial - (Advanced)
{: #crt-ov}

## Scenario
{: #crt-scenario}

Traditional lenders are under pressure to expand their digital portfolio of financial services to a larger and more diverse audience, which requires a new approach to credit risk modeling. Their data science teams currently rely on standard modeling techniques - like decision trees and logistic regression - which work well for moderate datasets, and make recommendations that can be easily explained. This satisfies regulatory requirements that credit lending decisions must be transparent and explainable.

To provide credit access to a wider and riskier population, applicant credit histories must expand beyond traditional credit, like mortgages and car loans, to alternate credit sources like utility and mobile phone plan payment histories, plus education and job titles. These new data sources offer promise, but also introduce risk by increasing the likelihood of unexpected correlations which introduce bias based on an applicant’s age, gender, or other personal traits.

The data science techniques most suited to these diverse datasets, such as gradient boosted trees and neural networks, can generate highly accurate risk models, but at a cost. Such "black box" models generate opaque predictions that must somehow become transparent, to ensure regulatory approval such as Article 22 of the General Data Protection Regulation (GDPR), or the federal Fair Credit Reporting Act (FCRA) managed by the Consumer Financial Protection Bureau.

The credit risk model provided in this tutorial uses a training dataset that contains 20 attributes about each loan applicant. Two of those attributes - age and sex - can be tested for bias. For this tutorial, the focus will be on bias against sex and age.

{{site.data.keyword.aios_short}} will monitor the deployed model's propensity for a favorable outcome ("No Risk") for one group (the Reference Group) over another (the Monitored Group). In this tutorial, the Monitored Group for sex is `female`, while the Monitored Group for age is `18 to 25`.

## Prerequisites
{: #crt-prereqs}

This tutorial uses a Jupyter notebook that should be run using a "Python 3.5 with Spark" runtime environment. It requires service credentials for the following {{site.data.keyword.cloud_notm}} services:

- {{site.data.keyword.aios_short}}
- Watson Machine Learning
- Db2 Warehouse

The Jupyter notebook will train, create and deploy a German Credit Risk model, configure {{site.data.keyword.aios_short}} to monitor that deployment, and provide seven days' worth of historical records and measurements for viewing in the {{site.data.keyword.aios_short}} Insights dashboard.

## Introduction
{: #crt-intro}

In this tutorial, you will:

- Provision {{site.data.keyword.cloud_notm}} machine learning and storage services
- Set up a Watson Studio project, and run a Python notebook to create, train and deploy a machine learning model
- Run a Python notebook to create a data mart, configure performance, accuracy, and fairness monitors, and create data to monitor
- View results in the {{site.data.keyword.aios_short}} Insights tab

## Provision {{site.data.keyword.cloud_notm}} Services
{: #crt-services}

Login to your [{{site.data.keyword.cloud_notm}} account ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}) with your {{site.data.keyword.ibmid}}. When provisioning services, particularly in the case of Db2 Warehouse, verify that your selected organization and space are the same for all services.

### Provision a Watson Machine Learning service
{: #crt-wml}

- [Provision a Watson Machine Learning instance ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/catalog/services/machine-learning) if you do not already have one associated with your account:

  ![Machine Learning](images/machine_learning.png)

- Give your service a name, choose the Lite (free) plan, and click the **Create** button.

### Provision a Db2 Warehouse service
{: #crt-db2}

- [Provision a Db2 Warehouse service ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/catalog/services/db2-warehouse) if you do not already have one associated with your account:

  ![Db2 Warehouse](images/db2_warehouse.png)

- Give your service a name, choose the Entry plan, and click the **Create** button.

## Create and deploy a machine learning model
{: #crt-make-model}

### Add the `Watson OpenScale and Watson ML engine` notebook to your favorite editor
{: #crt-add-notebook}

- Download the [Watson OpenScale and Watson ML engine ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Watson%20OpenScale%20and%20Watson%20ML%20Engine.ipynb)

### Edit and run the `Watson OpenScale and Watson ML engine` notebook
{: #crt-edit-notebook}

The `Watson OpenScale and Watson ML engine` notebook contains detailed instructions for each step in the Python code you will run. As you work through the notebook, take some time to understand what each command is doing.
{: tip}

- In the "Provision services and configure credentials" section, make the following changes:

    - Follow the instructions to create, copy, and paste an {{site.data.keyword.cloud_notm}} API key.

    - Replace the Watson Machine Learning (WML) and Db2 service credentials with the ones you created previously.

    - If you have an already-existing schema in your Db2 instance that you would like to use for {{site.data.keyword.aios_short}} data, specify it as the SCHEMA_NAME variable. Otherwise, leave the variable set to `None` to use the default Db2 schema.

    - If you previously configured {{site.data.keyword.aios_short}} to use a free internal PostgreSQL database as your data mart, you can switch to a new data mart that uses Db2 Warehouse. To delete your old PostgreSQL configuration and create a new one using Db2 Warehouse, set the KEEP_MY_INTERNAL_POSTGRES variable to `False`.

        The notebook will remove your existing internal PostgreSQL data mart and create a new Db2 data mart with the supplied Db2 credentials. **No data migration will occur**.
        {: important}

- Once you have provisioned your services and entered your credentials, your notebook is ready to run. Run each step of the notebook in sequence. Notice what is happening at each step, as described. Complete all the steps, up through and including the steps in the "Identify transactions for Explainability" section.

The net result is that you will have created, trained, and deployed the **German Credit Risk Model** to your {{site.data.keyword.aios_short}} service instance. {{site.data.keyword.aios_short}} will be configured to check the model for bias against sex (in this case, Female) or age (In this case, 18-25 years old).

## Viewing results
{: #crt-view-results}

### View insights for your deployment
{: #crt-view-insights}

Using the [{{site.data.keyword.aios_short}} dashboard ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://aiopenscale.cloud.ibm.com/aiopenscale/){: new_window}, click on the **Insights** tab:

  ![Insights](images/insight-dash-tab.png)

The Insights page provides an overview of metrics for your deployed models. You can easily see alerts for Fairness or Accuracy metrics that have fallen below the threshold set when running the notebook. The data and settings used in this tutorial will have created Accuracy and Fairness metrics similar to the ones shown here.

  ![Insight overview](images/insight-overview-adv-tutorial-2.png)

### View monitoring data for your deployment
{: #crt-view-mon-data}

Select a deployment by clicking the tile on the Insights page. The monitoring data for that deployment will appear. Slide the marker across the chart to select data for a specific one-hour window. Then select the **View details** link.

  ![Monitor data](images/insight-monitor-data2.png)

Now, you can review the charts for the data you monitored. For this example, you can see that for the "Sex" feature, the group `female` received the favorable outcome "No Risk" slightly less (74%) than the group `male` (78%).

  ![Insight overview](images/insight-review-charts2.png)

### View explainability for a model transaction
{: #crt-view-explain}

Please note that if you are using the internal lite version of PostgreSQL, you may not be able to retrieve your database credentials, which will prevent you from seeing transactions.
{: note}

Select the **View transactions** button from the charts for the latest biased data.

  ![View transactions](images/view_transactions.png)

  A list of transactions where the deployment has acted in a biased manner is listed. Select one of the transactions and click the **Explain** link.

  ![Transaction list](images/transaction_list_cr.png)

You will be taken to the **Explainability** tab, where you will now see an explanation of how the model arrived at its conclusion, including how confident the model was, the factors that contributed to the confidence level, and the attributes fed to the model.

  ![View Transaction](images/view_transaction_cr.png)

## Next steps
{: #crt-next-steps}

- Learn more about [viewing and interpreting the data](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-itc-timechart) and [monitoring explainability](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-ie-ov).
