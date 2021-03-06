---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-28"

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

# About
{: #abt-about}

{{site.data.keyword.aios_full}} is an enterprise-grade environment for AI-infused applications, providing enterprises visibility into how AI is being built, used, and delivering return on investment, at the scale of your business.
{: shortdesc}

## Implementation
{: #abt-implement}

Here's how you will implement {{site.data.keyword.aios_short}}:

- **Configure {{site.data.keyword.aios_short}}**: With the easy-to-use graphical environment, [set up a payload logging database](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-cdb-connect), and the [Watson Machine Learning instance](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-cwml-wml) where your AI models and deployments are stored.

- **Work with monitors**: For each deployment, configure how {{site.data.keyword.aios_short}} will monitor that deployment. You can monitor for:

    - [Fairness](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-mf-monitor)
    - [Accuracy](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-acc-monitor)

- **View and edit monitored data**: The {{site.data.keyword.aios_short}} [dashboard](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-iov-insights) lets you easily view key insights and identify issues for your deployments. Visualization of individual data points for each monitored feature provides additional detail.

## Limitations
{: #abt-limits}

- The current release only supports one database, one Watson Machine Learning instance, and one instance of {{site.data.keyword.aios_short}}.

- The database and Watson Machine Learning instance must be deployed in the same {{site.data.keyword.cloud_notm}} account.

- {{site.data.keyword.aios_short}} uses a PostgreSQL or Db2 database to store model deployment output and retraining data. Lite Db2 plans are not currently supported.

- There is a license limit of 20 deployed models per instance of {{site.data.keyword.aios_short}}.

- Currently, explanations cannot be generated for images which are greater than 1 MB in size.

## Supported model types
{: #abt-models}

Table 1. Model support details

| Algorithms | **Fairness** | **Auto-debias** | **Explain** | **Accuracy** |
|:---|:---:|:---:|:---:|:---:|
| **Structured Classification** | Yes | Yes<sup>1</sup> | Yes<sup>1</sup> | Yes |
| **Structured Regression**     | Yes | Coming soon | Yes | Yes |
| **Text Classification**       | No - active research topic | No - active research topic | Yes<sup>1</sup> | No |
| **Image Classification**      | No - active research topic | No - active research topic | Yes<sup>1</sup> | No ||
{: caption="Model support details" caption-side="top"}

<sup>1</sup> If your model / framework outputs prediction probabilities

## Supported frameworks
{: #abt-frame}

Table 1. Framework support details

| Algorithms | **Out-of-the-box support** | **[Custom environment](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-ccust-custom) or Python function support** |
|:---|:---:|:---:|
| **Structured Classification** | Spark mllib on WML, AWS Sagemaker Native<sup>1</sup>, Azure ML Studio Native | Scikit-Learn, XGboost, SPSS, Keras, Tensorflow,  Pytorch, Caffe,  or any other framework of your choice |
| **Structured Regression**     | Spark mllib on WML, AWS Sagemaker Native<sup>1</sup>, Azure ML Studio Native | Scikit-Learn, XGboost, SPSS, Keras, Tensorflow,  Pytorch, Caffe,  or any other framework of your choice |
| **Text Classification**       | Spark mllib on WML | Coming soon: Keras, Tensorflow, Pytorch, Caffe, and most others |
| **Image Classification**      | Keras on WML | Coming soon: Keras, Tensorflow, Pytorch, Caffe, and most others ||
{: caption="Framework support details" caption-side="top"}

<sup>1</sup> AWS built-in algorithms

## Browser support
{: #abt-browser}

The {{site.data.keyword.aios_short}} service tooling requires the same level of browser software as is required by {{site.data.keyword.cloud_notm}}. See the {{site.data.keyword.cloud_notm}} [Prerequisites](/docs/overview?topic=overview-prereqs-platform#browsers) topic for details.

## ModelOps CLI tool
{: #abt-mopscli}

The [{{site.data.keyword.aios_short}} CLI model operations tool ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/IBM-Watson/aiopenscale-modelops-cli){: new_window} allows you to execute tasks related to the lifecycle management of machine learning models. This tool is complementary to the {{site.data.keyword.cloud_notm}} CLI tool, augmented with the [machine learning plugin ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/DSXDOC/analyze-data/ml_dlaas_environment.html){: new_window}.

## Python client
{: #abt-python}

The [{{site.data.keyword.aios_short}} Python client ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://ai-openscale-python-client.mybluemix.net/){: new_window} is a Python library that allows you to work directly with the {{site.data.keyword.aios_short}} service on {{site.data.keyword.cloud_notm}}. You can use the Python client, instead of the {{site.data.keyword.aios_short}} client UI, to directly configure a logging database, bind your machine learning engine, and select and monitor deployments. For examples using the Python client in this way, see the [{{site.data.keyword.aios_short}} sample notebooks ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks).

## Next steps
{: #abt-next}

- [Get started](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-gs-get-started) with the service.
- View the [API Reference material ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/ai-openscale){: new_window}.

Still have questions? [Contact IBM ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/account/reg/us-en/signup?formid=MAIL-watson){: new_window}.
