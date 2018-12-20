---

copyright:
  years: 2018
lastupdated: "2018-12-14"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# Release notes

This document outlines new features and known issues for {{site.data.keyword.aios_full_notm}}.
{: shortdesc}

## 14 December 2018
{: #14December2018}

The following new features, changes, and known issues with the service are available.

### New features and changes

{{site.data.keyword.aios_short}} features that have been added or enhanced since the beta release include:

- __*General availability*__: The General Availability (GA) release of {{site.data.keyword.aios_full_notm}} on IBM Cloud Private for Data V1.2, See the [installation instructions](/docs/services/ai-openscale-icp/install-icp.html#install) for more information.

- __*Support for your model type*__: In addition to AI model deployments in Watson Machine Learning, {{site.data.keyword.aios_short}} supports model deployments in Microsoft Azure, Amazon SageMaker, and Custom environments. See [Supported model types](/docs/services/ai-openscale-icp/index.html#supported-model-types) for more information.

- __*Bias monitoring*__: Support for protected attributes of type `float` and `double`, and bias detection on linear regression models. And {{site.data.keyword.aios_short}} can automatically de-bias your AI model for you. See [Understanding fairness](/docs/services/ai-openscale-icp/monitor-fairness.html#understand-fair) for more information.

- __*Explainability*__: Support for regression models, Python functions, and complementary contrastive explanations. See [Monitoring explainability](/docs/services/ai-openscale-icp/insight-timechart.html#insight-explain) for more information.

- __*Data Store*__: Quality monitoring without reliance on Watson Machine Learning, and the ability to use your own database, whether it's Db2, Postgres or Db2 on Cloud.

- __*NeuNetS (Beta)*__: The IBM Neural Network Synthesizer (NeuNetS) is available as a beta release (public cloud only). See the [NeuNetS documentation](https://dataplatform.cloud.ibm.com/ml/neunets) for more information.

- __*Enhanced UI*__: The {{site.data.keyword.aios_short}} UI has been improved to include a runtime histogram distribution with toggle for training data, Model ID & Versioning, and a Transaction ID table from the histogram. See [Data visualization](/docs/services/ai-openscale-icp/insight-timechart.html#insight-data-visual) for more information.

- __*Tutorial module*__: To automate provisioning and configuration, and to see an {{site.data.keyword.aios_full_notm}} instance, including sample data, you can install and run a Python module. See [Automated setup](/docs/services/ai-openscale-icp/getting-started.html#module)

### Known issues

- **Microsoft Azure**

    - Of the two types of Azure Machine Learning web services, only the `New` type is supported by {{site.data.keyword.aios_short}}. The `Classic` type is not supported.

    - In the Azure web service, the default input name is `"input1"`. Currently, this field is mandated for {{site.data.keyword.aios_short}} and, if it is missing, {{site.data.keyword.aios_short}} will not work.

      If your Azure web service does not use the default name, change the input field name to `"input1"`, then the code will work.

- **AWS SageMaker**

    - When an invalid AWS SageMaker model exists in an AWS SageMaker engine that has been associated with a `binding_id` in {{site.data.keyword.aios_short}}, the service may return a `NullPointerException`.

      This issue may also appear during the onboarding step when you trying to list model deployments which contain an invalid model, and it may also occur when you are trying to list the model deployments from a Python API client when an invalid model exists.

    - The AWS SageMaker BlazingText algorithm input payload format is not supported in the current release of {{site.data.keyword.aios_short}}.

- **Code snippets invalid**

    - Both cURL and Python code snippets provided for monitor configuration are invalid. Correct code snippets for cURL are provided here:

      *Payload logging*

      ```cURL
      # Generate an ICP access token by passing an ICP username as $USERNAME, and ICP password as $PASSWORD in the request below

      curl -k -X GET \
      -user "$USERNAME:$PASSWORD" \
      "https://{{icp_hostname}:{{icp_port}}/v1/preauth/validateAuth"

      # the above CURL request will return an auth token under "accessToken", that you will use as {icp_token} in the payload logging request below
      # TODO: manually define and pass:
      # request - input to scoring endpoint in supported by AI OpenScale format - replace sample fields and values with proper ones
      # response - output from scored model in supported by AI OpenScale format - replace sample fields and values with proper ones
      # - $SCORING_ID - ID of the scoring transaction
      # - $SCORING_TIME - Time (ms) taken to make prediction (for performance monitoring)

      SCORING_PAYLOAD='[{
        "scoring_id": "$SCORING_ID",
        "response_time": "$SCORING_TIME",
        "request": {
          "fields": ["AGE", "SEX", "BP", "CHOLESTEROL", "NA", "K"],
          "values": [[28, "F", "LOW", "HIGH", 0.61, 0.026]]
      },
      "response": {
        "fields": ["AGE", "SEX", "BP", "CHOLESTEROL", "NA", "K", "probability", "prediction", "DRUG"],
        "values": [[28, "F", "LOW", "HIGH", 0.61, 0.026, [0.82, 0.07, 0.0, 0.05, 0.03], 0.0, "drugY"]]
        },
        "binding_id": "{{binding_id}}",
        "subscription_id": "{{subscription_id}}",
        "deployment_id": "{{deployment_id}}"
      }]'

      curl -k -X POST https://{{icp_hostname}:{{icp_port}}/v1/data_marts/{{data_mart_id}}/scoring_payloads -d "$SCORING_PAYLOAD" \
      --header 'Content-Type: application/json' --header 'Accept: application/json' --header "Authorization: Bearer $ICP_TOKEN"
      ```

      *Feedback logging*

      ```cURL
      # Generate an ICP access token by passing an ICP username as $USERNAME, and ICP password as $PASSWORD in the request below

      curl -k -X GET \
      --user "$USERNAME:$PASSWORD" \
      "https://{{icp_hostname}:{{icp_port}}/v1/preauth/validateAuth"

      # the above CURL request will return an auth token under "accessToken" key that you will use as {icp_token} in the payload logging request below
      # TODO: manually define and pass:
      # fields - list of fields names - replace sample values with proper ones
      # values - feedback data records - replace sample values with proper ones
      # - $SCORING_ID - ID of the scoring transaction
      # - $SCORING_TIME - Time (ms) taken to make prediction (for performance monitoring)

      FEEDBACK_DATA='{
        "fields": ["AGE", "SEX", "BP", "CHOLESTEROL", "NA", "K", "DRUG"],
        "values": [[28, "F", "LOW", "HIGH", 0.61, 0.026, "drugB"]],
        "binding_id": "{{binding_id}}",
        "subscription_id": "{{subscription_id}}"
      }'

      curl -k -X POST https://{{icp_hostname}:{{icp_port}}/v1/data_marts/{{data_mart_id}}/feedback_payloads -d "$FEEDBACK_DATA" \
      --header 'Content-Type: application/json' --header 'Accept: application/json' --header "Authorization: Bearer $ICP_TOKEN"
      ```

      *Bias Remediation*

      ```cURL
      # Generate an ICP access token by replacing ICP username as <USERNAME>, and ICP password as <PASSWORD> in the request below. Also replace the <HOSTNAME>:<PORT>

      curl -k -X GET --user "<USERNAME>:<PASSWORD>" "https://<HOSTNAME>:<PORT>/v1/preauth/validateAuth"

      # the above CURL request will return an auth token under "accessToken", use this value for <TOKEN> in the below request

      # Replace "fields" - list of features column from payload logging - replace sample values with proper ones
      # Replace "values" - payload logging data records - replace sample values with proper ones

      curl -X POST "https://<HOSTNAME>:<PORT>/v1/data_marts/<DATA_MART_ID>/service_bindings/<SERVICE_BINDING_ID>/subscriptions/<ASSET_ID>/deployments/<DEPLOYMENT_ID>/online" -H "accept: application/json" -H "Authorization: bearer <TOKEN>" -H "X-Global-Transaction-Id: " -H "Content-Type: application/json" -d "{ \"fields\": [ \"field1\", \"field2\", \"field3\" ], \"values\": [ [ \"field1Value1\", \"field2Value1\", \"field3Value1\" ], [ \"field1Value2\", \"field2Value2\", \"field3Value2\" ] ]}"
      ```

## 17 September 2018
{: #17September2018}

### New features and changes

- **Beta preview release** - Welcome to the beta preview release of {{site.data.keyword.aios_full_notm}}.
