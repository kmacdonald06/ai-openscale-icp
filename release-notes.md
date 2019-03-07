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

# Release notes
{: #rn-relnotes}

This document outlines new features and known issues for {{site.data.keyword.aios_full_notm}}.
{: shortdesc}

## 5 March 2019
{: #rn-5March2019}

The following new features and changes to the service are available.

### New features and changes
{: #rn-5March2019nf}

{{site.data.keyword.aios_short}} features that have been added or enhanced since the previous release include:

- __*New Credit Risk model*__: A new Credit Risk model example/tutorial is supported for all scoring engines. For more information see the [Getting started](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-gs-get-started#gs-get-started) and [Additional resources](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-arsc-ov#arsc-ov) topics.

- __*Computing debias*__: You can toggle between your production model and a de-biased model created by {{site.data.keyword.aios_short}}. See [Production model and De-biased model](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-itc-timechart#itc-prdb) and [Understanding how de-biasing works](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-mf-monitor#mf-debias) for more information.

## 22 February 2019
{: #rn-22February2019}

The following new features and changes to the service are available.

### New features and changes
{: #rn-22February2019nf}

{{site.data.keyword.aios_short}} features that have been added or enhanced since the previous release include:

- __*UI updates*__: You can import a JSON file to programmatically configure all monitors and features during subscription creation. You can also export the configuration file. See the [Configure deployment subscription using JSON files](/docs/services/ai-openscale?topic=ai-openscale-cf-ov) topic for more information.

## 7 February 2019
{: #rn-7February2019}

The following new features and changes to the service are available.

### New features and changes
{: #rn-7February2019nf}

{{site.data.keyword.aios_short}} features that have been added or enhanced since the previous release include:

- __*UI updates*__: Several improvements have been made to the {{site.data.keyword.aios_short}} user interface, including buttons to [check fairness and accuracy on demand](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdep), and the ability to see a list of transactions from the [fairness details chart](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-tra).

- __*Explainability enhancements*__: All numbers now have the same precision/scale across Pertinent Positive (PP) and Pertinent Negative (PN) values.

- __*IBM SPSS Collaboration & Deployment Services support*__: IBM SPSS C&DS is now a supported machine learning service instance. See [Specifying an IBM SPSS Collaboration & Deployment Services instance](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-cspss-spss)

- __*Db2 SSL support*__: {{site.data.keyword.aios_short}} supports passing self-signed certificates (Base-64 encoded) with Db2 credentials.

- __*IBM Cloud Database support*__: {{site.data.keyword.aios_short}} now supports Databases for PostgreSQL, in addition to Compose for PostgreSQL and Db2)

### Known issues
{: #rn-7February2019ki}

- **Python functions not supported**

    -  Bias checking, de-biasing, and explainability is not supported for Python functions, in the current release.

- **Explainability support limitations**

    - When building your models, do not include the target (label) column from the input request for scoring. If the model requires the target column to be included in the input request, then bias checking, de-biasing, and explainability will not work.

    - Image-based models cannot be deployed on Watson Machine Learning (WML), so the Explainability service does not support image-based models; this is a WML limitation.

- **Custom ML service instance**

    - The [Python module](/docs/services/ai-openscale?topic=ai-openscale-as-module) does not currently have Explainability working for the Custom service instance. This is because, to generate an explanation, the Custom service instance should have a numerical prediction in the response data, which is not included with the module script. Explainability will not be supported on the Custom service instance if the model that is sourcing the custom application returns a non-numerical prediction in the scoring response.

- **Microsoft Azure**

    - Some clusters may have an issue with obtaining web service metadata for Azure, when there are a large number of web services. When this occurs, the deployment response from Azure appears to be empty.

      This may be caused by timeout values that are exceeded by the time it takes to obtain this metadata. For example, if you are using the HAProxy load balancer, you may need to work around this issue by:

        - Logging into the load balancer node and updating `/etc/haproxy/haproxy.cfg` to set the client and server timeout from `1m` to `5m`:

          ```bash
          timeout client           5m
          timeout server           5m
          ```

        - Running `systemctl restart haproxy` to restart the HAProxy load balancer.

      If you are using a different load balancer, other than HAProxy, you may need to adjust timeout values in a similar fashion.
      {: note}

## 14 December 2018
{: #rn-14December2018}

The following new features and changes to the service are available.

### New features and changes
{: #rn-14December2018nf}

- **GA release**

    - Welcome to the General Availability (GA) release of {{site.data.keyword.aios_full_notm}}. This release contains the following features:

        - __*Releases*__: {{site.data.keyword.aios_short}} is available as an IBM Cloud Standard (paid) plan, and on IBM Cloud Private for Data V1.2

          The IBM Neural Network Synthesizer (NeuNetS) is also available as a beta release (public cloud only). See the [NeuNetS documentation ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://dataplatform.cloud.ibm.com/ml/neunets) for more information.

        - __*Enhanced UI*__: The {{site.data.keyword.aios_short}} UI now includes a runtime histogram distribution with toggle, Model ID & Versioning, and a Transaction ID table from the histogram

        - __*Bias*__: Support for protected attributes of type `float` and `double`, bias detection on linear regression models, and bias remediation

        - __*Explainability*__: Support for regression models, Python functions, and IBM Explainer, along with LIME, algorithms

        - __*Data Store*__: Quality monitoring without reliance on Watson Machine Learning, and Db2 support

### Known issues
{: #rn-14December2018ki}

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
      # request - input to scoring endpoint in supported by {{site.data.keyword.aios_short}} format - replace sample fields and values with proper ones
      # response - output from scored model in supported by {{site.data.keyword.aios_short}} format - replace sample fields and values with proper ones
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

    - Java code snippet provided for debiasing endpoint is invalid. Correct code snippet is provided here:

      *Debias endpoint*

      ```java
      /**
      At runtime you need to replace values for the following

      <HOSTNAME> - Host Name eg: aiopenscale.test.cloud.ibm.com
      <PORT> - Server Port
      <DATA_MART_ID> - DataMart id
      <SERVICE_BINDING_ID> - Service Binding id
      <ASSET_ID> - Asset id or the model id
      <DEPLOYMENT_ID> - Deployment id
      <TOKEN> - Bearer token

      */
      import org.apache.http.HttpVersion;
      import org.apache.http.client.fluent.Request;
      import org.apache.http.entity.ContentType;

      String bearerToken = "Bearer <TOKEN>";
      String URL = "https://<HOSTNAME>:<PORT>/v1/data_marts/<DATA_MART_ID>/service_bindings/<SERVICE_BINDING_ID>/subscriptions/<ASSET_ID>/deployments/<DEPLOYMENT_ID>/online";

      String payload = "{ \"fields\": [ \"field1\", \"field2\", \"field3\" ], \"values\": [ [ \"field1Value1\", \"field2Value1\", \"field3Value1\" ], [ \"field1Value2\", \"field2Value2\", \"field3Value2\" ]] }";

      byte[] res = Request.Post(URL).addHeader("Authorization", bearerToken).useExpectContinue().version(HttpVersion.HTTP_1_1)
                .bodyString(payload, ContentType.APPLICATION_JSON).execute().returnContent().asBytes();
      ```

## 17 September 2018
{: #rn-17September2018}

### New features and changes
{: #rn-17September2018nf}

- **Beta preview release** - Welcome to the beta preview release of {{site.data.keyword.aios_full_notm}}.
