---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-07"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# Accuracy
{: #acc-monitor}

Accuracy lets you know how well your model predicts outcomes.
{: shortdesc}

## Understanding Accuracy
{: #acc-understand}

Accuracy can mean different things depending on the type of the algorithm:

- *Multi-class classification*: Accuracy measures the number of times any class was predicted correctly, normalized by the number of data points. For more details, see [Multi-class classification ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://spark.apache.org/docs/2.1.0/mllib-evaluation-metrics.html#multiclass-classification) in the Apache Spark documentation.

- *Binary classification*: For a binary classification algorithm, accuracy is measured as the area under an ROC curve. See [Binary classification ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://spark.apache.org/docs/2.1.0/mllib-evaluation-metrics.html#binary-classification) in the Apache Spark documentation for more details.

- *Regression*: Regression algorithms are measured using the Coefficient of Determination, or R2. For more details, see [Regression model evaluation ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://spark.apache.org/docs/2.1.0/mllib-evaluation-metrics.html#regression-model-evaluation) in the Apache Spark documentation.

### How it works
{: #acc-uhow}


You need to add manually-labelled feedback data through the {{site.data.keyword.aios_short}} UI as shown below, using a [Python client ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://ai-openscale-python-client.mybluemix.net/#feedbacklogging){: new_window} or [Rest API ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/apidocs/ai-openscale#post-feedback-payload){: new_window}.

Review [Supported model types](/docs/services/ai-openscale?topic=ai-openscale-in-ov#in-mod) and [Supported frameworks](/docs/services/ai-openscale?topic=ai-openscale-in-ov#in-fram) for accuracy monitoring limitations.

## Configuring the Accuracy monitor
{: #acc-config}

1.  From the *What is Accuracy?* page, click **Next** to start the configuration process.

    ![What is Accuracy? page](images/accuracy-what-is.png)

1.  On the *Set accuracy threshold* page, select a value that represents an acceptable accuracy level.

    Accuracy is a value synthesized from relevant data science metrics associated with each particular model type. The score is a normalized measure to allow you to easily compare accuracy across different model types. In typical situations, an accuracy score of 80 is sufficient.
    {: note}

    ![Set accuracy limit](images/accuracy-set-limit.png)

    Click **Next** to continue.

1.  Now, set minimum and maximum sample sizes. Minimum size prevents measuring Accuracy until a minimum number of records are available in the evaluation dataset; this ensures the sample size is not too small to skew results. The maximum sample size helps better manage the time and effort it takes to evaluate the dataset; only the most recent records will be evaluated if this size is exceeded.

     ![Configure sample size](images/accuracy-config-sample.png)

1.  Click the **Next** button.

    A summary of your selections is presented for review. If you want to change anything, click the **Edit** link for that section.

1.  Click **Save** to complete your configuration.

You are now presented with the option to directly provide feedback data to your model, to evaluate for accuracy.

  ![Send feedback data](images/accuracy-send-feedback.png)

Select the *Add Feedback Data* button to upload a CSV-formatted data file; set the delimiter to match your data.

The feedback CSV file is expected to have all feature values, and the manually assigned target/label value. For example, the drug model training data contains feature values `"AGE"`, `"SEX"`, `"BP"`, `"CHOLESTEROL"`,`"NA"`,`"K"`, and the target/label value `"DRUG"`. The feedback CSV file needs to include values for those fields; an example would look like `[43, M, HIGH, NORMAL, 0.6345, 1.4587, DrugX]`. If a header is provided for the feedback CSV file, then field names are mapped using the header. Otherwise the field order **MUST** be exactly the same as in the training schema.
{: important}

  ![Accuracy delimiter](images/accuracy-delimit.png)

File sizes are currently limited to 8MB.
{: note}

Alternately, you can publish feedback data using the provided `cURL` or `Python` code snippets.

The fields and values in the code snippets need to be substituted with your real values, as the ones provided are only examples.
{: important}

You can also choose **Exit** to skip this optional step; you will still be able to upload a CSV file for evaluation at a later time.

## Next steps
{: #acc-next}

From the *Configure monitors* page, you can select another monitoring category.
