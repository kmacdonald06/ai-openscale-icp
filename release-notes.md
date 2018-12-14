---

copyright:
  years: 2018
lastupdated: "2018-12-13"

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

The following new features and changes to the service are available.

### New features and changes

- **GA release**

    - Welcome to the General Availability (GA) release of {{site.data.keyword.aios_full_notm}}. This release contains the following features:

        - __*Releases*__: {{site.data.keyword.aios_short}} is available as an IBM Cloud Standard (paid) plan, and on IBM Cloud Private for Data V1.2

          The IBM Neural Network Synthesizer (NeuNetS) is also available as a beta release (public cloud only). See the [NeuNetS documentation](https://dataplatform.cloud.ibm.com/ml/neunets) for more information

        - __*Enhanced UI*__: The {{site.data.keyword.aios_short}} UI now includes a runtime histogram distribution with toggle, Model ID & Versioning, and a Transaction ID table from the histogram

        - __*Bias*__: Support for protected attributes of type `float` and `double`, bias detection on linear regression models, and bias remediation

        - __*Explainability*__: Support for regression models, Python functions, and IBM Explainer, along with LIME, algorithms

        - __*Data Store*__: Quality monitoring without reliance on Watson Machine Learning, and Db2 support

### Known issues

- **Microsoft Azure**

    - Of the two types of Azure Machine Learning web services, only the `New` type is supported by {{site.data.keyword.aios_short}}. The `Classic` type is not supported.

    - In the Azure web service, the default input name is `"input1"`. Currently, this field is mandated for {{site.data.keyword.aios_short}} and, if it is missing, Accuracy monitoring will fail.

      If your Azure web service does not use the default name, change the input field name to `"input1"`, then the code will work.

- **AWS SageMaker**

    - When an invalid AWS SageMaker model exists in an AWS SageMaker engine that has been associated with a `binding_id` in {{site.data.keyword.aios_short}}, the service may return a `NullPointerException`.

      This issue may also appear during the onboarding step when you trying to list model deployments which contain an invalid model, and it may also occur when you are trying to list the model deployments from a Python API client when an invalid model exists.

    - The AWS SageMaker BlazingText algorithm input payload format is not supported in the current release of {{site.data.keyword.aios_short}}.

- **Code snippets invalid**

    - Both cURL and Python code snippets provided for monitor configuration are invalid. Correct code snippets are provided here:

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

## 17 September 2018
{: #17September2018}

### New features and changes

- **Beta preview release** - Welcome to the beta preview release of {{site.data.keyword.aios_full_notm}}.
