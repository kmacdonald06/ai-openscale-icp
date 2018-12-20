---

copyright:
  years: 2018
lastupdated: "2018-12-14"

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

{{site.data.keyword.aios_full}} is an enterprise-grade environment for AI-infused applications, providing enterprises visibility into how AI is being built, used, and delivering return on investment, at the scale of your business.
{: shortdesc}

## Implementation

Here's how you will implement {{site.data.keyword.aios_short}}:

- **Configure {{site.data.keyword.aios_short}}**: With the easy-to-use graphical environment, [set up a payload logging database](connect-db.html), and the [Watson Machine Learning instance](connect-wml.html) where your AI models and deployments are stored.

- **Work with monitors**: For each deployment, configure how {{site.data.keyword.aios_short}} will monitor that deployment. You can monitor for:

    - [Fairness](monitor-fairness.html)
    - [Accuracy](monitor-accuracy.html)

- **View and edit monitored data**: The {{site.data.keyword.aios_short}} [dashboard](insight-overview.html) lets you easily view key insights and identify issues for your deployments. Visualization of individual data points for each monitored feature provides additional detail.

## Limitations

- The current release only supports one database, one Watson Machine Learning instance, and one instance of {{site.data.keyword.aios_short}}

- The database and Watson Machine Learning instance must be deployed in the same {{site.data.keyword.Bluemix_notm}} account.

- There is a license limit of 20 deployed models per instance of {{site.data.keyword.aios_short}}.

- Currently, explanations cannot be generated for images which are greater than 1 MB in size.

## Supported model types

Table 1. Model support details

| Algorithms | **Fairness** | **Auto-debias** | **Explain** | **Accuracy** |
|:---|:---:|:---:|:---:|:---:|
| **Structured Classification** | Yes | Yes<sup>1 | Yes | Yes |
| **Structured Regression**     | Yes | Coming soon | Yes<sup>1 | Yes |
| **Text Classification**       | No - active research topic | No - active research topic | Yes | No |
| **Image Classification**      | No - active research topic | No - active research topic | Yes | No ||
{: caption="Model support details" caption-side="top"}

<sup>1</sup> If your model / framework outputs prediction probabilities

## Supported frameworks

Table 1. Framework support details

| Algorithms | **Out-of-the-box support** | **[Custom environment](connect-other.html#custom-works) or Python function support** |
|:---|:---:|:---:|
| **Structured Classification** | Spark mllib on WML, AWS Sagemaker Native, Azure ML Studio Native | Scikit-Learn, XGboost, SPSS, Keras, Tensorflow,  Pytorch, Caffe,  or any other framework of your choice |
| **Structured Regression**     | Spark mllib on WML, AWS Sagemaker Native, Azure ML Studio Native | Scikit-Learn, XGboost, SPSS, Keras, Tensorflow,  Pytorch, Caffe,  or any other framework of your choice |
| **Text Classification**       | Spark mllib on WML | Coming soon: Keras, Tensorflow, Pytorch, Caffe, and most others |
| **Image Classification**      | Keras on WML | Coming soon: Keras, Tensorflow, Pytorch, Caffe, and most others ||
{: caption="Framework support details" caption-side="top"}

## Browser support

The {{site.data.keyword.aios_short}} service tooling requires the same level of browser software as is required by {{site.data.keyword.Bluemix_notm}}. See the {{site.data.keyword.Bluemix_notm}} [Prerequisites ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/docs/overview/prereqs.html#browsers){: new_window} topic for details.

## ModelOps CLI tool

The [{{site.data.keyword.aios_short}} CLI model operations tool ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/IBM-Watson/aiopenscale-modelops-cli) allows you to execute tasks related to the lifecycle management of machine learning models. This tool is complementary to the {{site.data.keyword.Bluemix_notm}} CLI tool, augmented with the [machine learning plugin](https://www.ibm.com/support/knowledgecenter/DSXDOC/analyze-data/ml_dlaas_environment.html).

## Python client

The [{{site.data.keyword.aios_short}} Python client ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://ai-openscale-python-client.mybluemix.net/) is a Python library that allows you to work directly with the {{site.data.keyword.aios_short}} service on {{site.data.keyword.Bluemix_notm}}. You can use the Python client, instead of the {{site.data.keyword.aios_short}} client UI, to directly configure a logging database, bind your machine learning engine, and select and monitor deployments. For an example using the Python client in this way, see both the [CARS4U action recommendation - model ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/CARS4U%20action%20recommendation%20-%20model.ipynb) and the [Data Mart configuration and usage with ibm-ai-openscale python package ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Data%20Mart%20configuration%20and%20usage%20-%20CARS4U.ipynb) notebooks.

## Next steps

- [Get started](getting-started.html) with the service.
- View the [API Reference material ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/apidocs/ai-openscale){: new_window}.

Still have questions? [Contact IBM ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/account/reg/us-en/signup?formid=MAIL-watson){: new_window}.
