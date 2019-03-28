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

# Monitoring explainability
{: #ie-ov}

For each deployment, you can see explainability data for specific transactions.
{: shortdesc}

## Explaining transactions
{: #ie-view}

In the selected deployment tile, select the **Explain a transaction** tab ( ![Explain a transaction tab](images/insight-transact-tab.png) ) in the navigator and enter a transaction ID.

Whenever data is sent to the model for scoring, it sets a transaction ID in the HTTP header by setting the `X-Global-Transaction-Id` field. This transaction ID gets stored in the payload table. To find an explanation of the model behavior for a particular scoring, specify the transaction ID associated with that scoring request. This behavior applies only to Watson Machine Learning (WML) transactions, and is not applicable for non-WML transactions.
{: note}

### Finding a transaction ID in {{site.data.keyword.aios_short}}
{: #ie-find}

1.  From the time chart for your deployment, slide the marker across the chart and click the **View details** link to [visualize data for a specific hour](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-itc-timechart#itc-data-visual).
1.  Click the **View transactions** button to [view the list of transaction IDs](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-itc-timechart#itc-tra).
1.  Copy one of the transaction IDs from the list, paste it into the search box on the **Explain a transaction** page, and press Enter.

    The list of transaction IDs also has the option to simply click the **Explain** link in the Action column for any transaction ID, which will open that transaction in the Explainability tab.
    {: note}

  See the following sections for examples of explanations for different types of models.

  ![Explainability transaction ID](images/insight-explain-trans-id.png)

## Categorical model example
{: #ie-class}

This example of explainability is for a binary classification model that approves or denies insurance claims. You can see the factors that contributed positively or negatively to the final outcome of `DENIED` in this case.

The feature *POLICY AGE* having a value of `< 1 year` had the maximum impact in the model deciding a DENIED outcome. The other features that contributed to this outcome were *CLAIM FREQUENCY* (`High`) and *AGE* (`18`), with only a minor impact from *CAR VALUE* (`$50,000`).

![Explainability binary classification](images/insight-explain-binary.png)

While the charts are useful in showing the most significant factors in determining the outcome of a transaction, classification models can also include advanced explanations, detailed in the `Minimum changes for Approved outcome` and `Minimum changes for this outcome` sections.

Advanced explanations are not available for regression, image, and unstructured text models.
{: note}

The `Minimum changes for Approved outcome` tells us that, if the values of the features were changed to the values listed in this section, then the prediction of the model will change.

Likewise, the `Minimum changes for this outcome` tells us that, even if the values of the features were changed to those listed in this section, the prediction of the model would not have changed.

Thus, these two values tell us the behavior of the model in the vicinity of the data point for which the explanation is being generated.

![Explainability binary classification](images/insight-explain-binary2.png)

## Image model example
{: #ie-image}

For an image classification model example of explainability, you can see which parts of an image contributed positively to the predicted outcome and which contributed negatively. In the below example, the image on the right show the parts which impacted positively to the prediction and the image on the left shows the parts of images that had a negative impact on the outcome.

Currently, explanations cannot be generated for images which are greater than 1 MB in size.
{: note}

![Explainability image classification](images/insight-explain-image.png)

## Unstructured text model example
{: #ie-unstruct}

Finally, this example of explainability shows a classification model that evaluates unstructured text. The explanation shows the keywords that had a positive as well as a negative impact on the model prediction. We also show the position of the identified keywords in the original text which was fed as input to the model.

![Explainability image classification](images/insight-explain-text.png)
